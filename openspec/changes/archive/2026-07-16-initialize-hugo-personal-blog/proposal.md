## Why

Helder Rossa needs a personal blog named ZLabs that acts as a durable technical notebook for software development, homelab infrastructure, developer tools, code snippets, and 3D printing experiments. A Hugo-based static site published from Markdown through Git and GitHub Pages provides a simple, low-maintenance home for new writing and existing DEV Community articles.

## What Changes

- Create a new Hugo project for the personal blog.
- Provide a simple, modern, dark theme tailored to a technical notebook / maker journal style.
- Add initial site identity named ZLabs, with Helder Rossa as the author and GitHub, LinkedIn, X, and MakerWorld links.
- Add homepage, posts listing, tag pages, and about page.
- Support Markdown-first publishing through Git commits.
- Configure GitHub Actions to build and deploy the Hugo site to GitHub Pages on repository changes.
- Import or seed existing DEV Community articles from `https://dev.to/kimus` as initial posts while preserving original titles, dates, tags, and source URLs.
- Keep generated Hugo output out of version control.

## Capabilities

### New Capabilities
- `static-blog-site`: Defines the Hugo static blog, theme, navigation, content sections, metadata, and author identity.
- `markdown-content-workflow`: Defines the Markdown and Git based authoring workflow, post metadata, imported DEV article handling, and content organization.
- `github-pages-deployment`: Defines automated build and deployment to GitHub Pages using GitHub Actions.

### Modified Capabilities

None.

## Impact

- Adds Hugo project structure, configuration, layouts/theme assets, static assets, and starter content.
- Adds OpenGraph/social metadata, syntax highlighting support, and taxonomy pages for tags/categories as needed.
- Adds GitHub Actions workflow for GitHub Pages deployment.
- Adds documentation for writing posts, importing/migrating DEV articles, and publishing through Git.
- Introduces Hugo as the static site generator dependency and GitHub Pages as the hosting target.
