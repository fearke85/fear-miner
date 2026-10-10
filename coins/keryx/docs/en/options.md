# Keryx options

**English** · [Português (Brasil)](../pt-BR/options.md) · [Back to Keryx](../../README.md)

Options only Keryx has. They go after `--`. Options for every coin (`--device`, `--stats` and
others) are in [miner options](../../../../docs/en/options.md).

| Platform | Where |
| --- | --- |
| HiveOS | Extra config arguments, after `--`: `-- --tier 2` |
| Linux | `EXTRA=(--tier 2)` in `run.sh` |
| Windows | `set "EXTRA=--tier 2"` in `start.bat` |

## Options

| Option | What it does |
| --- | --- |
| `--tier 2` | Force one tier on every mining card. Not needed: the miner picks the highest tier itself |
| `--tier 2,0,2` | Force one tier per card, in `--device` order |
| `--headless` | Rig with no monitor: 10 and 12 GB cards mine a higher tier. Already on in HiveOS |
| `--inference-gpu N` | Card number that answers every AI request. `auto` picks one for you |
| `--escrow-cert HEX` | Solo, first start: the escrow cert from your wallet ([solo mining](solo.md)) |
| `--escrow-claim grpc://IP:PORT` | Pool rig: claim matured escrow through this node |
| `--escrow-dir PATH` | Folder for the escrow files |
| `--models-dir PATH` | Folder for the models |

A tier forced above what a card can mine may lower its hashrate a lot, or keep the card from
mining if no card on the rig can answer that tier's AI requests. The log says why.

## Examples

| Goal | HiveOS Extra config | `run.sh` / `start.bat` |
| --- | --- | --- |
| Tier 0 on every card | `-- --tier 0` | `EXTRA=(--tier 0)` / `set "EXTRA=--tier 0"` |
| Cards 1 and 6, tier 3 on both | `--device 1,6 -- --tier 3,3` | `DEVICES="1,6"` and `EXTRA=(--tier 3,3)` |
| Models on another disk | `-- --models-dir /data/models` | `EXTRA=(--models-dir /data/models)` |
| Linux rig with no monitor | already on | `EXTRA=(--headless)` |
