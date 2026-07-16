## Context

This repository will become ZLabs, Helder Rossa's personal blog: a static, Markdown-authored technical notebook for development, homelab, code snippets, and 3D printing content. The site should be easy to maintain with Git, built with Hugo, and deployed to GitHub Pages automatically through GitHub Actions.

The initial site will not start empty. Existing DEV Community articles from `https://dev.to/kimus` should seed the blog so the site launches with real content and validates post layouts, tags, dates, and metadata.

## Goals / Non-Goals

**Goals:**

- Use Hugo as the static site generator.
- Keep content authoring Markdown-first and Git-based.
- Provide a simple, modern, dark visual theme suitable for technical writing.
- Use ZLabs as the site name while including Helder Rossa's author identity, GitHub profile, LinkedIn profile, X account, and MakerWorld 3D printing profile.
- Support blog posts, tags, post lists, an about page, and code-focused content.
- Preserve DEV article source information during initial content migration.
- Deploy automatically to GitHub Pages on changes to the main branch.
- Avoid committing generated build output.

**Non-Goals:**

- No CMS, database, comments system, or server-side runtime.
- No complex JavaScript application framework.
- No automated two-way synchronization with DEV Community.
- No requirement to build a corporate portfolio or resume site in the initial version.
- No implementation of analytics unless added in a later change.

## Decisions

### Use Hugo with a small custom theme

The site will use Hugo with project-local layouts/assets rather than depending heavily on a third-party theme.

Rationale:
- The desired design is intentionally simple and can be implemented with a small amount of layout/CSS.
- A custom theme avoids third-party theme assumptions, lock-in, and excess features.
- Hugo is fast, well-suited for Markdown, and supported by GitHub Actions deployment flows.

Alternatives considered:
- Third-party Hugo theme: faster initial setup, but less control and more inherited structure.
- Jekyll: native GitHub Pages support, but Hugo better matches the user's preference.
- Astro/Next.js: more flexible, but unnecessary runtime/tooling complexity for a static Markdown blog.

### Blog-first information architecture

The first version will use a blog-first structure with a homepage, posts index, tag pages, and about page.

Rationale:
- The main use case is publishing notes and articles.
- Tags provide enough organization for mixed topics without over-structuring early.
- Dedicated sections such as `projects` or `snippets` can be added later if content volume justifies them.

Initial topic organization should support:
- software development
- homelab and infrastructure
- developer tools and productivity
- code snippets
- 3D printing experiments and build logs

### Preserve DEV article metadata

Imported DEV posts will preserve original title, publish date, tags, and canonical/source URL in front matter.

Rationale:
- Existing articles provide useful seed content.
- Preserving original source attribution avoids confusion about publication history.
- Keeping metadata in front matter allows templates to show an "Originally published on DEV" link.

### GitHub Actions owns deployment

The repository will use GitHub Actions to build the Hugo site and publish the generated artifact to GitHub Pages.

Rationale:
- The repository remains source-only; generated `public/` output is not committed.
- Every change can be deployed consistently through CI.
- The workflow matches the desired Git-based publishing model.

### Minimal JavaScript and strong readability

The theme should prioritize readable typography, accessible contrast, mobile layout, syntax highlighting, and lightweight pages.

Rationale:
- Technical notes benefit from excellent text and code readability.
- A static site with little or no JavaScript is easier to maintain and faster to load.

## Risks / Trade-offs

- DEV article content may contain embeds, images, or DEV-specific markup → Review imported posts and adjust Markdown/assets manually where needed.
- A custom theme takes more initial effort than installing a prebuilt theme → Keep the first design intentionally small and avoid decorative features.
- GitHub Pages deployment settings can differ between repositories and account/organization sites → Document the expected Pages source and validate the workflow after setup.
- Imported articles may create duplicate content with DEV → Preserve `original_url`/source metadata and decide later whether the personal blog or DEV is canonical going forward.
- Over-structuring categories too early may make publishing slower → Start with posts and tags, then add sections only when content patterns emerge.
