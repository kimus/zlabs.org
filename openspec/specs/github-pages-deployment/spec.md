## Purpose

Define how the ZLabs Hugo site is built and deployed to GitHub Pages at the custom domain root.

## Requirements

### Requirement: GitHub Actions deployment workflow
The system SHALL include a GitHub Actions workflow that builds the Hugo site and deploys it to GitHub Pages at the custom domain root.

#### Scenario: Push to main branch
- **WHEN** changes are pushed to the configured primary branch
- **THEN** GitHub Actions builds the Hugo site and publishes the generated static artifact to GitHub Pages at `https://zlabs.org/`

### Requirement: Source-only repository
The system SHALL keep generated Hugo build output out of version control.

#### Scenario: Build output generated locally
- **WHEN** Hugo generates the static output directory locally
- **THEN** the generated output is ignored by Git and not required to be committed for deployment

### Requirement: Reproducible CI build
The system SHALL configure the deployment workflow with the Hugo setup needed to reproduce the site build in CI.

#### Scenario: GitHub Actions runner builds site
- **WHEN** the deployment workflow runs on a clean GitHub Actions runner
- **THEN** the runner installs or configures Hugo, builds the site from repository source files, and uploads the Pages artifact

### Requirement: Manual deployment trigger
The system SHALL allow the deployment workflow to be triggered manually from GitHub Actions.

#### Scenario: Manual workflow dispatch
- **WHEN** the author manually runs the deployment workflow from GitHub Actions
- **THEN** the workflow builds and deploys the current selected branch according to the workflow configuration
