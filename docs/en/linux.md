# Linux

**English** · [Português (Brasil)](../pt-BR/linux.md) · [Back to README](../../README.md)

For a plain Linux machine, outside HiveOS.

## Before you start

- x86-64 Linux with glibc 2.35 or newer (Ubuntu 22.04, Debian 12 and newer).
- NVIDIA driver 580 or newer. Check with `nvidia-smi`. The package brings the CUDA libraries.
- Cards: Turing or newer. See [which tier your card mines](../../README.md#which-tier-does-my-card-mine).
- Disk next to the miner for the model of each tier you mine.

## Install

```
wget https://github.com/fearke85/fear-miner/releases/download/v0.0.31/fear-miner-linux-0.0.31.tar.gz
tar -xzf fear-miner-linux-0.0.31.tar.gz
cd fear-miner
nano run.sh
```

## Settings in run.sh

Edit the lines at the top of `run.sh`, then save:

| Line | What to put |
| --- | --- |
| `WALLET` | Your Keryx address, `keryx:...` |
| `WORKER` | A name for this rig on the pool |
| `POOL` | The pool, for example `stratum+tcp://krx.suprnova.cc:4404` |
| `NODE` | Solo only: `grpc://IP:PORT` of your node. Leave `POOL=""` |
| `ESCROW_CERT` | Solo only, first start: the 128 hex characters from your wallet. See [solo.md](solo.md) |
| `DEVICES` | `all`, or the cards to mine on, for example `0,2,5` |
| `EXTRA` | More options, for example `(--tier 0)` or `(--headless)` |
| `STATS` | Stats API address. `0.0.0.0:4060` opens it to your network |

On a machine with no monitor, add `--headless` to `EXTRA`: 10 and 12 GB cards then mine a higher
tier. Every option is listed in [configuration.md](configuration.md).

## Run

```
./run.sh
```

The first start downloads the model, which takes a few minutes. To keep the miner running after
you log out, start it in `screen` or `tmux`, or as a systemd service.

## Update to a new version

Unpack the new archive over the old folder, then copy your settings into the new `run.sh`. Models
and escrow files are in `./data` and stay.

## Where things are

| What | Where |
| --- | --- |
| Log with warnings, missed requests and crash reports | `log.txt` next to the miner |
| Models, escrow files | `./data`. Set `FEAR_DATA_DIR` to move them |
| Hashrate and shares | `curl 127.0.0.1:4060/stats` |
