# Keryx

**English** · [Português (Brasil)](README.pt-BR.md) · [All coins](../../README.md)

Mining Keryx with fear-miner. Algorithm: `keryxhash`.

> [!WARNING]
> **The H14 hard fork is live** (DAA 121,985,000, 2026-10-09). Versions before 0.0.22 are
> invalid: the network rejects their shares and blocks. Solo miners need keryx-node 1.6.4 or newer.

## Cards

- NVIDIA Turing or newer (RTX 20xx, 30xx, 40xx, 50xx) with 8 GB or more.
- NVIDIA CMP 170HX, including cards unlocked to 64 GB, which mine tier 4. Measured: ~3.2 MH/s per
  card at a 200 W power limit.
- Cards with 6 GB or less are not supported.
- Pascal (GTX 10xx, P104/P106) and older are not supported.

## Which tier does my card mine?

Each card mines the highest tier whose model fits in its memory with room left to answer that
tier's AI requests. You do not need `--tier`.

| Card memory | Tier | Free disk for the model |
| --- | --- | --- |
| 8 GB | 0 | ~6.7 GB |
| 10-11 GB | 1 | ~8.5 GB |
| 12-16 GB | 2 | ~10 GB |
| 20-24 GB | 3 | ~17 GB |
| 32 GB or more | 4 | ~30 GB |

With a monitor attached, what the desktop takes does not count, and a card near the edge may
mine one tier lower.

## Settings

Install the package with your platform's guide, then use these values.

### HiveOS flight sheet

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.3.0/fear-miner-1.3.0.tar.gz` |
| Hash algorithm | `keryxhash` |
| Wallet and worker template | Pool: `%WAL%.%WORKER_NAME%`. Solo: `%WAL%` |
| Pool URL | Pool: `stratum+tcp://krx.suprnova.cc:4404`. Solo: `grpc://IP:PORT` of your node |
| Password | `x`, or the pool password |

The wallet is your Keryx address, `keryx:...`. Install guide: [HiveOS](../../docs/en/hiveos.md).

### start-keryx.sh (Linux) and start-keryx.bat (Windows)

The pool line is already filled in. Put your address in `-wallet`. For solo, comment the pool
line and uncomment the solo line.

| What | Value |
| --- | --- |
| `-wallet` | Your Keryx address, `keryx:...` |
| `-worker` | A name for this rig on the pool |
| `-pool` | `krx.suprnova.cc:4404` |
| `-node` | Solo only: `grpc://IP:PORT` of your node |
| `--escrow-cert` | Solo only, first start: see [solo mining](docs/en/solo.md) |

Install guides: [Linux](../../docs/en/linux.md) · [Windows](../../docs/en/windows.md).

## AI requests

Keryx sends AI requests to the miners of each tier, and every miner of that tier has to answer
them in time. The miner answers them by itself while it mines. A request your rig does not answer
counts as a strike against your payout address: keep the miner running and the cards stable, and
check `log.txt`. More in [troubleshooting](docs/en/troubleshooting.md).

## More

- [Solo mining](docs/en/solo.md)
- [Keryx options](docs/en/options.md) (after `--`)
- [Keryx troubleshooting](docs/en/troubleshooting.md)
- [Miner options and general troubleshooting](../../docs/en/options.md)
