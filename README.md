# Cloudflare WARP Binary for Debian (Trixie)

This repository automatically extracts and releases Cloudflare WARP binaries (`warp-svc`, `warp-cli`) for Debian Trixie on `amd64` and `arm64` architectures.

## Auto-Update

A GitHub Actions workflow runs every Sunday at 00:00 UTC to check for new versions from the official Cloudflare repository.

If a new version is detected:

1. The workflow automatically downloads the `.deb` packages.
2. Extracts the binaries (`warp-svc` and `warp-cli`).
3. Updates `warp-debian.version` in this repository.
4. Creates a new GitHub Release with the extracted binaries.

## Systemd Service File

Download the binaries and place them in `/usr/local/bin/`, Then create a
systemd service file `/etc/systemd/system/cloudflare-warp.service`:

```
[Unit]
Description=Cloudflare Zero Trust Client Daemon
After=pre-network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/warp-svc
DynamicUser=no
CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_BIND_SERVICE CAP_SYS_PTRACE CAP_DAC_READ_SEARCH CAP_NET_RAW CAP_SETUID CAP_SETGID
AmbientCapabilities=CAP_NET_ADMIN CAP_NET_BIND_SERVICE CAP_SYS_PTRACE CAP_DAC_READ_SEARCH CAP_NET_RAW CAP_SETUID CAP_SETGID
StateDirectory=cloudflare-warp
RuntimeDirectory=cloudflare-warp
LogsDirectory=cloudflare-warp
Restart=always

[Install]
WantedBy=multi-user.target
```
