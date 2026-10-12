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
- 6 GB cards mine tier 0 next to another card on the same rig, with 2 GB of RAM free at start.
- Pascal (GTX 10xx, P104/P106) and older are not supported.

## Which tier does my card mine?

The miner picks the highest tier each card supports by itself. You do not need `--tier`.

Free disk each tier needs for its model download:

| Tier | Free disk |
| --- | --- |
| 0 | ~6.7 GB |
| 1 | ~8.5 GB |
| 2 | ~10 GB |
| 3 | ~17 GB |
| 4 | ~30 GB |

## Settings

Install the package with your platform's guide, then use these values.

### HiveOS flight sheet

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.0.1/fear-miner-1.0.1.tar.gz` |
| Hash algorithm | `keryxhash` |
| Wallet and worker template | Pool: `%WAL%.%WORKER_NAME%`. Solo: `%WAL%` |
| Pool URL | Pool: `stratum+tcp://krx.suprnova.cc:4404`. Solo: `grpc://IP:PORT` of your node |
| Password | `x`, or the pool password |

The wallet is your Keryx address, `keryx:...`. Install guide: [HiveOS](../../docs/en/hiveos.md).

### run.sh (Linux) and start.bat (Windows)

| Line | Value |
| --- | --- |
| `WALLET` | Your Keryx address, `keryx:...` |
| `WORKER` | A name for this rig on the pool |
| `POOL` | `stratum+tcp://krx.suprnova.cc:4404` |
| `NODE` | Solo only: `grpc://IP:PORT` of your node, with `POOL` empty |
| `ESCROW_CERT` | Solo only, first start: see [solo mining](docs/en/solo.md) |

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
