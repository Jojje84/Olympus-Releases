# UniCore Releases

**Official public downloads and release information for UniCore.**

[Live demo](https://jojje84.github.io/UniCore/) · [Security](.github/SECURITY.md) · [Installation](docs/INSTALL.md) · [Verify downloads](docs/VERIFY.md)

UniCore is a lightweight, local-first UniFi monitoring dashboard written in Go.

This repository is the **public distribution channel** for UniCore. The application source code is maintained separately in a private development repository.

## Current release status

No public UniCore release has been published yet.

The first production release will be published here after the current release candidate has completed real-controller, browser, migration, Docker and target-device validation.

When releases begin, this repository will provide:

- Linux binaries for amd64, arm64 and armv7
- SHA-256 checksums
- CycloneDX SBOM files
- versioned release notes
- Docker/container distribution information
- a machine-readable release channel used by UniCore and downstream app stores

## Release files

A release is expected to contain artifacts similar to:

```text
unicore_<version>_linux_amd64.tar.gz
unicore_<version>_linux_arm64.tar.gz
unicore_<version>_linux_armv7.tar.gz
SHA256SUMS
unicore_<version>_sbom.cdx.json
```

Only files attached to releases in this repository should be treated as official public UniCore downloads.

## Release channel

`release-channel.json` is the stable machine-readable update feed.

Before the first public release its `latest` value is `null`. Once releases begin, the private UniCore build pipeline will update this file automatically after a release has passed verification and been published successfully.

## Security

Do not publish credentials, UniFi API keys, session cookies, customer data or private network information in public issues.

See [the security policy](.github/SECURITY.md) for reporting guidance.

## Source and distribution model

UniCore uses a private-source/public-binary distribution model:

```text
Private UniCore source
        |
        v
CI + security verification
        |
        v
Signed/checksummed release artifacts
        |
        v
UniCore-Releases
        |
        +--> Olympus Store
        +--> direct downloads
        +--> UniCore update checks
```

This repository is intentionally kept small. It is a distribution endpoint, not a second development repository.
