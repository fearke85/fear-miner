# HiveOS

**English** · [Português (Brasil)](../pt-BR/hiveos.md) · [Back to README](../../README.md)

How to install fear-miner on HiveOS, for any coin. The values for your coin (algorithm, wallet
template, pool URL) are on its page: [Keryx](../../coins/keryx/README.md#hiveos-flight-sheet),
[Vela](../../coins/vela/README.md#hiveos-flight-sheet),
[Numen](../../coins/numen/README.md#hiveos-flight-sheet).

## Before you start

- HiveOS on the Ubuntu 22.04 (jammy) image. The 20.04 image is not supported.
- NVIDIA driver 580 or newer. Update it from the HiveOS dashboard or with `nvidia-driver-update`.
- A card your coin supports, and the free disk your coin's page asks for.

## Flight sheet

Create a flight sheet with miner **Custom**:

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.4.3/fear-miner-1.4.3.tar.gz` |
| Hash algorithm | from your coin's page |
| Wallet and worker template | from your coin's page |
| Pool URL | from your coin's page |
| Password | `x`, or the pool password |
| Extra config arguments | Leave empty, or see below |

The Pool URL needs its prefix: `stratum+tcp://` for a pool, `grpc://` for a node. A bare
`host:port` or `http://` is refused.

Apply the flight sheet. The dashboard shows the hashrate once the cards are mining.

## Install from the rig console

```
/hive/miners/custom/custom-get https://github.com/fearke85/fear-miner/releases/download/v1.4.3/fear-miner-1.4.3.tar.gz
```

Add `-f` to reinstall.

## Update to a new version

Change the version in the Installation URL, twice: in `v1.4.3` and in
`fear-miner-1.4.3.tar.gz`. The rest of the flight sheet stays. Keeping the old URL keeps
installing the old version.

Everything the miner keeps (models, keys, the log) stays in `/var/lib/fear-miner` across updates
and reinstalls. Escrow files for each wallet are in `escrow/<wallet>/` there. Models stay in
`models/`, or wherever `--models-dir` points.

## Extra config arguments

Miner flags take one hyphen. Coin flags take two. Hash algorithm on the flight sheet is the
coin (`-coin`); a `-coin` in Extra config arguments overrides it, for a coin HiveOS does not list
(Vela). A bare `--` from an older sheet is still accepted.

```
-device 0,2 -stats 0.0.0.0:4060 --tier 2
```

| What | Extra config arguments |
| --- | --- |
| Mine on cards 0 and 2 only | `-device 0,2` |
| Open the stats API to your LAN | `-stats 0.0.0.0:4060` |
| Mine Vela, which is not in HiveOS's Hash algorithm list | `-coin vela` |

The package already runs headless. Miner options: [options.md](options.md). Coin options: your
coin's page ([Keryx](../../coins/keryx/docs/en/options.md), [Vela](../../coins/vela/README.md#vela-options),
[Numen](../../coins/numen/README.md#numen-options)).

## Where things are

| What | Where |
| --- | --- |
| Log with warnings, errors and crash reports | `/var/lib/fear-miner/log.txt` |
| Data the miner keeps | `/var/lib/fear-miner` |
| Miner console | `miner` in the rig shell, or the dashboard's miner log |

## CPU use on rigs with few cores

Keryx: on a rig with many GPUs and a small CPU, set `FEAR_SYNC=block` in the flight sheet
environment to lower CPU use, for about 0.1% less hashrate. `FEAR_SYNC=spin` uses one full core
per GPU.

Vela leaves the CPU idle while the cards work and does not read `FEAR_SYNC`.
