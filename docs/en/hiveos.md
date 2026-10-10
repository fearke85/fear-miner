# HiveOS

**English** · [Português (Brasil)](../pt-BR/hiveos.md) · [Back to README](../../README.md)

## Before you start

- HiveOS on the Ubuntu 22.04 (jammy) image. The 20.04 image is not supported.
- NVIDIA driver 580 or newer. Update it from the HiveOS dashboard or with `nvidia-driver-update`.
- Cards: Turing or newer. See [which tier your card mines](../../README.md#which-tier-does-my-card-mine).
- Disk for the model of each tier you mine. A 32 GB USB stick fits tier 2.

## Flight sheet

Create a flight sheet with miner **Custom** and fill in:

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-0.0.31.tar.gz` |
| Hash algorithm | `keryxhash` |
| Wallet and worker template | Pool: `%WAL%.%WORKER_NAME%`. Solo: `%WAL%` |
| Pool URL | Pool: `stratum+tcp://krx.suprnova.cc:4404`. Solo: `grpc://IP:PORT` of your node |
| Password | `x`, or the pool password |
| Extra config arguments | Leave empty, or see below |

The wallet is your Keryx address, `keryx:...`. The Pool URL needs its prefix: `stratum+tcp://` for
a pool, `grpc://` for a node. A bare `host:port` or `http://` is refused.

Apply the flight sheet. The first start downloads the model, which takes a few minutes. The
dashboard shows the hashrate once the cards are mining.

For solo mining, read [solo.md](solo.md) first: the first start needs a step in your wallet.

## Install from the rig console

```
/hive/miners/custom/custom-get https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-0.0.31.tar.gz
```

Add `-f` to reinstall.

## Update to a new version

Change the version in the Installation URL, twice: in `v0.0.31` and in
`fear-miner-0.0.31.tar.gz`. The rest of the flight sheet stays. Keeping the old URL keeps
installing the old version.

Models, escrow files and the log stay in `/var/lib/fear-miner` across updates and reinstalls.

## Extra config arguments

Miner options go before `--`, Keryx options after it. Common examples:

| What | Extra config arguments |
| --- | --- |
| Mine on cards 0 and 2 only | `--device 0,2` |
| Force tier 2 on every card | `-- --tier 2` |
| Cards 1 and 6, tier 3 on both | `--device 1,6 -- --tier 3,3` |
| Open the stats API to your LAN | `--stats 0.0.0.0:4060` |
| Solo: first start with the escrow cert | `-- --escrow-cert PASTE_THE_128_HEX_CHARS` |
| Keep models on another disk | `-- --models-dir /data/models` |

The package already runs headless. Do not add `--headless`. Every option is listed in
[configuration.md](configuration.md).

## Where things are

| What | Where |
| --- | --- |
| Log with warnings, missed requests and crash reports | `/var/lib/fear-miner/log.txt` |
| Models | `/var/lib/fear-miner/models` |
| Escrow key, cert and state | `/var/lib/fear-miner` |
| Miner console | `miner` in the rig shell, or the dashboard's miner log |

A model another miner on the rig already downloaded (for example the Suprnova miner's
`/hive/miners/custom/models`) is checked and reused, without a second copy on disk.

## CPU use on rigs with few cores

On a rig with many GPUs and a small CPU, set `FEAR_SYNC=block` in the flight sheet environment to
lower CPU use, for about 0.1% less hashrate. `FEAR_SYNC=spin` uses one full core per GPU.
