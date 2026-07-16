+++
title = "How easy and securely is to backup your computer?"
date = "2023-03-12T12:09:19Z"
description = "We all know that we should always back up our stuff and that there's lots of things that can go wrong..."
draft = false
tags = ["tutorial", "backup"]
source = "dev.to"
original_url = "https://dev.to/kimus/how-easy-and-securely-is-to-backup-your-computer-2g7d"
+++
We all know that we should always back up our stuff and that there's lots of things that can go wrong if we don't:
-   Hard drives could fail or loss data
-   Files of folders can accidentally be deleted, become corrupt, or maybe accidentally over wrote a newer one
-   Viruses can corrupt or delete files
-   You may upgrade to a new computer and need to move your files.

For what ever reason, and depending on the importance of that information, you could be in a seriously problem or loose hours of work.

[Restic](https://restic.net/)  is the backup software that I'm using to backup my files. Its Open Source, with strong encryption, versioning, and only transfers what you need to, so you don't use up more space than you need to. Works on Linux, Mac, BSD, and Windows, however if you want to use Restic, you still need to know your way around a shell.

This is one of the tools that I use to [restore my computer from scratch](https://dev.to/kimus/my-macos-from-scratch-setup-6ja).

## Restic Setup

Let's create the restic configuration folders (you can create on any other path, this is just my preference):

```bash
mkdir -p ~/.restic/backups
```

And create the `~/.restic/cron.sh` script to perform the backups:

```bash
#!/usr/bin/env zsh
RESTIC_ROOT="$( cd "$(dirname "$0")" ; pwd -P )"

for BACKUP_ROOT in $RESTIC_ROOT/backups/* ; do
    source "$BACKUP_ROOT/env"

    BACKUP_DIR=$(cat "$BACKUP_ROOT/path")

    restic backup $BACKUP_DIR -q --exclude-file="$BACKUP_ROOT/excludes" --exclude-caches
    
    restic forget -q --keep-last 2 --prune
done
```

This script will go throw all backup configurations and perform the backup and forget restic commands for each of them.

Note that I'm keeping the last two backups, but there's a lot of options in restic. You can choose to keep weekly, monthly or yearly backups. Just go to their documentation about [keep policy](https://restic.readthedocs.io/en/stable/060_forget.html#removing-snapshots-according-to-a-policy).


## Backup configuration

So, let's create our first backup configuration. In this case, I'll backup stuff from my user home folder.

Instead of resting prompting for the password, and manually creating one, I prefer to generate a random password. And so, using `openssl` to generate a bunch or random characters:

```bash
openssl rand -hex 64 > ~/.restic/backups/home/password
```

> Remembering your password is important! If you lose it, you won’t be able to access data stored in the repository because all data it's encrypted.

After that, store my home folder path:

```bash
echo $HOME > ~/.restic/backups/home/path
```

Set [environment configurations](https://restic.readthedocs.io/en/stable/040_backup.html#environment-variables) for this backup. I'm using [B2 Cloud Storage](https://www.backblaze.com/b2/cloud-storage.html) for this. It's free for the first 10 GB. You can use any of the restic [supported repositories](https://restic.readthedocs.io/en/stable/030_preparing_a_new_repo.html):

```bash
cat > ~/.restic/backups/home/env << EOL
export RESTIC_REPOSITORY=b2:bucket-name:path-to-store
export B2_ACCOUNT_ID=<your account id here>
export B2_ACCOUNT_KEY=<your account key here>
export RESTIC_PASSWORD_FILE=~/.restic/backups/home/password
EOL
```

Create the [excludes](https://restic.readthedocs.io/en/stable/040_backup.html#excluding-files) file. In reality this is where I say restic what to backup in every line starting with the `!` sign:

```bash
cat > ~/.restic/backups/home/excludes << EOL
# excluding any directory, then selectively add back some of them
/Users/kimus/*
!/Users/kimus/Documents
!/Users/kimus/Develop
/Users/kimus/Develop/**/*.gz

# dotfiles
!/Users/kimus/.local/share/chezmoi
!/Users/kimus/.gitconfig
!/Users/kimus/.restic
!/Users/kimus/.ssh
!/Users/kimus/.zshrc
!/Users/kimus/.zprofile
!/Users/kimus/.kube
/Users/kimus/.kube/cache

# global ignores
node_modules
.next/cache
.DS_Store
EOL
```

Please note that this is my initial configuration, and yours could be different. You should take some time to make sure your are backing up all information that you need and excluding files that you don't. Doing so, the backup will be optimised in size and that will provide faster backup times and less payments in your cloud provider.

In the end will get something like this:

```bash
.restic
├── backups
│   └── home
│       ├── env
│       ├── excludes
│       ├── password
│       └── path
└── cron.sh
```

In my case I'm trying to backup only the essencial files, like the dotfiles, source code, documents, etc. All files or folders not needed I will exclude them. And so, to test the configuration, and check all the files this configuration will backup you can use the following:

```bash
source ~/.restic/backups/user/env
restic backup $HOME --exclude-file="$HOME/.restic/backups/home/excludes" --dry-run -vv
```

> check for files bigger then a size:
> `du -ch -t 1M Develop | grep -v node_modules`


Manually execute the `cron.sh` and you will get your first backup. To check, you can execute the `snapshots` command. You will need the source the env file if not done yet.

```bash
source ~/.restic/backups/user/env
$ restic snapshots
repository b4fadbba opened (version 2, compression level auto)
ID        Time                 Host                   Tags        Paths
------------------------------------------------------------------------------
e4183d6f  2023-03-10 12:00:00  Helders-MacBook-Pro14              /Users/kimus
------------------------------------------------------------------------------
1 snapshot
```

And to check the size of the snapshot, and other ifnormation you could use the `stats` command. I use this to check and control the size of the backup information:

```bash
❯ restic stats latest
repository b4fadbba opened (version 2, compression level auto)
scanning...
Stats in restore-size mode:
     Snapshots processed:  1
        Total File Count:  8097
              Total Size:  758.753 MiB
```


## Schedule Backups

If you wonder how often you should back up your data, just ask yourself, "_How many days work can I afford to lose_"? Whenever you make changes to files, or add new files, you need to back up your files again. It is a good practice to back up your files on a daily basis. If you are working on a critical project, you may want to back it up even more often.

For simplicity I'm using crontab to do scheduled backups every day at 12h.

```
0 12 * * * source $HOME/.zprofile; /Users/kimus/.restic/cron.sh
```

> I'm including my `~/.zprofile` because I use `zsh` and it's where I'm loading my `homebrew` configuration. Depending on your enviorment configuration you can just put the `cron.sh` here.



## Restoring from backup

Restoring a snapshot is as easy as it sounds, just use the following command to restore the contents of the `latest` snapshot to `/tmp/restore-work`:

```bash
$ restic restore latest  --target /tmp/restore-work
repository b4fadbba opened (version 2, compression level auto)
restoring <Snapshot 5eb3c41e of [/Users/kimus] at 2023-03-10 13:54:00.623059 +0000 UTC by kimus@Helders-MacBook-Pro14> to /tmp/restore-work
```

> You can use `--target=/` to restore the backup to the original path.

Just look at the files:
```bash
open /tmp/restore-work
```

![Image of my restored files](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ylbo3u39x81toy2cekxh.png)

> To toggle hidden files in the macOS Finder you can to use `Shift+Command+.` shortcut.



## Find, Dump or Restore single files

Let's say we want to find the a file `cron.sh` from the list of backup snapshots:

```bash
$ restic find cron.sh
repository b4fadbba opened (version 2, compression level auto)
Found matching entries in snapshot 3241c91f from 2023-03-12 12:00:00
/Users/kimus/.restic/cron.sh

Found matching entries in snapshot 5eb3c41e from 2023-03-10 13:54:00
/Users/kimus/.restic/cron.sh
```

Now we can check the contents of the file by using:

```bash
$ restic dump -q 5eb3c41e /Users/kimus/.restic/cron.sh
#!/usr/bin/env zsh
RESTIC_ROOT="$( cd "$(dirname "$0")" ; pwd -P )"
   (...)
done
```

To restore the file we could do:

```bash
restic restore latest --path=/Users/kimus --include=/Users/kimus/.restic/cron.sh --target=/tmp/restore-work

```

> Again, you can use `--target=/` to restore the file to the original path.


## Backup Databases

Regarding database (or any other) dump files we could use the power of restic to backup, versioning and restoring this files. Restic is capable of reading data from stdin, which can be used for saving the output of your database dump program.

Example of using `mongodump` (equivalent to `mysqldump`) to backup the dump file to the repository:

```bash
mongodump -d database --collection=Events --quiet --gzip --archive | restic backup --stdin --stdin-filename database-events.tgz
repository b4fadbba opened (version 2, compression level auto)

Files:           1 new,     0 changed,     0 unmodified
Dirs:            0 new,     0 changed,     0 unmodified
Added to the repository: 291 B (262 B stored)

processed 1 files, 610 B in 0:07
snapshot 529265dd saved
```

The backup snapshot can now be checked:

```bash
restic snapshots --path /database-events.tgz
repository b4fadbba opened (version 2, compression level auto)
ID        Time                 Host                   Tags        Paths
--------------------------------------------------------------------------------------
ad104c68  2023-03-12 15:02:47  Helders-MacBook-Pro14              /database-events.tgz
--------------------------------------------------------------------------------------
1 snapshots
```

When needed, we could also easily restore it:
```bash
restic dump latest database-events.tgz | mongorestore --gzip --archive --drop
```
