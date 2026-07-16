## MODIFIED Requirements

### Requirement: Site identity
The system SHALL identify the site as ZLabs, Helder Rossa's personal technical notebook, expose the configured social/contact links, present a richer About identity experience, and use TailwindCSS for page/component styling.

#### Scenario: View homepage identity
- **WHEN** a visitor opens the homepage
- **THEN** the page presents the ZLabs site name, Helder Rossa's author identity, a short technical notebook tagline, and icon-only links to GitHub `https://github.com/kimus`, LinkedIn `https://www.linkedin.com/in/helderrossa`, X `https://x.com/helderrossa`, DEV `https://dev.to/kimus`, MakerWorld `https://makerworld.com/en/@helder.rossa`, and email `mailto:helder@rossa.eu.org`

#### Scenario: View About identity card
- **WHEN** a visitor opens the About page
- **THEN** the page presents Helder Rossa's GitHub profile photo, role summary, location, richer biography, and icon-with-label links to GitHub, LinkedIn, X, DEV, MakerWorld, and email

#### Scenario: Use social icon link accessibility
- **WHEN** a visitor navigates social/contact links using assistive technology
- **THEN** every icon-only social/contact link has an accessible label identifying its destination

### Requirement: Core pages and navigation
The system SHALL provide homepage, posts index, tag pages, and about page navigation styled through TailwindCSS utility classes.

#### Scenario: Navigate site sections
- **WHEN** a visitor uses the site's main navigation
- **THEN** they can access the homepage, all posts, tags, about page, and external profile links

#### Scenario: Build Tailwind-styled pages
- **WHEN** the Hugo build command runs
- **THEN** Hugo processes the TailwindCSS input through `css.TailwindCSS` and generates styled homepage, posts, tags, post detail, footer, and About pages
