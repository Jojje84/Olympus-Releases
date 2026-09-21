# Verifying UniCore downloads

Official UniCore releases publish SHA-256 checksums and Sigstore verification bundles alongside release artifacts.

Verify both the checksum and the Sigstore bundle before installation.

## SHA-256 verification

Download the release archive and `SHA256SUMS`, then run on Linux:

```bash
sha256sum --check SHA256SUMS
```

A valid downloaded file reports `OK`.

On macOS, verify one file with:

```bash
shasum -a 256 unicore_<version>_linux_amd64.tar.gz
```

Compare the output with the matching entry in `SHA256SUMS`.

## Sigstore verification

Install Cosign 3.x, then download the artifact and its matching `.sigstore.json` bundle.

For example, to verify the arm64 archive for version `1.0.0`:

```bash
cosign verify-blob unicore_1.0.0_linux_arm64.tar.gz \
  --bundle unicore_1.0.0_linux_arm64.tar.gz.sigstore.json \
  --certificate-identity "https://github.com/Jojje84/UniCore/.github/workflows/release.yml@refs/tags/v1.0.0" \
  --certificate-oidc-issuer "https://token.actions.githubusercontent.com"
```

Use the matching release tag in the certificate identity when verifying another version.

The same process applies to `SHA256SUMS` and the CycloneDX SBOM because each published payload receives its own Sigstore bundle.

## Container verification

Official multi-architecture container images are signed by immutable digest. Resolve the image digest first, then verify it with Cosign using the same GitHub Actions identity and OIDC issuer.

## Supply-chain metadata

Each release is designed to contain:

- Linux archives for amd64, arm64 and armv7
- `SHA256SUMS`
- a CycloneDX SBOM
- one `.sigstore.json` bundle per published release payload
- release metadata linking the version to its source revision

Do not install an artifact when its checksum or Sigstore verification fails.
