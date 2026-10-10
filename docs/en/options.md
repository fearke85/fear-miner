# Miner options

**English** · [Português (Brasil)](../pt-BR/options.md) · [Back to README](../../README.md)

Options that work the same for every coin. Coin options are on each coin's page:
[Keryx](../../coins/keryx/docs/en/options.md).

## Where options go

| Platform | Where |
| --- | --- |
| HiveOS | Flight sheet, **Extra config arguments** |
| Linux | `run.sh`: `DEVICES`, `STATS` and `EXTRA`, or after `./run.sh` on the command line |
| Windows | `start.bat`: `DEVICES`, `STATS` and `EXTRA` |

**Miner options** go first. **Coin options** go after `--`. On HiveOS write the `--` yourself. In
`run.sh` and `start.bat` it is already there, so `EXTRA` holds coin options only.

```
--device 1,6 --stats 0.0.0.0:4060 -- <coin options>
└──── miner options ─────────────┘
```

Paths are one word, with no quotes.

## Options

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

## Environment variables

| Variable | What it does |
| --- | --- |
| `FEAR_DATA_DIR` | Linux and Windows: folder for the data the miner keeps. Default `data` next to the miner |
| `FEAR_SYNC=block` | Lower CPU use on rigs with many GPUs and few cores, for about 0.1% less hashrate |
| `FEAR_SYNC=spin` | One full CPU core per GPU |

## Examples

| Goal | HiveOS Extra config | `run.sh` / `start.bat` |
| --- | --- | --- |
| Cards 0 and 1 only | `--device 0,1` | `DEVICES="0,1"` |
| Stats on the LAN | `--stats 0.0.0.0:4060` | `STATS="0.0.0.0:4060"` |
| Data on another disk | | `FEAR_DATA_DIR=/data/fear-miner` |
