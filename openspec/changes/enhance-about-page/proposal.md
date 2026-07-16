## Why

The current About page is too minimal for ZLabs and does not fully express Helder Rossa's professional background, maker identity, GitHub profile presence, or complete set of social/contact links. Enhancing it with a profile photo, richer bio copy, and icon-based contact links will make the site feel more personal, credible, and polished.

## What Changes

- Enhance the About page with a profile/identity card for Helder Rossa.
- Use the GitHub profile avatar as the About page photo source.
- Blend the GitHub profile README/profile bio into the About page copy while preserving the ZLabs technical notebook tone.
- Add DEV Community and email contact links alongside GitHub, LinkedIn, X, and MakerWorld.
- Add reusable social/contact link rendering with icons.
- Add Hugo TailwindCSS processing using the built-in `css.TailwindCSS` function.
- Convert existing page templates and new About/social components from custom CSS classes to TailwindCSS utility classes.
- Use icon-only social links on homepage/footer and icon-with-label links on the About page.
- Preserve accessible labels for icon links.

## Capabilities

### New Capabilities

None.

### Modified Capabilities
- `static-blog-site`: Enhance site identity presentation, About page content, avatar handling, social/contact link rendering, and migrate site styling to TailwindCSS.

## Impact

- Updates Hugo configuration parameters for additional social/contact metadata, including DEV and email.
- Updates About page content and likely adds About-specific layout/styling.
- Adds or updates reusable Hugo partials for social links and inline SVG icons.
- Updates homepage/footer rendering to use icon-only social links.
- Adds a TailwindCSS input stylesheet and updates Hugo asset pipeline usage.
- Converts layout templates to TailwindCSS utility classes while preserving the current dark visual identity.
- Reduces or removes custom CSS previously used for layout, avatar, identity card, and icon link presentation.
- May require GitHub Actions to use a Hugo version that supports `css.TailwindCSS`.
- No changes to content import workflow or generated output versioning.
