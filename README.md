# Olympus Releases

**Official public release hub for Olympus applications and related projects.**

This repository is the shared public distribution endpoint for projects whose source
repositories remain separate. It contains release metadata, verification information
and product-specific stable update feeds. Application source code does not live here.

## Products

| Product | Stable channel | Public release tag prefix |
| --- | --- | --- |
| UniCore | `channels/unicore/stable.json` | `unicore-` |
| ForgeCore | `channels/forgecore/stable.json` | `forgecore-` |

The complete machine-readable product index is available in `release-index.json`.

## Release naming

Source repositories keep their normal version tags, for example:

- UniCore source: `v1.0.0`
- ForgeCore source: `v0.1.0-beta.20`

Published releases in this shared repository are namespaced so products can use the
same version numbers without collisions:

- `unicore-v1.0.0`
- `forgecore-v0.1.0-beta.20`
- `forgecore-v0.1.0`

## Stable vs prerelease

Prereleases are allowed to publish verified GitHub Release assets here, but they never
change a product's stable channel file.

Stable source tags update only that product's file under `channels/<product>/stable.json`
after the release artifacts have been published and verified.

## Source and distribution model

```text
Private source repositories
  ├── Jojje84/UniCore
  ├── Jojje84/ForgeCore
  └── future projects
            |
            v
   CI + release verification
            |
            v
   Jojje84/Olympus-Releases
      ├── GitHub Releases
      ├── release-index.json
      └── channels/<product>/stable.json
            |
            +--> Olympus Store
            +--> direct downloads
            +--> product update checks
```

## Repository policy

Release archives, binaries, checksums, SBOMs and signature bundles belong on GitHub
Releases. They must not be committed directly to this Git repository.

See `docs/REPOSITORY_POLICY.md` and `.github/SECURITY.md`.
