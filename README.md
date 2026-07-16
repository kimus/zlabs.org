# ZLabs

Personal technical notebook by Helder Rossa for software development, homelab infrastructure, developer tools, code snippets, and 3D printing experiments.

Built with [Hugo](https://gohugo.io/), authored in Markdown, versioned with Git, and deployed with GitHub Actions to GitHub Pages at the custom domain root (`https://zlabs.org/`).

## Links

- GitHub: <https://github.com/kimus>
- LinkedIn: <https://www.linkedin.com/in/helderrossa>
- X: <https://x.com/helderrossa>
- MakerWorld: <https://makerworld.com/en/@helder.rossa>

## Local preview

Install Hugo Extended, then run:

```sh
hugo server --buildDrafts
```

Open the local URL printed by Hugo, usually <http://localhost:1313/>.

## Create a new post

```sh
hugo new posts/my-new-post.md
```

Edit the generated Markdown file and update the front matter:

```toml
title = "My New Post"
date = 2026-01-10T12:00:00Z
description = "Short summary for listings and metadata."
draft = false
tags = ["homelab", "docker"]
source = ""
original_url = ""
```

For imported or cross-posted articles, set `source` and `original_url`:

```toml
source = "dev.to"
original_url = "https://dev.to/kimus/example"
```

## Publish

The publishing workflow is Git-based:

```sh
git add .
git commit -m "Add new post"
git push origin main
```

GitHub Actions builds the Hugo site and deploys it to GitHub Pages. The `static/CNAME` file configures the custom domain `zlabs.org`; configure the same custom domain in the repository's GitHub Pages settings and point DNS at GitHub Pages. Generated output in `public/` is ignored and should not be committed.

## Build locally

```sh
hugo --gc --minify
```
