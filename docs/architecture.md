# Styles Repository - Claude Description

## Overview
`styles` is a shared style package published/consumed as `@karelhagel/styles` across multiple Angular frontends in this workspace.

## Architecture
- Package type: lightweight npm-style SCSS package.
- Primary artifact: `styles.scss`.
- Package metadata defines style entry points:
  - `main: styles.scss`
  - `style: styles.scss`
  - `sass: styles.scss`

## Usage
Consumers add the dependency in `package.json`, for example:
```json
"@karelhagel/styles": "https://github.com/karelhagel/styles.git"
```

Version/tag pinning guidance is documented in `instructions.md`.

## API Surface
There is no HTTP API in this repository.
The public interface is the exported SCSS contract from `styles.scss`:
- shared variables
- shared selectors
- shared component/layout style conventions

## Development and Release
Typical release flow from `instructions.md`:
1. Bump package version (`npm version patch|minor|major`).
2. Push tags.
3. Update dependent repos (`npm update @karelhagel/styles`) or pin explicit tag.

## Role in Workspace
This repository centralizes visual consistency and reduces duplicated CSS across micro-frontends and shell applications.
