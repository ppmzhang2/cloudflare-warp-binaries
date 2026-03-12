# Cloudflare WARP Binaries for Debian

Automatically extracts and publishes `warp-svc` and `warp-cli` binaries from
the official Cloudflare WARP Debian package (Trixie repository) for both
`amd64` and `arm64` architectures.

## How It Works

A GitHub Actions workflow ([`publish-warp-svc.yml`](.github/workflows/publish-warp-svc.yml)) runs automatically every Sunday at 00:00 UTC and:

1. Fetches the latest `cloudflare-warp` version from the Cloudflare Debian
   Trixie package repository.
2. Compares it against the version recorded in `warp-debian.version`.
3. If a newer version is found:
   - Downloads the `.deb` package for both `amd64` and `arm64`.
   - Extracts the `warp-svc` and `warp-cli` binaries from each package.
   - Commits the updated `warp-debian.version` to the repository.
   - Creates a new [GitHub Release](../../releases) with the extracted binaries
     as assets.

The workflow can also be triggered manually via the **Run workflow** button in
the Actions tab.

## Release Assets

Each release contains four binaries:

| File | Description |
|------|-------------|
| `warp-svc-amd64` | WARP service daemon for x86-64 |
| `warp-cli-amd64` | WARP CLI for x86-64 |
| `warp-svc-arm64` | WARP service daemon for ARM64 |
| `warp-cli-arm64` | WARP CLI for ARM64 |

## Usage

Download the appropriate binary for your architecture from the
[Releases](../../releases/latest) page and make it executable:

```bash
chmod +x warp-svc-amd64   # or warp-svc-arm64 / warp-cli-amd64 / warp-cli-arm64
```
