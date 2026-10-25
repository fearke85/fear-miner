# Vela

**English** · [Português (Brasil)](README.pt-BR.md) · [All coins](../../README.md)

Mining Vela with fear-miner. Algorithm: `vela`. Pool mining on
[suprnova](https://vela.suprnova.cc) or [AriaPool](https://pool.ariabrain.com/vela.html), and solo
mining on your own Vela node.

Vela is a proof-of-inference coin: each attempt is one image-model inference, so the miner shows
its speed in **inferences per second** (`inf/s`) and its efficiency in **inferences per joule**
(`inf/J`). HiveOS knows hash units only and shows the same number as H/s.

## Cards

- NVIDIA Turing or newer (RTX 20xx, 30xx, 40xx, 50xx).
- Pascal (GTX 10xx) and older are not supported.

Measured with fear-miner on a HiveOS rig, at the overclock that rig uses for Keryx (power limit
at default, fans 75-85%). Watts are the card's draw while mining. Where the rig has two cards of a
model, the range covers both.

| Card | inf/s | Watts | inf/J | Core lock | Core offset | Memory offset |
| --- | --- | --- | --- | --- | --- | --- |
| RTX 3060 | 13.6-13.7 | 78-83 | 0.166-0.173 | 1350 MHz | +200 / +255 | -1000 |
| RTX 3070 | 20.9 | 123 | 0.170 | 1250 MHz | +250 | +1000 |
| RTX 3080 | 27.6 | 190-193 | 0.143-0.145 | 1100 MHz | +250 | -2000 |
| RTX 5070 Ti | 57.8-57.9 | 197-211 | 0.274-0.294 | 2300 MHz | +450 | 0 |

fear-miner 1.3.2 is about 3% faster than these rates at the same overclock, and a little more
efficient (higher inf/J).

Vela's speed follows the core clock: a higher core lock gives more inf/s and draws more watts.
Vela keeps the card at full load. Watch the temperature: an RTX 5070 Ti at stock settings reached
84 °C on an open rig. A power limit or a lower core lock keeps it cooler.

## Disk

The model (1.2 GB) downloads on the first start and is checked before use. It stays for the next
starts and updates:

| Platform | Model folder |
| --- | --- |
| HiveOS | `/var/lib/fear-miner/vela/models` |
| Linux and Windows | `vela/models` next to the miner, or under `FEAR_DATA_DIR` |

## Settings

Install the package with your platform's guide, then use these values.

### Pools

| Pool | `-pool` on Linux and Windows | Pool URL on HiveOS |
| --- | --- | --- |
| [suprnova](https://vela.suprnova.cc) | `vela.suprnova.cc:7601` | `stratum+tcp://vela.suprnova.cc:7601` |
| [AriaPool](https://pool.ariabrain.com/vela.html) | `http://159.69.194.46:3349` | `http://159.69.194.46:3349` |

The login is the same on both: your Vela address and a worker name, password `x`. The tables below
use suprnova; for AriaPool, change only the pool.

### HiveOS flight sheet

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.4.2/fear-miner-1.4.2.tar.gz` |
| Hash algorithm | `poi`, or any one from the list (see below) |
| Wallet and worker template | `%WAL%.%WORKER_NAME%` |
| Pool URL | `stratum+tcp://vela.suprnova.cc:7601` |
| Password | `x` |
| Extra config arguments | `-coin vela` |

HiveOS has no `vela` in its Hash algorithm list. `poi` means Vela to the miner. With any other
algorithm, put `-coin vela` in Extra config arguments: it overrides the Hash algorithm, and the
miner mines Vela. Vela options go
on the same line, after it: `-coin vela --batch 4 --lanes 1`.

The wallet is your Vela address, `vela1...`. Install guide: [HiveOS](../../docs/en/hiveos.md).

### start-vela.sh (Linux) and start-vela.bat (Windows)

The pool line is already filled in. Put your address in `-wallet`.

| What | Value |
| --- | --- |
| `-wallet` | Your Vela address, `vela1...` |
| `-worker` | A name for this rig on the pool |
| `-pool` | `vela.suprnova.cc:7601` |

Install guides: [Linux](../../docs/en/linux.md) · [Windows](../../docs/en/windows.md).

### Solo on your own node

Solo mining needs a synced Vela node with its RPC server on. The block reward goes to `-wallet`.

```
./fear-miner -coin vela -node http://RPCUSER:RPCPASSWORD@127.0.0.1:18743 -wallet vela1...
```

Use the `rpcuser`, `rpcpassword` and `rpcport` of your node's configuration. On HiveOS, put
`-coin vela -node http://RPCUSER:RPCPASSWORD@NODE_IP:18743` in Extra config arguments: `-node`
takes the place of the Pool URL.

## Vela options

Coin options take two hyphens. On HiveOS they go in Extra config arguments.

| Option | What it does |
| --- | --- |
| `--batch N` | Inferences per launch, 1 to 16. The miner picks it from the card's memory. |
| `--lanes N` | Parallel streams per card, 1 to 4. The miner picks it from the card's memory. |
| `--suggest-diff D` | Asks the pool for share difficulty `D` (suprnova only). |
| `--models-dir PATH` | Keep the model in `PATH`. |
| `--model FILE` | Use this model file where it is, instead of downloading it. |

The automatic choice is the fastest on every card we measured. On an RTX 5070 Ti,
`--batch 4 --lanes 1` is 5% slower and 3% more efficient (inf/J).

## Not yet

- suprnova's TLS port.

## Troubleshooting

| What you see | What to do |
| --- | --- |
| `not enough disk for ...` at the first start | Free 1.2 GB where the model folder is, or point `--models-dir` elsewhere. |
| `model hash ... does not match` | The model file is damaged or a different one. Delete it; the miner downloads it again. |
| `... is too little for ...` | The card has too little free memory. Close what uses it, or pass `--batch 1 --lanes 1`. |
| Shares rejected as stale | Check the rig's network; a slow link turns late shares into stale ones. |

General problems: [troubleshooting](../../docs/en/troubleshooting.md).

## Help

- [Discord](https://discord.gg/uK93NPAhbd)
- [Open an issue](https://github.com/fearke85/fear-miner/issues/new/choose) and attach `log.txt`
