# Windows

**English** · [Português (Brasil)](../pt-BR/windows.md) · [Back to README](../../README.md)

How to install fear-miner on Windows, for any coin. The values for your coin are on its page:
[Keryx](../../coins/keryx/README.md#start-keryxsh-linux-and-start-keryxbat-windows), [Vela](../../coins/vela/README.md#start-velash-linux-and-start-velabat-windows), [Numen](../../coins/numen/README.md#start-numensh-linux-and-start-numenbat-windows).

## Before you start

- Windows 10 or 11, 64-bit.
- NVIDIA driver 580 or newer, from nvidia.com or the NVIDIA app. The package brings the CUDA
  libraries.
- A card your coin supports, and the free disk your coin's page asks for, next to the miner.

## Install

1. Download `fear-miner-windows-1.5.0.zip` from the
   [release page](https://github.com/fearke85/fear-miner/releases/tag/v1.5.0).
2. Extract it to a folder of its own, for example `C:\fear-miner`.
3. Right-click `start-keryx.bat` (Vela: `start-vela.bat`), choose **Edit** (or open it in Notepad).

## Settings in the start script

Each coin has its own script: `start-keryx.bat` for Keryx, `start-vela.bat` for Vela, `start-numen.bat` for Numen. Leave one
line uncommented, the pool line or the solo line, and put your address in `-wallet`. The pool, the node and the other
values are on your coin's page.

Other options go on that same line. Miner options: [options.md](options.md).

## Run

Save the script and double-click it. Keep the window open: closing it stops the miner.
When CUDA dies on a card, the miner exits and the script starts it again after 3 seconds.

## Update to a new version

Extract the new zip over the old folder, then copy your line into the new start script. What
the miner keeps is in `keryx` (Vela: `vela`) and stays. An older `data` folder is picked up from there.

## Where things are

| What | Where |
| --- | --- |
| Log with warnings, errors and crash reports | `log.txt` next to `fear-miner.exe` |
| Data the miner keeps | `keryx` (`models\`, and `escrow\<wallet>\`), `vela` (`models\`). Set `FEAR_DATA_DIR` to move it |
| Hashrate and shares | `http://127.0.0.1:4060/stats` in a browser |
