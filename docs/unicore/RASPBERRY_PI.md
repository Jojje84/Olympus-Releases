# Raspberry Pi installation

UniCore v1.0 publishes separate Linux binaries for 64-bit ARM and 32-bit ARMv7. Choose the package from the operating-system architecture, not only from the Raspberry Pi model.

## 1. Check the Raspberry Pi architecture

Run:

```bash
uname -m
```

Use this package:

| `uname -m` | UniCore package | Notes |
| --- | --- | --- |
| `aarch64` | `unicore_<version>_linux_arm64.tar.gz` | Recommended for 64-bit Raspberry Pi OS |
| `armv7l` | `unicore_<version>_linux_armv7.tar.gz` | For 32-bit Raspberry Pi OS |
| `x86_64` | `unicore_<version>_linux_amd64.tar.gz` | Intel/AMD Linux, not Raspberry Pi |
| `armv6l` | Not supported | Use a newer Pi/OS architecture |

For a modern Raspberry Pi running 64-bit Raspberry Pi OS, choose **arm64**.

## 2. Download and verify the release

Download the matching archive plus `SHA256SUMS` and its Sigstore verification bundle from the official Olympus Releases hub.

Verify the checksum before installation:

```bash
sha256sum -c SHA256SUMS --ignore-missing
```

The release page also provides Sigstore verification instructions. Use both checksum and Sigstore verification for an official installation.

## 3. Extract the package

Example for ARM64:

```bash
tar -xzf unicore_<version>_linux_arm64.tar.gz
cd unicore_<version>_linux_arm64
```

For 32-bit Raspberry Pi OS, replace `arm64` with `armv7`.

The archive contains:

- `unicore`
- `README.md`
- `LICENSE.md`
- `CHANGELOG.md`
- `RASPBERRY_PI.md`
- `config.example.env`
- `unicore.service`

## 4. Create the service account and directories

```bash
sudo useradd --system --home /var/lib/unicore --shell /usr/sbin/nologin unicore 2>/dev/null || true
sudo install -d -o unicore -g unicore /opt/unicore /var/lib/unicore
sudo install -m 0755 unicore /opt/unicore/unicore
sudo install -m 0640 config.example.env /etc/unicore.env
sudo chown root:unicore /etc/unicore.env
sudo install -m 0644 unicore.service /etc/systemd/system/unicore.service
```

## 5. Configure UniCore

Edit:

```bash
sudo nano /etc/unicore.env
```

The recommended UniFi authentication method is an API key:

```env
UNICORE_UNIFI_URL=https://192.168.1.1
UNICORE_UNIFI_API_KEY=replace-me
UNICORE_UNIFI_SITE=default

UNICORE_AUTH_USERNAME=admin
UNICORE_AUTH_PASSWORD=replace-with-a-strong-password
UNICORE_AUTH_SECRET=replace-with-at-least-32-random-characters
```

If the controller uses a trusted self-signed certificate, `UNICORE_UNIFI_INSECURE_SKIP_VERIFY=true` can be used intentionally. Do not enable it for an untrusted controller.

## 6. Enable and start UniCore

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now unicore
sudo systemctl status unicore
```

View logs:

```bash
journalctl -u unicore -f
```

Open the dashboard from another device on the same network:

```text
http://<raspberry-pi-ip>:8080
```

To find the Pi address:

```bash
hostname -I
```

## 7. Check health

On the Raspberry Pi:

```bash
curl -fsS http://127.0.0.1:8080/health
```

A successful response confirms that the local UniCore HTTP service is running.

## 8. Upgrade

Before upgrading, download a database backup from UniCore or preserve `/var/lib/unicore/unicore.db`.

Then stop the service, replace only the binary, and restart:

```bash
sudo systemctl stop unicore
sudo install -m 0755 unicore /opt/unicore/unicore
sudo systemctl start unicore
sudo systemctl status unicore
```

Keep the existing `/etc/unicore.env` and `/var/lib/unicore` unless the release notes explicitly require a configuration change.

## Automated ARM validation

UniCore validates Raspberry Pi release targets automatically before changes can pass the required `verify` gate:

- ARM64 is executed natively on a GitHub-hosted ARM64 Linux runner.
- ARM64 is also executed under QEMU.
- ARMv7 is executed under QEMU.
- The runtime tests verify startup, `/health`, authentication, protected API access, SQLite database creation and restart behavior.

For v1.0, these automated checks are the required ARM runtime validation. A physical Raspberry Pi is **not** required as a release blocker.

This means UniCore can state that the ARM64 and ARMv7 Linux builds are automatically runtime-tested, but it does not claim that a particular Raspberry Pi model or Raspberry Pi OS image was physically tested. Physical-device soak and thermal/resource measurements can be added later as extra field validation.
