# Configuration

**English** · [Português (Brasil)](../pt-BR/configuration.md) · [Back to README](../../README.md)

## Where options go

| Platform | Where |
| --- | --- |
| HiveOS | Flight sheet, **Extra config arguments** |
| Linux | `EXTRA=( ... )` in `run.sh`, or after `./run.sh` on the command line |
| Windows | `set "EXTRA=..."` in `start.bat` |

Options come in two groups. **Miner options** go first. **Keryx options** go after `--`. On
HiveOS write the `--` yourself. In `run.sh` and `start.bat` it is already there, so `EXTRA` holds
Keryx options only.

```
--device 1,6 --stats 0.0.0.0:4060 -- --tier 3,3
└──── miner options ─────────────┘    └ Keryx ┘
```

Paths are one word, with no quotes.

## Miner options

| Option | What it does | Default |
| --- | --- | --- |
| `--device 0,2,5` | Mine on these cards only, by the numbers the miner shows | `all` |
| `--pool host:port` | Pool to mine on | set by the launcher |
| `--node grpc://IP:PORT` | Your node, for solo mining | set by the launcher |
| `--user ADDRESS.WORKER` | Pool username, or the payout address for solo | set by the launcher |
| `--password x` | Pool password | `x` |
| `--stats ADDRESS:PORT` | Address of the stats API (`GET /stats`) | `127.0.0.1:4060` |
| `--log-file PATH` | Where to write `log.txt` | next to the miner |

The stats API has no password. `0.0.0.0:4060` opens it to every machine that can reach the rig,
so keep it on your LAN.

## Keryx options (after `--`)

| Option | What it does |
| --- | --- |
| `--tier 2` | Force one tier on every mining card |
| `--tier 2,0,2` | Force one tier per card, in `--device` order |
| `--headless` | Rig with no monitor: 10 and 12 GB cards mine a higher tier. Already on in HiveOS |
| `--inference-gpu N` | Card number that answers every AI request. `auto` picks one for you |
| `--escrow-cert HEX` | Solo, first start: the escrow cert from your wallet ([solo.md](solo.md)) |
| `--escrow-claim grpc://IP:PORT` | Pool rig: claim matured escrow through this node |
| `--no-inference` | Solo only: mine without answering AI requests. Another rig on the same payout address must answer this rig's tiers, or the address takes strikes |
| `--escrow-dir PATH` | Folder for the escrow files |
| `--models-dir PATH` | Folder for the models |

A tier forced above what a card can mine may lower its hashrate a lot, or keep the card from
mining if no card on the rig can answer that tier's AI requests. The log says why.

## Environment variables

| Variable | What it does |
| --- | --- |
| `FEAR_DATA_DIR` | Linux and Windows: folder for models and escrow files. Default `data` next to the miner |
| `FEAR_SYNC=block` | Lower CPU use on rigs with many GPUs and few cores, for about 0.1% less hashrate |
| `FEAR_SYNC=spin` | One full CPU core per GPU |

## Examples

| Goal | HiveOS Extra config | `run.sh` / `start.bat` |
| --- | --- | --- |
| Cards 0 and 1 only | `--device 0,1` | `DEVICES="0,1"` |
| Tier 0 on every card | `-- --tier 0` | `EXTRA=(--tier 0)` / `set "EXTRA=--tier 0"` |
| Stats on the LAN | `--stats 0.0.0.0:4060` | `STATS="0.0.0.0:4060"` |
| Models on another disk | `-- --models-dir /data/models` | `FEAR_DATA_DIR=/data/fear-miner` |
