+++
title = "My macOS from Scratch for Development"
date = "2023-02-28T19:43:04Z"
description = "Lately I needed to change computer. I've been thinking about backing up only my relevant files, like..."
draft = false
tags = ["tutorial", "backup", "macos", "productivity"]
source = "dev.to"
original_url = "https://dev.to/kimus/my-macos-from-scratch-setup-6ja"
image = "https://media2.dev.to/dynamic/image/width=1000,height=420,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fmekxz9ajhibvdexvje2m.jpg"
+++

Lately I needed to change computer. I've been thinking about backing up only my relevant files, like documents, images app settings, dotfiles, etc, instead of backing up the full OS. And when I wanted to install my macOS from scratch I would only need to execute a script to restore those files and quickly having a working computer in a couple of minutes.

Be advice that this is a working progress and I'm open for comments to improve this scripts.



## Start from Scratch

Although not needed to execute the script, you may want to start from scratch (clean your current disk), and if you didn't both a new computer, your only option is to reinstall your macOS. You can read the [official apple guide](https://support.apple.com/en-us/HT204904) on how to do it.

But in short:
- Restart machine and press `Cmd+R` to go into recovery mode
- Open Disk Utility to wipe out disk entirely (this should be an option of the initial setup)
- Quit Disk Utility, go back to setup and use the option to reinstall OS

Now that you have a clean disk you can go through all the steps of installing your macOS, creating the user account, etc.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dwbim9tu2dvtf32lffva.png)


## The Magic Steps

When you gain access to the desktop, you could now follow the next steps that will installs and configure most of the software I use on my personal macOS using [Homebrew](https://brew.sh) and [Chezmoi](https://www.chezmoi.io).


### 1. Install Homebrew

You need to start from somewhere right? So, let's ensure Homebrew installed using [skip tap clonning](https://docs.brew.sh/Installation#skip-tap-cloning-beta) option:

```bash
export HOMEBREW_INSTALL_FROM_API=1
export HOMEBREW_NO_ANALYTICS=1
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

This also will install Command Line Tools for Xcode, and all the tools for the next steps.


### 2. Clone the repository to your local drive

Of course I will use my own repository, but you could clone it and customise it.

```bash
git clone https://github.com/kimus/macos-from-scratch
cd macos-from-scratch
```


### 3. Run bootstrap.sh script
From here it's expected to be all automatically.

```bash
./bootstrap.sh
```

By default it uses your current user name (environment variable USER) to get your dotfiles from GitHub. You can use my own like this:

```bash
GITHUB_USERNAME=kimus ./bootstrap.sh
```

The script will ask you for your [Bitwarden](https://bitwarden.com/) account. This is where I store my secrets (i.e. SSH keys).

In the future I'm planning to restore my working folder and other files (pictures, documents, etc) from a backup made with [restic](https://restic.net/). I have a separated post about [restic backups](https://dev.to/kimus/how-easy-and-securely-is-to-backup-your-computer-2g7d).

And that's it, at this time you should have a working macOS with your favourite applications and settings.

Here is how my terminal looks like:
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0gxbeim5ma0ehqlbmee4.png)


## Defaults

This script will setup a bunch of tools, applications and configurations.


### Tools and Applications

Applications (installed with Homebrew Cask):

  - [Docker](https://www.docker.com/)
  - [Google Chrome](https://www.google.com/chrome/)
  - [Google Chrome Dev](https://www.google.com/chrome/dev/)
  - [Slack](https://slack.com/)
  - [Visual Studio Code](https://code.visualstudio.com/)
  - [Fork](https://fork.dev/)
  - [iTerm2](https://iterm2.com/)
  - [Oh My Zsh](https://ohmyz.sh)
  - [Obsidian](https://obsidian.md/)

Check `Brewfile` for the full list of tools and applications.


### Visual Studio Code Extensions

Check `vscodefile` for the full list of Visual Studio Code extensions.


### MacOS System Preferences

There are a few other preferences and settings added on for various apps and services. Check `osxfile` for a list of macos specific system preferences.


### dotfiles

Finally, the [dotfiles](https://github.com/kimus/dotfiles) are also installed by `Chezmoi` into the current user's home directory. This step needs the `Bitwarden` account to restore the SSH keys.
