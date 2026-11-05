# Riebeckite E2E: separate directories

A public, continuously deployed Riebeckite sample where the Vault and the site live in one repository but in separate directories.

- **Published site:** <https://directories.riebeckite.dev>
- **Riebeckite documentation:** <https://riebeckite.dev>
- **Other samples:** [integrated](https://integrated.riebeckite.dev) · [separate repositories](https://repositories.riebeckite.dev)

## Purpose

This repository is for teams that want one checkout and one review process, but a clear boundary between writing and site engineering. The Vault can be opened directly in Obsidian; the site only reads it.

The important setting is in `site/riebeckite.config.ts`:

```ts
content: {
  directory: "../vault",
}
```

The build runs from `site/`, resolves the sibling `vault/`, and writes `site/dist/`.

## Directory structure

```text
.
├── vault/                     Content, Obsidian-compatible
│   ├── index.md
│   ├── notes/
│   └── assets/
├── site/                      Riebeckite site
│   ├── app/
│   ├── public/
│   ├── riebeckite.config.ts
│   ├── wrangler.jsonc
│   └── package.json
└── .github/workflows/
    └── publish.yml            Build and deploy on changes to site/ or vault/
```

## Requirements

- Node.js 22 or newer
- npm
- A Cloudflare account with a `riebeckite.dev` zone

## Setup

```sh
git clone https://github.com/Rerurate514/riebeckite-e2e-directories.git
cd riebeckite-e2e-directories/site
npm ci
```

Riebeckite is installed from npm as `@riebeckite/*` packages, not linked from a local checkout.

## Local development

Run from `site/`:

```sh
npm exec riebeckite check
npm exec riebeckite dev
```

Edit `../vault/index.md` while the dev server is running. The page reloads because the content directory is watched through the configured path.

Useful commands:

```sh
npm exec riebeckite doctor
npm run build
npm exec riebeckite inspect
```

## Build

```sh
cd site
npm run build
```

The output is `site/dist/`. `vault/` is never modified by the build.

## Deploy

The Worker is named `riebeckite-e2e-directories` and is attached to `directories.riebeckite.dev` by `site/wrangler.jsonc`.

```sh
cd site
npx wrangler login
npx wrangler deploy
```

The first deploy creates the Worker and the custom domain. Cloudflare manages the DNS record for the custom domain.

## GitHub Actions

`.github/workflows/publish.yml` runs when `site/**`, `vault/**`, or the workflow itself changes on `main`. All run steps use `site/` as the working directory.

Required repository credentials:

| Name | Kind | Purpose |
| --- | --- | --- |
| `CLOUDFLARE_API_TOKEN` | Secret | Workers Scripts:Edit for the account |
| `CLOUDFLARE_ACCOUNT_ID` | Variable | Cloudflare account ID |

## Content in this sample

`vault/index.md` explains the layout. `vault/notes/` demonstrates frontmatter, tags, WikiLinks, backlinks, Markdown links, tables, code, Mermaid, and images. The source image is in `vault/assets/`; the downloadable text attachment is in `site/public/assets/`.

## Continuous E2E

This repository tracks the latest stable `@riebeckite/*` release, so it tests the package as an external consumer rather than through a workspace link.

To validate a release candidate, create a branch, pin the candidate version in `site/package.json`, run `npm install`, `npm exec -- riebeckite check`, and `npm exec -- riebeckite build` from `site/`, then push the branch and run the publish workflow with `workflow_dispatch`. Keep the version in the commit message. Do not merge the candidate branch until the deploy succeeds; `main` remains on the stable release.

## Related documentation

- [Quick Start](https://riebeckite.dev/getting-started/quick-start)
- [Content location](https://riebeckite.dev/getting-started/content-location)
- [Separate directories setup](https://riebeckite.dev/getting-started/separate-directories-setup)
- [Cloudflare Workers deployment](https://riebeckite.dev/guides/deployment/cloudflare-workers)
- [GitHub Actions deployment](https://riebeckite.dev/guides/deployment/github-actions)

## License

Apache License 2.0. See [LICENSE](LICENSE).
