# fear-miner

**English** · [Português (Brasil)](README.pt-BR.md)

NVIDIA GPU miner for Keryx (keryxhash). Packages for HiveOS, Linux and Windows.

[![release](https://img.shields.io/badge/release-0.0.31-2b7bd6)](https://github.com/fearke85/fear-miner/releases/tag/v0.0.31)
![HiveOS](https://img.shields.io/badge/HiveOS-jammy-3a9a3a)
![Linux](https://img.shields.io/badge/Linux-glibc%202.35%2B-3a9a3a)
![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-3a9a3a)
[![Discord](https://img.shields.io/badge/chat-Discord-5865f2)](https://discord.gg/uK93NPAhbd)

> [!WARNING]
> **The H14 hard fork is live** (DAA 121,985,000, 2026-10-09). Versions before 0.0.22 are
> invalid: the network rejects their shares and blocks. Solo miners need keryx-node 1.6.4 or newer.

## Download: 0.0.31 (2026-10-09)

| Platform | File | Guide |
| --- | --- | --- |
| HiveOS | [fear-miner-0.0.31.tar.gz](https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-0.0.31.tar.gz) | [docs/en/hiveos.md](docs/en/hiveos.md) |
| Linux | [fear-miner-linux-0.0.31.tar.gz](https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-linux-0.0.31.tar.gz) | [docs/en/linux.md](docs/en/linux.md) |
| Windows | [fear-miner-windows-0.0.31.zip](https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-windows-0.0.31.zip) | [docs/en/windows.md](docs/en/windows.md) |

What changed: [release notes](https://github.com/fearke85/fear-miner/releases/tag/v0.0.31) ·
[CHANGELOG](CHANGELOG.md). Checksums are on the release page.

## Quick start

<details open>
<summary><b>HiveOS</b></summary>

Create a flight sheet with miner **Custom**:

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-0.0.31.tar.gz` |
| Wallet and worker template | `%WAL%.%WORKER_NAME%` (wallet `keryx:YOUR_ADDRESS`) |
| Pool URL | `stratum+tcp://krx.suprnova.cc:4404`, or `grpc://IP:PORT` of your node for solo |
| Password | `x` |

To update later, change the version in the Installation URL. The rest of the flight sheet stays.
Full guide: [docs/en/hiveos.md](docs/en/hiveos.md).
</details>

<details>
<summary><b>Linux</b></summary>

```
tar -xzf fear-miner-linux-0.0.31.tar.gz
cd fear-miner
nano run.sh     # set WALLET, WORKER and POOL (or NODE for solo)
./run.sh
```

Full guide: [docs/en/linux.md](docs/en/linux.md).
</details>

<details>
<summary><b>Windows</b></summary>

Unzip `fear-miner-windows-0.0.31.zip`, open `start.bat` in Notepad, set `WALLET`, `WORKER`
and `POOL` (or `NODE` for solo), save, and double-click it.

Full guide: [docs/en/windows.md](docs/en/windows.md).
</details>

## Requirements

- NVIDIA Turing or newer (RTX 20xx, 30xx, 40xx, 50xx) with 8 GB or more. 6 GB cards mine tier 0
  next to another card. Pascal (GTX 10xx, P104/P106) and older are not supported.
- NVIDIA driver 580 or newer (CUDA 13.2). The packages bring the CUDA libraries, not the driver.
- Free disk for the model of each tier you mine (table below). It downloads on the first start.
- HiveOS: the Ubuntu 22.04 (jammy) image. The 20.04 image is not supported.

## Which tier does my card mine?

The miner picks the highest tier each card supports by itself. You do not need `--tier`.

Free disk each tier needs for its model download:

| Tier | Free disk |
| --- | --- |
| 0 | ~6.7 GB |
| 1 | ~8.5 GB |
| 2 | ~10 GB |
| 3 | ~17 GB |
| 4 | ~30 GB |

## Is it working?

- Hashrate and shares: `curl 127.0.0.1:4060/stats` on the rig. On HiveOS they show in the dashboard.
- Warnings, missed AI requests and crash reports go to `log.txt`: `/var/lib/fear-miner/log.txt`
  on HiveOS, next to the miner on Linux and Windows.

## Help

- [Troubleshooting](docs/en/troubleshooting.md)
- [Solo mining](docs/en/solo.md) · [All options](docs/en/configuration.md)
- [Discord](https://discord.gg/uK93NPAhbd)
- [Open an issue](https://github.com/fearke85/fear-miner/issues/new/choose) and attach `log.txt`

## License

fear-miner is proprietary. The [LICENSE](LICENSE) allows use of the unmodified software only.
Modification, extraction and attempts to break the protected encoding are prohibited.
Third-party components in the package are listed in [NOTICE](NOTICE). This repository publishes
the release archives and the documentation. It does not publish source code.
