---
publish: true
title: Home
tags:
  - sample
---

# Riebeckite sample: separate directories

This is the **separate directories** sample. The Vault and the site live in the same repository, but in different directories: [Rerurate514/riebeckite-e2e-directories](https://github.com/Rerurate514/riebeckite-e2e-directories).

- Content (Vault): `vault/`
- Site code: `site/` (`site/app/`, `site/riebeckite.config.ts`)
- Deployment: `site/wrangler.jsonc` and `.github/workflows/publish.yml`
- Published site: <https://directories.riebeckite.dev>

## How this layout works

`site/riebeckite.config.ts` sets `content.directory` to `"../vault"`. The build runs from `site/`, reads Markdown from the sibling `vault/` directory, and writes `site/dist/`. One GitHub Actions workflow watches both directories, so editing either the Vault or the site rebuilds and deploys the site.

## Start here

- [[welcome]] — frontmatter, tags, WikiLinks, and backlinks
- [[japanese]] — Japanese content and internal links
- [[markdown]] — Markdown links, tables, and code
- [[diagram]] — a Mermaid diagram
- [[attachments]] — images and a downloadable attachment

## Compare the other layouts

- [Integrated sample](https://integrated.riebeckite.dev)
- [Separate repositories sample](https://repositories.riebeckite.dev)

## Riebeckite documentation

- [Quick Start](https://riebeckite.dev/getting-started/quick-start)
- [Content location](https://riebeckite.dev/guides/content-repositories/basics)
