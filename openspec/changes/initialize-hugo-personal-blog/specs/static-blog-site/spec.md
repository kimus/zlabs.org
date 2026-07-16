## ADDED Requirements

### Requirement: Hugo static site
The system SHALL be a Hugo static site suitable for local development and static hosting.

#### Scenario: Build static site
- **WHEN** the Hugo build command is run for the repository
- **THEN** the system generates a static website without requiring a server-side runtime, database, or CMS

### Requirement: Dark technical theme
The system SHALL provide a simple, modern, dark theme optimized for technical writing.

#### Scenario: View site in browser
- **WHEN** a visitor opens the homepage or a post page
- **THEN** the page uses a dark visual design with readable typography, accessible contrast, responsive layout, and clear navigation

### Requirement: Site identity
The system SHALL identify the site as ZLabs, Helder Rossa's personal technical notebook, and expose the configured social links.

#### Scenario: View homepage identity
- **WHEN** a visitor opens the homepage
- **THEN** the page presents the ZLabs site name, Helder Rossa's author identity, a short technical notebook tagline, and links to GitHub `https://github.com/kimus`, LinkedIn `https://www.linkedin.com/in/helderrossa`, X `https://x.com/helderrossa`, and MakerWorld `https://makerworld.com/en/@helder.rossa`

### Requirement: Core pages and navigation
The system SHALL provide homepage, posts index, tag pages, and about page navigation.

#### Scenario: Navigate site sections
- **WHEN** a visitor uses the site's main navigation
- **THEN** they can access the homepage, all posts, tags, about page, and external profile links

### Requirement: Technical post presentation
The system SHALL render technical posts with support for Markdown content, code blocks, metadata, tags, and responsive reading layout.

#### Scenario: View technical post
- **WHEN** a visitor opens a post containing code blocks and tags
- **THEN** the page displays the title, publication date, tags, formatted Markdown, readable code blocks, and navigation back to related content
