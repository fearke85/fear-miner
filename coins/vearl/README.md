# Vearl

**English** · [Português (Brasil)](README.pt-BR.md) · [All coins](../../README.md)

Mining Vearl (VRL) on its public testnet with fear-miner. Algorithm: `vearl`. Pool mining on
[AriaPool](https://pool.ariabrain.com/vrl.html), [NurseryPool](https://vearl.nurserypool.com/) or
the [Vearl pool](https://pool.vearl.org/), and solo through any of them on its solo port.

The testnet coins have no value. Its rewards program counts points per block; the rules and the
registration are on [vearl.org](https://vearl.org/participate/).

The miner shows its speed in **sigmas per second** (`sigma/s`), the unit the pools show, and its
efficiency in `sigma/J`. HiveOS knows hash units only and shows the same number as H/s. One sigma
is 4096 tile attempts, so the official miner's MH/s is sigma/s × 4096 / 1,000,000.

## Cards

- NVIDIA Ampere or newer (RTX 30xx, 40xx, 50xx).
- Turing with tensor cores (RTX 20xx, CMP 40HX, CMP 50HX, T4).
- GTX 16xx and CMP 30HX are the same generation and have no tensor cores, so Vearl cannot use them. Older cards cannot either.

Measured with fear-miner at each rig's overclock (RTX 30 on a HiveOS rig, RTX 40 on another,
RTX 5070 Ti on a desktop at stock clocks):

| Card | sigma/s | official miner MH/s |
| --- | --- | --- |
| RTX 3060 | 22,300 | 91 |
| RTX 3070 | 35,300 | 145 |
| RTX 3080 | 45,900 | 188 |
| RTX 4060 Ti | 31,400 | 129 |
| RTX 4070 SUPER | 40,400 | 166 |
| RTX 5070 Ti | 108,100 | 443 |

A CMP 50HX at a 200 W limit, with no overclock, does 19,300 sigma/s (79 MH/s).

## Settings

Install the package with your platform's guide, then use these values.

### Pools

| Pool | Mode | `-pool` on Linux and Windows | Pool URL on HiveOS |
| --- | --- | --- | --- |
| [AriaPool](https://pool.ariabrain.com/vrl.html) | shared (PPLNS, 2%) | `vrl.ariabrain.com:3354` | `vrl.ariabrain.com:3354` |
| AriaPool | solo (0%) | `vrl.ariabrain.com:3355` | `vrl.ariabrain.com:3355` |
| [NurseryPool](https://vearl.nurserypool.com/) | shared (PPLNS, 2%) | `vearl.nurserypool.com:3367` | `vearl.nurserypool.com:3367` |
| NurseryPool | solo (0%) | `vearl.nurserypool.com:3366` | `vearl.nurserypool.com:3366` |
| [Vearl pool](https://pool.vearl.org/) | shared (PPLNS, 1%) | `pool.vearl.org:3333` | `pool.vearl.org:3333` |
| Vearl pool | solo (1%) | `pool.vearl.org:3366` | `pool.vearl.org:3366` |

The wallet is your Vearl address (`vrl1...`). The pools need no registration and no password.

### HiveOS flight sheet

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.5.2/fear-miner-1.5.2.tar.gz` |
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

Point `-pool` (on HiveOS, Pool URL) at a pool's solo port: `vrl.ariabrain.com:3355`,
`vearl.nurserypool.com:3366` or `pool.vearl.org:3366`. A block you find is paid to your address whole, and its testnet
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
| `no NVIDIA GPU that can run Vearl` | The card is older than RTX 20, or it is a GTX 16xx / CMP 30HX (no tensor cores). |
| `payout address` errors | The wallet must be a `vrl1...` address, with `.worker` after it if you want a worker name. |
| Shares counted as stale right after a block | Normal: a new block makes the previous one's shares late. |

General problems: [troubleshooting](../../docs/en/troubleshooting.md).

## Help

- [Discord](https://discord.gg/uK93NPAhbd)
- [Open an issue](https://github.com/fearke85/fear-miner/issues/new/choose) and attach `log.txt`
