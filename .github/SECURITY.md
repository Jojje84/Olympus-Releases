# Security Policy

This repository is the public release hub for multiple Olympus applications.

## Reporting a vulnerability

Do **not** post exploit details, credentials, API keys, session cookies, private network
information, database contents or customer data in a public issue.

Use GitHub private vulnerability reporting / security advisories when available. If a
private reporting option is unavailable, open a public issue containing only a request
for a private security contact channel and no technical exploit details.

Include privately, when possible:

- affected product and version
- installation method
- affected endpoint or component
- steps to reproduce
- expected and observed behavior
- impact
- suggested mitigation, if known

## Official artifacts

Only release files published through `Jojje84/Olympus-Releases` and product-specific
container coordinates referenced by an official release should be treated as official
distribution artifacts.

Verify downloaded artifacts using the published SHA-256 checksums and matching Sigstore
bundle before installation.

## Product documentation

Product-specific verification and license documents live under `docs/<product>/`.
