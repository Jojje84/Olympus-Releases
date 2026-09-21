# Repository Policy

`UniCore-Releases` is a public **distribution repository**, not a source-code repository.

## Allowed content

The Git tree should contain only:

- release-channel metadata
- public installation and verification documentation
- security and ownership metadata
- GitHub Actions used to validate the distribution repository

## Not allowed in Git

Do not commit:

- UniCore application source code
- compiled binaries
- Docker images or image layers
- release archives
- package files such as DEB or RPM
- credentials, API keys, tokens, cookies or private network data

Release binaries, checksums and SBOM files belong on a versioned **GitHub Release** as release assets.

## Release source of truth

The private `Jojje84/UniCore` repository is the development source of truth.

Only verified release output produced by that repository's release pipeline should be published here.

## Stable update feed

`release-channel.json` is the stable machine-readable update feed used by UniCore and downstream distribution systems.

A release must not be added to the stable feed until its build, tests, checksums and publication have completed successfully.

## Main branch policy

The `main` branch should be protected by a GitHub ruleset that:

- requires pull requests
- requires the `verify` status check
- requires the branch to be up to date
- blocks force pushes
- blocks branch deletion
- uses squash merges for normal maintenance changes

Automated release publication may use a narrowly scoped credential or GitHub App with only the permissions required to publish release assets and update the release feed.
