# Installing UniCore

No public production build has been published yet.

When the first release is available, install UniCore only from the **Releases** section of this repository or from a downstream store that references the same official release channel.

## Supported release targets

The release pipeline is designed to publish Linux builds for:

- amd64
- arm64
- armv7

Docker/container distribution will use the same UniCore version as the binary release.

## Binary installation

For a future release, download the archive matching the target architecture and its published `SHA256SUMS` file.

Verify the download before installation. See [VERIFY.md](VERIFY.md).

Extract the archive and follow the release-specific installation notes. The production service is intended to run as a dedicated non-root `unicore` user when installed directly on Linux.

## Docker

Official container coordinates will be documented here when the public registry channel is enabled.

Do not rely on third-party images that are not referenced by this repository.

## Configuration

UniCore requires access to a UniFi Network controller. An official UniFi Network Integration API key is the preferred authentication method.

Never put real controller credentials or API keys into public issues, screenshots, or support logs.

## Updates

UniCore will use the machine-readable `channels/unicore/stable.json` feed in this repository for stable update discovery.

The update feed remains in `pre-release` state until the first production release is published.
