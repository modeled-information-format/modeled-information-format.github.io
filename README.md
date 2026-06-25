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

The landing's authoring home stays in the `.github` repo. To redeploy after a
change to either source repo, push to `main` here, run the workflow manually, or
send a `repository_dispatch` event of type `source-updated`.
