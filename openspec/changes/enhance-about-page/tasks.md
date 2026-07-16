## 1. Social Metadata

- [x] 1.1 Add DEV and email contact URLs to Hugo social/contact configuration.
- [x] 1.2 Add GitHub avatar and location metadata for Helder Rossa.

## 2. Reusable Social Icons

- [x] 2.1 Create reusable inline SVG icon rendering for GitHub, LinkedIn, X, DEV, MakerWorld, and email.
- [x] 2.2 Create a reusable social/contact links partial with icon-only and icon-with-label variants.
- [x] 2.3 Ensure icon-only links have accessible labels.

## 3. TailwindCSS Setup

- [x] 3.1 Add a TailwindCSS input stylesheet for Hugo asset processing.
- [x] 3.2 Update the head partial to process CSS with Hugo's `css.TailwindCSS` function and production minification/fingerprinting.
- [x] 3.3 Verify the local and GitHub Actions Hugo versions support `css.TailwindCSS`.

## 4. Template Conversion

- [x] 4.1 Convert base, header, footer, homepage, list, single post, taxonomy, and post-card templates to TailwindCSS utility classes.
- [x] 4.2 Replace or remove custom CSS classes that are superseded by Tailwind utilities.
- [x] 4.3 Preserve the existing simple, modern, dark visual identity after conversion.

## 5. Homepage and Footer

- [x] 5.1 Replace homepage text social links with icon-only social/contact buttons.
- [x] 5.2 Replace footer text social links with icon-only social/contact buttons.
- [x] 5.3 Verify homepage and footer include GitHub, LinkedIn, X, DEV, MakerWorld, and email links.

## 6. About Page

- [x] 6.1 Add an About-specific layout or layout branch for an identity card.
- [x] 6.2 Render the GitHub profile avatar, Helder Rossa name, role summary, and Sesimbra, Portugal location on the About page.
- [x] 6.3 Render icon-with-label social/contact links on the About page.
- [x] 6.4 Rewrite About page copy to blend GitHub profile README/profile bio themes with the ZLabs technical notebook tone.

## 7. Styling and Validation

- [x] 7.1 Add responsive Tailwind styling for avatar, identity card, social icons, and icon-with-label links.
- [x] 7.2 Run Hugo build and fix any template, Tailwind, or styling issues that block generation.
- [x] 7.3 Verify generated homepage, footer, and About page social/contact links and accessibility labels.
- [x] 7.4 Verify generated homepage, posts list, post page, tag pages, footer, and About page preserve the intended dark visual design.
- [x] 7.5 Validate the OpenSpec change.
