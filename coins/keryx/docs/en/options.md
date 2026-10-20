# Keryx options

**English** · [Português (Brasil)](../pt-BR/options.md) · [Back to Keryx](../../README.md)

Options only Keryx has. They take two hyphens. Miner flags take one (`-device`, `-stats`);
those are in [miner options](../../../../docs/en/options.md). A bare `--` from an older command
is still accepted.

| Platform | Where |
| --- | --- |
| HiveOS | Extra config arguments: `--tier 2` |
| Linux | On the line in `start-keryx.sh`, for example `--tier 2` |
| Windows | On the line in `start-keryx.bat`, for example `--tier 2` |

## Options

| Option | What it does |
| --- | --- |
| `--tier 2` | Force one tier on every mining card. Not needed: the miner picks the highest tier itself |
| `--tier 2,0,2` | Force one tier per card, in `-device` order |
| `--headless` | Rig with no monitor: 10 GB cards mine a higher tier. Already on in HiveOS |
| `--inference-gpu N` | Card number that answers every AI request. `auto` picks one for you |
| `--escrow-cert HEX` | Solo, first start: the escrow cert from your wallet ([solo mining](solo.md)) |
| `--escrow-claim grpc://IP:PORT` | Pool rig: claim matured escrow through this node |
| `--escrow-dir PATH` | Folder that holds one subfolder per wallet (`escrow.key`, `escrow.cert`, `escrow.state.json`) |
| `--models-dir PATH` | Folder for the models |

A card forced above its tier mines the forced tier only when that tier's model fits in its
memory; its AI requests are then answered by a larger card of that tier on the rig if there is
one, and more slowly if not. Otherwise the card mines the tier its memory holds. The log says
which tier each card mines and why.

## Examples

| Goal | HiveOS Extra config | `start-keryx.sh` / `start-keryx.bat` |
| --- | --- | --- |
| Tier 0 on every card | `--tier 0` | `--tier 0` on the start line |
| Cards 1 and 6, tier 1 on both | `-device 1,6 --tier 1,1` | `-device 1,6 --tier 1,1` on the start line |
| Models on another disk | `--models-dir /data/models` | `--models-dir /data/models` on the start line |
| Linux rig with no monitor | already on | `--headless` on the start line |
