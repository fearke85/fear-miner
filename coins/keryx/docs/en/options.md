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
| `--headless` | Rig with no monitor: 10 GB cards mine a higher tier. Already on in HiveOS |
| `--inference-gpu N` | Card number that answers every AI request. `auto` picks one for you |
| `--escrow-cert HEX` | Solo, first start: the escrow cert from your wallet ([solo mining](solo.md)) |
| `--escrow-claim grpc://IP:PORT` | Pool rig: claim matured escrow through this node |
| `--escrow-dir PATH` | Folder for the escrow files |
| `--models-dir PATH` | Folder for the models |

A card forced above its tier mines the forced tier only when that tier's model fits in its
memory; its AI requests are then answered by a larger card of that tier on the rig if there is
one, and more slowly if not. Otherwise the card mines the tier its memory holds. The log says
which tier each card mines and why.

## Examples

| Goal | HiveOS Extra config | `run.sh` / `start.bat` |
| --- | --- | --- |
| Tier 0 on every card | `-- --tier 0` | `EXTRA=(--tier 0)` / `set "EXTRA=--tier 0"` |
| Cards 1 and 6, tier 1 on both | `--device 1,6 -- --tier 1,1` | `DEVICES="1,6"` and `EXTRA=(--tier 1,1)` |
| Models on another disk | `-- --models-dir /data/models` | `EXTRA=(--models-dir /data/models)` |
| Linux rig with no monitor | already on | `EXTRA=(--headless)` |
