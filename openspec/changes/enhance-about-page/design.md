## Context

ZLabs currently has a minimal About page with a short Helder Rossa bio and text links. The site already has social metadata for GitHub, LinkedIn, X, and MakerWorld, and the user wants to expand the About page using GitHub profile material, add the GitHub profile photo, add DEV and email links, and introduce icon-based social/contact links. The user also wants the site styling migrated to TailwindCSS using Hugo's built-in `css.TailwindCSS` function.

GitHub profile context discovered during exploration:
- Avatar: `https://avatars.githubusercontent.com/u/188404?v=4`
- Profile bio: "I believe that technology has important effects on business and affects the culture, efficiency and relationships."
- Profile README themes: technology leadership, imagining/developing/delivering technology solutions, business profitability/productivity, adaptability.
- Location: Sesimbra, Portugal.

## Goals / Non-Goals

**Goals:**

- Make the About page richer, more personal, and more credible.
- Preserve the ZLabs technical notebook / maker journal tone.
- Present Helder Rossa as technology leader, developer, homelab tinkerer, and maker.
- Use the GitHub avatar as the profile photo.
- Add social/contact links for GitHub, LinkedIn, X, DEV, MakerWorld, and email.
- Render social links as icon-only buttons on homepage/footer.
- Render social links as icon + text links on the About page.
- Keep icon links accessible with labels.
- Add TailwindCSS through Hugo's built-in asset pipeline.
- Convert existing layouts/pages and new components to Tailwind utility classes.
- Preserve the existing simple, modern, dark visual identity.
- Avoid external JavaScript or icon font dependencies.

**Non-Goals:**

- No automated synchronization with the GitHub profile README.
- No contact form or server-side email handling.
- No analytics or tracking.
- No major homepage redesign beyond social icon presentation and Tailwind class conversion.
- No dependency on a third-party icon package.
- No separate JavaScript build framework.

## Decisions

### Use Hugo TailwindCSS for styling

Add a Tailwind input stylesheet and process it through Hugo's built-in `css.TailwindCSS` function from the asset pipeline.

Rationale:
- Keeps styling integrated with Hugo instead of introducing a separate frontend framework.
- Allows templates to use Tailwind utility classes directly.
- Reduces the amount of bespoke CSS needed for layout, typography, cards, avatar, and social links.
- Makes future visual iteration easier once the utility-class pattern is established.

Implementation direction:
- Use an input stylesheet such as `assets/css/main.css` or `assets/css/input.css` containing Tailwind imports.
- Update the head partial to pipe the stylesheet through `css.TailwindCSS`, with minification/fingerprinting in production.
- Convert templates to Tailwind classes rather than preserving the current custom class system.
- Keep minimal custom CSS only if needed for Hugo/Tailwind integration or hard-to-express details.

Alternatives considered:
- Keep custom CSS: lowest risk but does not satisfy the requested TailwindCSS migration.
- Add Node/PostCSS build tooling manually: more flexible but unnecessary if Hugo's built-in function is sufficient.

### Use inline SVG icons through reusable Hugo partials

Implement social/contact icons as inline SVGs rendered through reusable partials rather than loading Font Awesome, icon fonts, or external scripts.

Rationale:
- Keeps the static site lightweight and dependency-free.
- Works without JavaScript.
- Allows accessible labels and consistent styling.
- Avoids third-party asset loading for basic UI chrome.

Alternatives considered:
- Icon font/library: faster to source icons but adds external dependency and unnecessary weight.
- Text-only links: accessible and simple but less polished than requested.

### Use one social metadata source with display variants

Store social/contact URLs in Hugo site params and render them through a shared `social-links` partial with variants for icon-only and icon-with-label display.

Rationale:
- Avoids duplicating URLs across homepage, footer, and About page.
- Makes future social link changes localized.
- Supports distinct presentation for compact and detailed contexts.

Expected links:
- GitHub: `https://github.com/kimus`
- LinkedIn: `https://www.linkedin.com/in/helderrossa`
- X: `https://x.com/helderrossa`
- DEV: `https://dev.to/kimus`
- MakerWorld: `https://makerworld.com/en/@helder.rossa`
- Email: `mailto:helder@rossa.eu.org`

### Add About-specific presentation

Use an About-specific layout or layout branch to render an identity card with avatar, short role summary, location, and social/contact links before the page body.

Rationale:
- The generic single page template is good for posts but too plain for About identity content.
- An About-specific layout allows stronger visual hierarchy while keeping Markdown content maintainable.

### Blend, do not paste, GitHub profile copy

Use the ideas from the GitHub profile README/bio but adapt them to ZLabs' tone.

Rationale:
- The GitHub README is more professional/corporate than the blog tone.
- Blending it gives the About page more substance while keeping the personal technical notebook identity.

Suggested copy direction:
- Introduce Helder Rossa as a technology leader, developer, homelab tinkerer, and maker based in Sesimbra, Portugal.
- Include belief that technology affects business, culture, efficiency, and relationships.
- Mention professional focus on imagining, developing, and delivering technology solutions.
- Connect ZLabs to notes, experiments, build logs, code snippets, infrastructure work, and 3D printing models.

## Risks / Trade-offs

- GitHub avatar URL could change or be unavailable → Use the GitHub avatar initially as requested; local copy can be added later if stability becomes important.
- Icon-only links can be inaccessible if unlabeled → Require `aria-label` or visually hidden text for every icon-only link.
- About page could become too corporate → Blend profile README language with personal maker/dev tone.
- More social links can clutter the UI → Use icon-only compact links outside About and icon + text only where context allows.
- Hugo TailwindCSS support is version-sensitive → Pin or verify a Hugo version in GitHub Actions that supports `css.TailwindCSS` and validate locally before pushing.
- Tailwind utility classes can make templates verbose → Prefer readable grouping and reusable partials for repeated structures such as social links.
- Full styling migration may introduce visual regressions → Validate homepage, posts list, post page, tag pages, footer, and About page after conversion.
