# Security Policy

This repository is the public distribution channel for UniCore.

## Supported versions

Before the first production release, no public version is considered supported.

After v1.0 is published, the latest stable release will be the supported release line unless a release notice states otherwise.

## Reporting a vulnerability

Do **not** post exploit details, credentials, UniFi API keys, session cookies, private network information, database contents, or customer data in a public issue.

Use GitHub's private vulnerability reporting / security advisory flow when it is available for this repository. If a private reporting option is not available, open a public issue containing only a request for a private security contact channel and no technical exploit details.

Please include privately, when possible:

- affected UniCore version
- installation method
- affected endpoint or component
- steps to reproduce
- expected and observed behavior
- impact
- suggested mitigation, if known

## Official artifacts

Only release files published through `Jojje84/UniCore-Releases` and container coordinates explicitly referenced by this repository should be treated as official UniCore distributions.

Verify downloaded artifacts using the published `SHA256SUMS` before installation.

## Internet-facing deployments

Use HTTPS through a trusted reverse proxy, enable UniCore authentication, keep UniCore current, and prefer a UniFi API key over controller username/password authentication.
