# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

Community theme catalog for the Continuum media streaming server. This repo is data-only — no build system, no tests, no code. It serves as the remote source that the Continuum frontend fetches to list and install community themes.

## Structure

- **`catalog.json`** — Theme index fetched by the Continuum client. Contains metadata for each theme (id, name, description, author, preview colors, tags, download URL, version). The top-level `version` field is the catalog schema version; `updatedAt` should be bumped on every change.
- **`themes/`** — Individual theme files (`<id>.json`). Each defines CSS custom property overrides applied on top of a `baseTheme` in the Continuum UI.

## Theme File Format

Each theme JSON has:
- `version` (schema version, currently `1`)
- `name`, `description`, `author`
- `baseTheme` — the built-in Continuum theme to extend (e.g. `"midnight-cinema"`)
- `vars` — map of CSS custom property names to hex color values (background, foreground, card, primary, accent, sidebar variants, surface variants, ambient, etc.)
- `customCss` — optional raw CSS string for overrides beyond color variables
- `createdAt` — ISO 8601 timestamp

## Adding a Theme

1. Create `themes/<id>.json` following the format above. The `id` must be a kebab-case slug.
2. Add a corresponding entry to `catalog.json`'s `themes` array. The `downloadUrl` must point to the raw GitHub URL for the theme file on `main`.
3. Update `catalog.json`'s `updatedAt` timestamp.

## Conventions

- Theme IDs are kebab-case and must match the filename (e.g. id `"nord-aurora"` → `themes/nord-aurora.json`).
- All colors in `vars` are hex values.
- `previewAccent` and `previewBg` in the catalog entry are used for thumbnail rendering in the theme browser — pick representative colors from the theme's `vars`.
