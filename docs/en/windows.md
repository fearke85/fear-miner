# Windows

**English** · [Português (Brasil)](../pt-BR/windows.md) · [Back to README](../../README.md)

How to install fear-miner on Windows, for any coin. The values for your coin are on its page:
[Keryx](../../coins/keryx/README.md#runsh-linux-and-startbat-windows).

## Before you start

- Windows 10 or 11, 64-bit.
- NVIDIA driver 580 or newer, from nvidia.com or the NVIDIA app. The package brings the CUDA
  libraries.
- A card your coin supports, and the free disk your coin's page asks for, next to the miner.

## Install

1. Download `fear-miner-windows-0.0.31.zip` from the
   [release page](https://github.com/fearke85/fear-miner/releases/tag/v0.0.31).
2. Extract it to a folder of its own, for example `C:\fear-miner`.
3. Right-click `start.bat`, choose **Edit** (or open it in Notepad).

## Settings in start.bat

`WALLET`, `POOL`, `NODE` and any line your coin adds take the values from your coin's page.

| Line | What to put |
| --- | --- |
| `WALLET` | Your payout address |
| `WORKER` | A name for this PC on the pool |
| `POOL` | The pool, `stratum+tcp://host:port` |
| `NODE` | Solo only: `grpc://IP:PORT` of your node. Leave `POOL=` empty |
| `DEVICES` | `all`, or the cards to mine on, for example `0,2,5` |
| `EXTRA` | Coin options |
| `STATS` | Stats API address. `0.0.0.0:4060` opens it to your network |

Miner options: [options.md](options.md).

## Run

Save `start.bat` and double-click it. Keep the window open: closing it stops the miner.

## Update to a new version

Extract the new zip over the old folder, then copy your settings into the new `start.bat`. What
the miner keeps is in `data` and stays.

## Where things are

| What | Where |
| --- | --- |
| Log with warnings, errors and crash reports | `log.txt` next to `fear-miner.exe` |
| Data the miner keeps | `data`. Set `FEAR_DATA_DIR` to move it |
| Hashrate and shares | `http://127.0.0.1:4060/stats` in a browser |
