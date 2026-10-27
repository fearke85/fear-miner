# Numen

**English** · [Português (Brasil)](README.pt-BR.md) · [All coins](../../README.md)

Mining Numen (NUMN) with fear-miner. Algorithm: `numen` (HiveOS calls it `poscan`). Pool mining
on [rplant](https://pool.rplant.xyz), [ninjaraider](https://ninjaraider.com) or
[Nitopool](https://pool.nitopool.online/), solo through rplant or Nitopool, and solo on your own
Numen node.

The miner shows its speed in MH/s.

## Cards

- NVIDIA Turing or newer (RTX 20xx, 30xx, 40xx, 50xx).
- Pascal (GTX 10xx) and older are not supported.

Measured with fear-miner on a HiveOS rig, at the core lock that rig uses (RTX 30 at 1500 MHz,
RTX 5070 Ti at 2300 MHz):

| Card | MH/s |
| --- | --- |
| RTX 3060 | 0.34 |
| RTX 3070 | 0.55 |
| RTX 3080 | 0.81 |
| RTX 5070 Ti | 1.30 |

Numen's speed follows the core clock: a higher core lock gives more MH/s and draws more watts.

## Settings

Install the package with your platform's guide, then use these values.

### Pools

| Pool | `-pool` on Linux and Windows | Pool URL on HiveOS |
| --- | --- | --- |
| [rplant](https://pool.rplant.xyz), Europe | `eu.rplant.xyz:7189` | `stratum+tcp://eu.rplant.xyz:7189` |
| rplant, North America | `na.rplant.xyz:7189` | `stratum+tcp://na.rplant.xyz:7189` |
| rplant, Asia | `asia.rplant.xyz:7189` | `stratum+tcp://asia.rplant.xyz:7189` |
| [ninjaraider](https://ninjaraider.com) | `numen.ninjaraider.com:44960` | `stratum+tcp://numen.ninjaraider.com:44960` |
| [Nitopool](https://pool.nitopool.online/) | `numn.stratum.nitopool.online:3028` | `stratum+tcp://numn.stratum.nitopool.online:3028` |
| Nitopool, farms | `numn.stratum.nitopool.online:3029` | `stratum+tcp://numn.stratum.nitopool.online:3029` |

Pick the rplant region closest to the rig: a slow link turns late shares into stale ones.
Nitopool's shared mode is PPLNS at a 0.9% fee; its farm port starts at a share difficulty eight
times higher, for rigs with many cards.

### HiveOS flight sheet

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.4.3/fear-miner-1.4.3.tar.gz` |
| Hash algorithm | `poscan` |
| Wallet and worker template | `%WAL%.%WORKER_NAME%` |
| Pool URL | `stratum+tcp://eu.rplant.xyz:7189` |
| Password | `x` (or `m=solo`, see below) |
| Extra config arguments | empty |

The wallet is your Numen address. Install guide: [HiveOS](../../docs/en/hiveos.md).

### start-numen.sh (Linux) and start-numen.bat (Windows)

The pool line is already filled in. Put your address in `-wallet`.

| What | Value |
| --- | --- |
| `-wallet` | Your Numen address |
| `-worker` | A name for this rig on the pool |
| `-pool` | `eu.rplant.xyz:7189` |

Install guides: [Linux](../../docs/en/linux.md) · [Windows](../../docs/en/windows.md).

### Solo through rplant

rplant mines solo on the same stratum: put `m=solo` in the password. A block you find is paid to
you whole, at rplant's solo fee (2%, against 1% in shared mode).

| Where | Value |
| --- | --- |
| Linux and Windows | `-password m=solo` |
| HiveOS | Password field: `m=solo` |

rplant's other password options go on the same line, separated by commas: `m=solo,d=200000`
sets a fixed share difficulty.

### Solo through Nitopool

Nitopool mines solo on its own ports: `numn.stratum.nitopool.online:3024`, or `numn.stratum.nitopool.online:3026` for a farm. A block you find is
paid to you whole, at Nitopool's 0.9% fee. On HiveOS, put `stratum+tcp://numn.stratum.nitopool.online:3024` in Pool URL;
the password stays `x`.

### Solo on your own node

```
./fear-miner -coin numen -node ws://127.0.0.1:9944
```

The node pays the block to the mining account set on the node, not to `-wallet`. `-node` takes
the place of `-pool`; do not pass both. On HiveOS, put the node in Pool URL:
`ws://NODE_IP:9944`.

## Numen options

Coin options take two hyphens. On HiveOS they go in Extra config arguments.

| Option | What it does |
| --- | --- |
| `--block 128` or `--block 256` | Skips the first start's choice between the two and uses this one. |
| `--kernel exact` | A much slower scan, for checking results. The default, `fast`, is the one to mine with. |

The first start measures the card for a few seconds and remembers the result.

## Not yet

- rplant's TLS port.

## Troubleshooting

| What you see | What to do |
| --- | --- |
| Shares rejected as `stale share` | Some are normal: jobs change every few seconds. Many mean a slow link; pick a closer rplant region. |
| Shares rejected as `invalid PoScan work` on Nitopool | A few are normal: Nitopool reports a share that arrived after its job changed this way. Many mean a slow link to the pool. |
| `pass -pool or -node, not both` | Keep one of them. |

General problems: [troubleshooting](../../docs/en/troubleshooting.md).

## Help

- [Discord](https://discord.gg/uK93NPAhbd)
- [Open an issue](https://github.com/fearke85/fear-miner/issues/new/choose) and attach `log.txt`
