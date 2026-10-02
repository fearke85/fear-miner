# fear-miner

Install packages for HiveOS. This repository publishes the license texts and the release archives. It does not publish source code.

fear-miner is proprietary. The [LICENSE](LICENSE) grants use of the unmodified software only. Modification, extraction, and attempts to break the protected encoding are prohibited. Third-party software in the package is listed in [NOTICE](NOTICE).

## Flight sheet

Create a flight sheet with miner **Custom**.

| Field | Value |
| --- | --- |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/vX.Y.Z/fear-miner-X.Y.Z.tar.gz` |
| Miner name | `fear-miner` |
| Pool URL | `host:port` (a `stratum+tcp://` prefix is stripped) |
| Wallet template | pool username |
| Password | pool password (`x` when empty) |

Use the asset from the latest release. The archive name is `fear-miner-<version>.tar.gz`. The version does not contain a hyphen, so Hive detects the miner name `fear-miner`.

To install from the rig console:

```
/hive/miners/custom/custom-get https://github.com/fearke85/fear-miner/releases/download/vX.Y.Z/fear-miner-X.Y.Z.tar.gz
```

Add `-f` to reinstall. Reinstall replaces `/hive/miners/custom/fear-miner` and leaves `/var/lib/fear-miner` in place.

## Rig requirements

- HiveOS on Ubuntu 22.04 (jammy). The Ubuntu 20.04 image is not supported.
- NVIDIA driver new enough for CUDA 13.2 (driver series 580 or newer). The package brings the CUDA runtime libraries. It does not bring the driver.
- The first start downloads the public model set into `/var/lib/fear-miner/models`.

## Extra config arguments

Flags before `--` are miner flags. Flags after `--` are coin flags. Example, pinning two cards and one tier:

```
--device 0,1 -- --tier 2
```

Escrow key, certificate, and state are stored under `/var/lib/fear-miner`. The Kubo repo is `/var/lib/fear-miner/.ipfs`.
