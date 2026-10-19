# Linux

**English** · [Português (Brasil)](../pt-BR/linux.md) · [Back to README](../../README.md)

How to install fear-miner on a plain Linux machine, outside HiveOS, for any coin. The values for
your coin are on its page: [Keryx](../../coins/keryx/README.md#runsh-linux-and-startbat-windows).

## Before you start

- x86-64 Linux with glibc 2.35 or newer (Ubuntu 22.04, Debian 12 and newer).
- NVIDIA driver 580 or newer. Check with `nvidia-smi`. The package brings the CUDA libraries.
- A card your coin supports, and the free disk your coin's page asks for, next to the miner.

## Install

```
wget https://github.com/fearke85/fear-miner/releases/download/v1.1.0/fear-miner-linux-1.1.0.tar.gz
tar -xzf fear-miner-linux-1.1.0.tar.gz
cd fear-miner
nano run.sh
```

## Settings in run.sh

Edit the lines at the top of `run.sh`, then save. `WALLET`, `POOL`, `NODE` and any line your coin
adds take the values from your coin's page.

| Line | What to put |
| --- | --- |
| `WALLET` | Your payout address |
| `WORKER` | A name for this rig on the pool |
| `POOL` | The pool, `stratum+tcp://host:port` |
| `NODE` | Solo only: `grpc://IP:PORT` of your node. Leave `POOL=""` |
| `DEVICES` | `all`, or the cards to mine on, for example `0,2,5` |
| `EXTRA` | Coin options, for example `(--headless)` |
| `STATS` | Stats API address. `0.0.0.0:4060` opens it to your network |

Miner options: [options.md](options.md).

## Run

```
./run.sh
```

To keep the miner running after you log out, start it in `screen` or `tmux`, or as a systemd
service.

## Update to a new version

Unpack the new archive over the old folder, then copy your settings into the new `run.sh`. What
the miner keeps is in `./data` and stays.

## Where things are

| What | Where |
| --- | --- |
| Log with warnings, errors and crash reports | `log.txt` next to the miner |
| Data the miner keeps | `./data`. Set `FEAR_DATA_DIR` to move it |
| Hashrate and shares | `curl 127.0.0.1:4060/stats` |
