# Repository Policy

`Olympus-Releases` is a public **multi-product distribution repository**, not a
source-code repository.

## Allowed content

The Git tree should contain only:

- `release-index.json`
- product channel metadata under `channels/`
- public installation, license and verification documentation under `docs/`
- security and ownership metadata
- GitHub Actions used to validate the release hub

## Not allowed in Git

Do not commit:

- application source code
- compiled binaries
- Docker images or image layers
- release archives
- package files such as DEB or RPM
- credentials, API keys, tokens, cookies or private network data

Release binaries, archives, checksums, SBOM files and signature bundles belong on a
versioned **GitHub Release** as release assets.

## Source of truth

Each product has its own authoritative source repository. For the current products:

- UniCore source of truth: `Jojje84/UniCore`
- ForgeCore source of truth: `Jojje84/ForgeCore`

This repository only receives verified release output and update metadata from those
source repositories.

## Release namespacing

GitHub Release tags in this shared repository must include the product prefix:

- `unicore-v<version>`
- `forgecore-v<version>`

This prevents collisions when two products use the same semantic version.

## Stable update feeds

Each product owns one stable feed:

- `channels/unicore/stable.json`
- `channels/forgecore/stable.json`

Prereleases may exist as GitHub Releases but must not update a stable feed.

## Main branch policy

The `main` branch should be protected by a GitHub ruleset that:

- requires pull requests
- requires the `verify` status check
- requires the branch to be up to date
- blocks force pushes
- blocks branch deletion
- uses squash merges for normal maintenance changes

Automated release publication may use narrowly scoped credentials with only the
permissions required to publish release assets and update the relevant product feed.
