# Vearl

**English** · [Português (Brasil)](README.pt-BR.md) · [All coins](../../README.md)

Mining Vearl (VRL) on its public testnet with fear-miner. Algorithm: `vearl`. Pool mining on
[AriaPool](https://pool.ariabrain.com/vrl.html) or [NurseryPool](https://vearl.nurserypool.com/),
and solo through either pool's solo port.

The testnet coins have no value. Its rewards program counts points per block; the rules and the
registration are on [vearl.org](https://vearl.org/participate/).

The miner shows its speed in MH/s and, next to it, in sigma/s, the unit the pools show.

## Cards

- NVIDIA Ampere or newer (RTX 30xx, 40xx, 50xx).
- Turing (RTX 20xx) and older are not supported: Vearl's work needs instructions they lack.

Measured with fear-miner at each rig's overclock (RTX 30 on a HiveOS rig, RTX 40 on another,
RTX 5070 Ti on a desktop at stock clocks):

| Card | MH/s | sigma/s |
| --- | --- | --- |
| RTX 3060 | 61 | 15,000 |
| RTX 3070 | 96 | 23,500 |
| RTX 3080 | 129 | 31,600 |
| RTX 4060 Ti | 129 | 31,400 |
| RTX 4070 SUPER | 166 | 40,400 |
| RTX 5070 Ti | 305 | 74,500 |

## Settings

Install the package with your platform's guide, then use these values.

### Pools

| Pool | Mode | `-pool` on Linux and Windows | Pool URL on HiveOS |
| --- | --- | --- | --- |
| [AriaPool](https://pool.ariabrain.com/vrl.html) | shared (PPLNS, 2%) | `vrl.ariabrain.com:3354` | `vrl.ariabrain.com:3354` |
| AriaPool | solo (0%) | `vrl.ariabrain.com:3355` | `vrl.ariabrain.com:3355` |
| [NurseryPool](https://vearl.nurserypool.com/) | shared (PPLNS, 2%) | `vearl.nurserypool.com:3367` | `vearl.nurserypool.com:3367` |
| NurseryPool | solo (0%) | `vearl.nurserypool.com:3366` | `vearl.nurserypool.com:3366` |

The wallet is your Vearl address (`vrl1...`). The pools need no registration and no password.

### HiveOS flight sheet

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.4.0/fear-miner-1.4.0.tar.gz` |
| Hash algorithm | `vearl` |
| Wallet and worker template | `%WAL%.%WORKER_NAME%` |
| Pool URL | `vrl.ariabrain.com:3354` |
| Password | `x` |
| Extra config arguments | empty |

Install guide: [HiveOS](../../docs/en/hiveos.md).

### start-vearl.sh (Linux) and start-vearl.bat (Windows)

The pool line is already filled in. Put your address in `-wallet`.

| What | Value |
| --- | --- |
| `-wallet` | Your Vearl address (`vrl1...`) |
| `-worker` | A name for this rig on the pool: 1 to 32 letters, digits, `.`, `_` or `-` |
| `-pool` | `vrl.ariabrain.com:3354` |

Install guides: [Linux](../../docs/en/linux.md) · [Windows](../../docs/en/windows.md).

### Solo

Point `-pool` (on HiveOS, Pool URL) at a pool's solo port: `vrl.ariabrain.com:3355` or
`vearl.nurserypool.com:3366`. A block you find is paid to your address whole, and its testnet
points are yours. A solo block is rare on one rig; the shared port pays steadily.

Solo on your own Vearl node is not available: the node mines by itself and takes no outside
miner. `-node` is refused with a message that names the solo ports.

### Your testnet points

The pools sign receipts of your work every minute. fear-miner checks each one and keeps it in
`vearl/receipts.jsonl` next to the miner (on HiveOS, `/var/lib/fear-miner/vearl/receipts.jsonl`).
Keep that file: it is your proof if a pool credits you less than it signed. The pool's page
shows the points of your address, and the miner shows them on its screen.

## Vearl options

Coin options take two hyphens. On HiveOS they go in Extra config arguments.

| Option | What it does |
| --- | --- |
| `--receipts FILE` | Keeps the pool's receipts in this file instead of the default. |

## Troubleshooting

| What you see | What to do |
| --- | --- |
| `no NVIDIA GPU of compute capability 8.0 or newer` | The card is older than RTX 30. Vearl cannot use it. |
| `payout address` errors | The wallet must be a `vrl1...` address, with `.worker` after it if you want a worker name. |
| Shares counted as stale right after a block | Normal: a new block makes the previous one's shares late. |

General problems: [troubleshooting](../../docs/en/troubleshooting.md).

## Help

- [Discord](https://discord.gg/uK93NPAhbd)
- [Open an issue](https://github.com/fearke85/fear-miner/issues/new/choose) and attach `log.txt`
