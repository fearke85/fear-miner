# Windows

**English** · [Português (Brasil)](../pt-BR/windows.md) · [Back to README](../../README.md)

## Before you start

- Windows 10 or 11, 64-bit.
- NVIDIA driver 580 or newer, from nvidia.com or the NVIDIA app. The package brings the CUDA
  libraries.
- Cards: Turing or newer. See [which tier your card mines](../../README.md#which-tier-does-my-card-mine).
- Disk next to the miner for the model of each tier you mine.

## Install

1. Download `fear-miner-windows-0.0.31.zip` from the
   [release page](https://github.com/fearke85/fear-miner/releases/tag/v0.0.31).
2. Extract it to a folder of its own, for example `C:\fear-miner`.
3. Right-click `start.bat`, choose **Edit** (or open it in Notepad).

## Settings in start.bat

| Line | What to put |
| --- | --- |
| `WALLET` | Your Keryx address, `keryx:...` |
| `WORKER` | A name for this PC on the pool |
| `POOL` | The pool, for example `stratum+tcp://krx.suprnova.cc:4404` |
| `NODE` | Solo only: `grpc://IP:PORT` of your node. Leave `POOL=` empty |
| `ESCROW_CERT` | Solo only, first start: the 128 hex characters from your wallet. See [solo.md](solo.md) |
| `DEVICES` | `all`, or the cards to mine on, for example `0,2,5` |
| `EXTRA` | More options, for example `--tier 0` |
| `STATS` | Stats API address. `0.0.0.0:4060` opens it to your network |

Every option is listed in [configuration.md](configuration.md).

## Run

Save `start.bat` and double-click it. The first start downloads the model, which takes a few
minutes. Keep the window open: closing it stops the miner.

## Update to a new version

Extract the new zip over the old folder, then copy your settings into the new `start.bat`. Models
and escrow files are in `data` and stay.

## Where things are

| What | Where |
| --- | --- |
| Log with warnings, missed requests and crash reports | `log.txt` next to `fear-miner.exe` |
| Models, escrow files | `data`. Set `FEAR_DATA_DIR` to move them |
| Hashrate and shares | `http://127.0.0.1:4060/stats` in a browser |
