## ADDED Requirements

### Requirement: Markdown-first content authoring
The system SHALL allow blog content to be authored and maintained as Markdown files in the repository.

#### Scenario: Add new post
- **WHEN** an author adds a new Markdown post with valid front matter and commits it to the repository
- **THEN** the post is included in the generated site according to its publication metadata

### Requirement: Post front matter metadata
The system SHALL define and support front matter metadata for title, date, tags, draft state, and optional source/original URL information.

#### Scenario: Render post metadata
- **WHEN** a post includes title, date, tags, and source URL fields in front matter
- **THEN** the generated post page and list pages display the relevant metadata and preserve the source URL for attribution

### Requirement: Existing DEV articles as initial content
The system SHALL seed the blog with existing public DEV Community articles from `https://dev.to/kimus` while preserving their publication history.

#### Scenario: Imported DEV article appears on blog
- **WHEN** an imported DEV article is present as a Markdown post
- **THEN** the generated blog displays it using the original title, original publish date, original tags, and a link to the DEV article

### Requirement: Content organization with tags
The system SHALL organize posts using tags so mixed topics can be browsed without requiring rigid section structure.

#### Scenario: Browse by tag
- **WHEN** a visitor opens a tag page such as `backup`, `macos`, `rust`, or `3d-printing`
- **THEN** the page lists posts assigned to that tag

### Requirement: Git-based publishing workflow documentation
The system SHALL document how to create, preview, commit, and publish content using Markdown and Git.

#### Scenario: Author follows publishing instructions
- **WHEN** the author follows the repository documentation for adding a post
- **THEN** they can create a Markdown file, preview it locally, commit it, push it, and rely on deployment automation to publish it
