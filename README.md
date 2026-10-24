# fear-miner

**English** · [Português (Brasil)](README.pt-BR.md)

Multi-algorithm NVIDIA GPU miner. Packages for HiveOS, Linux and Windows.

[![release](https://img.shields.io/badge/release-1.4.1-2b7bd6)](https://github.com/fearke85/fear-miner/releases/tag/v1.4.1)
![HiveOS](https://img.shields.io/badge/HiveOS-jammy-3a9a3a)
![Linux](https://img.shields.io/badge/Linux-glibc%202.35%2B-3a9a3a)
![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-3a9a3a)
[![Discord](https://img.shields.io/badge/chat-Discord-5865f2)](https://discord.gg/uK93NPAhbd)

## Coins

Pick your coin. Its page has the pool and wallet settings, the cards it supports and its own
options.

| Coin | Algorithm | Cards | Docs |
| --- | --- | --- | --- |
| Keryx | `keryxhash` | NVIDIA Turing or newer, 8 GB or more | [coins/keryx](coins/keryx/README.md) |
| Vela | `vela` | NVIDIA Turing or newer | [coins/vela](coins/vela/README.md) |
| Numen | `numen` | NVIDIA Turing or newer | [coins/numen](coins/numen/README.md) |
| Vearl (testnet) | `vearl` | NVIDIA Ampere or newer | [coins/vearl](coins/vearl/README.md) |

> [!WARNING]
> **Keryx:** the H14 hard fork is live. Versions before 0.0.22 are invalid.
> See [coins/keryx](coins/keryx/README.md).

## Download: 1.4.1 (2026-10-24)

One package per platform. It mines every coin in the table above.

| Platform | File | Install guide |
| --- | --- | --- |
| HiveOS | [fear-miner-1.4.1.tar.gz](https://github.com/fearke85/fear-miner/releases/download/v1.4.1/fear-miner-1.4.1.tar.gz) | [docs/en/hiveos.md](docs/en/hiveos.md) |
| Linux | [fear-miner-linux-1.4.1.tar.gz](https://github.com/fearke85/fear-miner/releases/download/v1.4.1/fear-miner-linux-1.4.1.tar.gz) | [docs/en/linux.md](docs/en/linux.md) |
| Windows | [fear-miner-windows-1.4.1.zip](https://github.com/fearke85/fear-miner/releases/download/v1.4.1/fear-miner-windows-1.4.1.zip) | [docs/en/windows.md](docs/en/windows.md) |

What changed: [release notes](https://github.com/fearke85/fear-miner/releases/tag/v1.4.1) ·
[CHANGELOG](CHANGELOG.md). Checksums are on the release page.

## Getting started

1. Choose your coin in the table above and note its pool, wallet and algorithm settings.
2. Install the package for your platform with its guide: [HiveOS](docs/en/hiveos.md),
   [Linux](docs/en/linux.md) or [Windows](docs/en/windows.md).
3. Check that it mines: the HiveOS dashboard, or `curl 127.0.0.1:4060/stats` on the rig.

## Requirements for every coin

- An NVIDIA card the coin supports (see its page).
- NVIDIA driver 580 or newer (CUDA 13.2). The packages bring the CUDA libraries, not the driver.
- HiveOS on the Ubuntu 22.04 (jammy) image, Linux with glibc 2.35 or newer, or Windows 10 / 11.

## Documentation

| Topic | For every coin | Keryx | Vela | Numen | Vearl |
| --- | --- | --- | --- | --- | --- |
| Install | [HiveOS](docs/en/hiveos.md) · [Linux](docs/en/linux.md) · [Windows](docs/en/windows.md) | [Settings per platform](coins/keryx/README.md#settings) | [Settings per platform](coins/vela/README.md#settings) | [Settings per platform](coins/numen/README.md#settings) | [Settings per platform](coins/vearl/README.md#settings) |
| Options | [Miner options](docs/en/options.md) | [Keryx options](coins/keryx/docs/en/options.md) | [Vela options](coins/vela/README.md#vela-options) | [Numen options](coins/numen/README.md#numen-options) | [Vearl options](coins/vearl/README.md#vearl-options) |
| Problems | [Troubleshooting](docs/en/troubleshooting.md) | [Keryx troubleshooting](coins/keryx/docs/en/troubleshooting.md) | [Vela troubleshooting](coins/vela/README.md#troubleshooting) | [Numen troubleshooting](coins/numen/README.md#troubleshooting) | [Vearl troubleshooting](coins/vearl/README.md#troubleshooting) |
| Solo mining | | [Keryx solo](coins/keryx/docs/en/solo.md) | [Vela solo](coins/vela/README.md#solo-on-your-own-node) | [Numen solo](coins/numen/README.md#solo-through-rplant) | [Vearl solo](coins/vearl/README.md#solo) |

## Community tools

[Juliano Caju](https://www.julianocaju.com.br/en/calculator/) has tools for several coins, in
English and Portuguese:

- [Overclock table](https://www.julianocaju.com.br/en/overclocks/) per card and coin
- [Mining calculator](https://www.julianocaju.com.br/en/calculator/)
- [Profitability per card](https://www.julianocaju.com.br/en/profitability/)

## Help

- [Discord](https://discord.gg/uK93NPAhbd)
- [Open an issue](https://github.com/fearke85/fear-miner/issues/new/choose) and attach `log.txt`

## License

fear-miner is proprietary. The [LICENSE](LICENSE) allows use of the unmodified software only.
Modification, extraction and attempts to break the protected encoding are prohibited.
Third-party components in the package are listed in [NOTICE](NOTICE). This repository publishes
the release archives and the documentation. It does not publish source code.
