# Miner options

**English** · [Português (Brasil)](../pt-BR/options.md) · [Back to README](../../README.md)

Options that work the same for every coin. Coin options are on each coin's page:
[Keryx](../../coins/keryx/docs/en/options.md), [Vela](../../coins/vela/README.md#vela-options).

## Where options go

| Platform | Where |
| --- | --- |
| HiveOS | Flight sheet, **Extra config arguments** |
| Linux | On the line in the coin's `start-<coin>.sh` |
| Windows | On the line in the coin's `start-<coin>.bat` |

Miner flags take one hyphen. Coin flags take two. They can sit in any order, on the same line.
A bare `--` from an older command line is still accepted and ignored.

```
-device 1,6 -stats 0.0.0.0:4060 --tier 2
└──── miner flags ─────────────┘ └ coin ┘
```

Paths are one word, with no quotes.

## Options

| Option | What it does | Default |
| --- | --- | --- |
| `-coin keryxhash` | Coin to mine: `keryxhash` or `vela`. Same as a positional `keryxhash`; when both are set, `-coin` wins | required |
| `-device 0,2,5` | Mine on these cards only, by the numbers the miner shows | `all` |
| `-pool host:port` | Pool to mine on | set by the launcher |
| `-node grpc://IP:PORT` | Your node, for solo mining | set by the launcher |
| `-wallet ADDRESS` | Payout address. `-address` is the same field; the last one wins | set by the launcher |
| `-worker NAME` | Rig name. Replaces the part of the wallet after the first `.` | |
| `-user ADDRESS.WORKER` | Full pool username. Prefer `-wallet` and `-worker` | set by the launcher |
| `-password x` | Pool password | `x` |
| `-stats ADDRESS:PORT` | Address of the stats API (`GET /stats`) | `127.0.0.1:4060` |
| `-log-file PATH` | Where to write `log.txt` | next to the miner |

Two hyphens still work for these flags (`--pool`, `--device`). Coin flags do not: `--escrow-dir`
is a coin flag, `-escrow-dir` is rejected.

The stats API has no password. `0.0.0.0:4060` opens it to every machine that can reach the rig,
so keep it on your LAN.

## Overclock

The miner sets clocks and fans itself, on Linux and Windows, through the NVIDIA driver (NVML).

| Option | What it does |
| --- | --- |
| `-cclock 275` | Core clock offset in MHz. Negative lowers it: `-cclock -100` |
| `-mclock 1000` | Memory clock offset in MHz. Negative lowers it: `-mclock -500`. The memory clock the miner shows moves by half the value |
| `-lock-cclock 2610` | Locks the core clock at this MHz |
| `-lock-mclock 810` | Locks the memory clock at this MHz (RTX 30 and newer) |
| `-fan 75` | Fan speed in percent, every fan of the card |

One value sets every card. Cards that differ take a list, one value per card, in the order of
`-device`; `*` leaves that card as it is:

```
-device 0,1,2 -cclock 275,250,* -lock-cclock 2610,1350,1350 -fan 75
```

Here card 0 gets +275 and 2610 MHz, card 1 +250 and 1350 MHz, card 2 keeps its offset and gets
1350 MHz, and every fan runs at 75%. Without `-device`, the list follows the card numbers the
miner shows: 0, 1, 2…

- A list with the wrong number of values changes nothing on any card, and the log says so. If
  a card drops off the bus, the numbers shift; the miner then mines at stock instead of putting
  one card's clocks on another.
- Linux needs root ([with sudo](linux.md#with-sudo)) and Windows needs **Run as administrator**.
  HiveOS already runs the miner as root.
- On exit (Ctrl+C, or quitting the screen), the miner puts back what it changed: offsets 0,
  clocks unlocked, fans on auto. If it is killed, the settings stay until the next start.
- On HiveOS, use either these flags or the OC page for a card, not both: the miner's exit
  undoes Hive's lock and fan until Hive applies its profile again.

## Environment variables

| Variable | What it does |
| --- | --- |
| `FEAR_DATA_DIR` | Linux and Windows: folder for the data the miner keeps. Default `keryx` (Vela: `vela`) next to the miner |
| `FEAR_SYNC=block` | Keryx: lower CPU use on rigs with many GPUs and few cores, for about 0.1% less hashrate |
| `FEAR_SYNC=spin` | Keryx: one full CPU core per GPU. Vela does not read `FEAR_SYNC` |

## Examples

| Goal | HiveOS Extra config | `start-<coin>.sh` / `start-<coin>.bat` |
| --- | --- | --- |
| Cards 0 and 1 only | `-device 0,1` | `-device 0,1` on the start line |
| Stats on the LAN | `-stats 0.0.0.0:4060` | `-stats 0.0.0.0:4060` on the start line |
| Data on another disk | | `FEAR_DATA_DIR=/data/fear-miner` |
| Overclock, same on every card | `-cclock 275 -lock-cclock 2610 -lock-mclock 810 -fan 75` | the same, on the start line |
