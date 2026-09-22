# Olympus Releases

**Official public release hub for Jojje84 applications distributed through Olympus.**

This repository is the shared public release and update channel for products whose
source code is maintained in separate private repositories.

## Products

- **UniCore** — UniFi monitoring dashboard
- **ForgeCore** — self-hosted GitHub Actions runner platform for Umbrel

Additional products can be added without creating another public release repository.

## Repository model

```text
Private source repositories
├── Jojje84/UniCore
├── Jojje84/ForgeCore
└── future products
        |
        v
verified release workflows
        |
        v
Jojje84/Olympus-Releases
├── release-index.json
├── channels/
│   ├── unicore/stable.json
│   └── forgecore/stable.json
└── GitHub Releases
    ├── unicore-v...
    └── forgecore-v...
        |
        v
olympus-community-app-store
```

The private source repository for each product remains its source of truth.
`olympus-community-app-store` is a downstream app-store/distribution layer.

## Release naming

Public GitHub Release tags are namespaced by product so different applications can
use the same semantic version without collisions.

Examples:

```text
unicore-v1.0.0
forgecore-v0.1.0-beta.20
forgecore-v0.1.0
```

## Stable channels

`release-index.json` is the hub index.

Each product has its own machine-readable stable feed:

```text
channels/unicore/stable.json
channels/forgecore/stable.json
```

Prereleases can be published and fully verified without changing a stable feed.

## UniCore compatibility

The root `release-channel.json` is temporarily retained as the legacy UniCore
stable feed while UniCore moves to `channels/unicore/stable.json`.

UniCore-specific installation, verification and binary-license documents currently
remain under `docs/` for backwards compatibility.

## Security

Do not publish credentials, access tokens, private source code, customer data or
machine secrets in this repository.

Only verified release artifacts should be attached to GitHub Releases.
