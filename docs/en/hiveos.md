# HiveOS

**English** · [Português (Brasil)](../pt-BR/hiveos.md) · [Back to README](../../README.md)

How to install fear-miner on HiveOS, for any coin. The values for your coin (algorithm, wallet
template, pool URL) are on its page: [Keryx](../../coins/keryx/README.md#hiveos-flight-sheet).

## Before you start

- HiveOS on the Ubuntu 22.04 (jammy) image. The 20.04 image is not supported.
- NVIDIA driver 580 or newer. Update it from the HiveOS dashboard or with `nvidia-driver-update`.
- A card your coin supports, and the free disk your coin's page asks for.

## Flight sheet

Create a flight sheet with miner **Custom**:

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.0.0/fear-miner-1.0.0.tar.gz` |
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
/hive/miners/custom/custom-get https://github.com/fearke85/fear-miner/releases/download/v1.0.0/fear-miner-1.0.0.tar.gz
```

Add `-f` to reinstall.

## Update to a new version

Change the version in the Installation URL, twice: in `v1.0.0` and in
`fear-miner-1.0.0.tar.gz`. The rest of the flight sheet stays. Keeping the old URL keeps
installing the old version.

Everything the miner keeps (models, keys, the log) stays in `/var/lib/fear-miner` across updates
and reinstalls.

## Extra config arguments

Miner options go before `--`, coin options after it:

```
--device 0,2 --stats 0.0.0.0:4060 -- <coin options>
```

| What | Extra config arguments |
| --- | --- |
| Mine on cards 0 and 2 only | `--device 0,2` |
| Open the stats API to your LAN | `--stats 0.0.0.0:4060` |

The package already runs headless. Miner options: [options.md](options.md). Coin options: your
coin's page ([Keryx](../../coins/keryx/docs/en/options.md)).

## Where things are

| What | Where |
| --- | --- |
| Log with warnings, errors and crash reports | `/var/lib/fear-miner/log.txt` |
| Data the miner keeps | `/var/lib/fear-miner` |
| Miner console | `miner` in the rig shell, or the dashboard's miner log |

## CPU use on rigs with few cores

On a rig with many GPUs and a small CPU, set `FEAR_SYNC=block` in the flight sheet environment to
lower CPU use, for about 0.1% less hashrate. `FEAR_SYNC=spin` uses one full core per GPU.
