# modeled-information-format.github.io

The organization Pages root for **MIF (Modeled Information Format)**. This repo
exists because an organization's root domain
(`https://modeled-information-format.github.io/`) can only be served by a repo
named `<org>.github.io` — the `.github` repo cannot serve the org root itself.

## What it publishes

| Path | Source | Built from |
| --- | --- | --- |
| `/` | Root landing | the [`.github`](https://github.com/modeled-information-format/.github) repo (`index.html`) |
| `/docs/` | Ecosystem documentation | the [`doc-site`](https://github.com/modeled-information-format/doc-site) repo (Astro/Starlight, `base: "/docs"`) |

The MIF **specification** and canonical **schemas** are served separately at
[`mif-spec.dev`](https://mif-spec.dev) from the
[`MIF`](https://github.com/modeled-information-format/MIF) repo.

## How it deploys

[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) checks out the
landing and the doc-site, builds the doc-site, assembles `_site/` (landing at the
root, doc-site `dist/` under `/docs/`), and deploys it to GitHub Pages. All
actions are SHA-pinned per the org Actions policy.

Cross-repo source access is authenticated via the org `pages` GitHub App — one of
the five least-privilege apps (ADR-011) — using `actions/create-github-app-token`,
never the default `GITHUB_TOKEN`. Set the app credentials at the org level (or per
repo):

- `vars.PAGES_CLIENT_APP_ID` — the app's OAuth client id
- `secrets.PAGES_CLIENT_APP_PRIVATE_KEY` — the app's private key

The App token is used only for the cross-repo checkouts, so the installation must
grant `contents: read` on `.github` and `doc-site`. This repo is checked out with
the default token, and the Pages deployment step uses the run's ephemeral OIDC token.

The landing's authoring home stays in the `.github` repo. To redeploy after a
change to either source repo, push to `main` here, run the workflow manually, or
send a `repository_dispatch` event of type `source-updated`.

## Release process

This repository follows the shared, audit-gated attested release process of the
[`modeled-information-format`](https://github.com/modeled-information-format)
organization. The governing process — punch-list audit, epics and sub-issues, a
decision log, a release workplan issue, one PR per epic under GitHub Flow, and
the attested cutover — is documented in the org
[release runbook](https://github.com/modeled-information-format/.github/blob/main/docs/runbooks/release-runbook.md).
