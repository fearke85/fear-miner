# Keryx

**English** · [Português (Brasil)](README.pt-BR.md) · [All coins](../../README.md)

Mining Keryx with fear-miner. Algorithm: `keryxhash`.

> [!WARNING]
> **The H16 hard fork** activates at DAA 147,000,000 (2026-11-07, around 14:00 UTC). From then on
> versions before 1.6.0 are invalid: the network rejects their shares and blocks. Solo miners need
> keryx-node 1.6.7 or newer.

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
| 8-11 GB | 0 | ~6.7 GB |
| 12 GB | 1 | ~8.5 GB |
| 16-20 GB | 2 | ~10 GB |
| 24 GB | 3 | ~17 GB |
| 32 GB or more | 4 | ~30 GB |

Each AI answer is also kept on disk for 12 hours, tens of MB per answer, so leave a few GB free
beyond the model on a rig that answers many requests.

With a monitor attached, what the desktop takes does not count, and a card near the edge may
mine one tier lower.

## Settings

Install the package with your platform's guide, then use these values.

### HiveOS flight sheet

| Field | Value |
| --- | --- |
| Miner name | `fear-miner` |
| Installation URL | `https://github.com/fearke85/fear-miner/releases/download/v1.6.5/fear-miner-1.6.5.tar.gz` |
| Hash algorithm | `keryxhash` |
| Wallet and worker template | Pool: `%WAL%.%WORKER_NAME%`. Solo: `%WAL%` |
| Pool URL | Pool: `stratum+tcp://krx.suprnova.cc:4404`, or `stratum+ssl://krx.cryo-pool.com:5555`. Solo: `grpc://IP:PORT` of your node |
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

### Pools

| Pool | Address | Transport |
| --- | --- | --- |
| Suprnova | `krx.suprnova.cc:4404` (EU), `stratum-us.suprnova.cc:4404` (US) | plain; `stratum+ssl://krx.suprnova.cc:4405` also works |
| Cryo Pool | `krx.cryo-pool.com:5555` | encrypted only: `stratum+ssl://krx.cryo-pool.com:5555` |

`-pool` takes a bare `host:port` or a stratum URL; `stratum+ssl://` (or `stratum+tls://`) wraps
the connection in TLS. The miner checks the pool's certificate, so an address without a valid
certificate does not connect. The same wallet and worker work on both pools; each one has its own
dashboard. On HiveOS, put the full URL in the Pool URL field.

Install guides: [Linux](../../docs/en/linux.md) · [Windows](../../docs/en/windows.md).

## AI requests

Keryx sends AI requests to the miners of each tier, and every miner of that tier has to answer
them in time. The miner answers them by itself while it mines. A request your rig does not answer
counts as a strike against your payout address: keep the miner running and the cards stable, and
check `log.txt`. More in [troubleshooting](docs/en/troubleshooting.md).

Since H15 the network gives far less time to answer. A request that arrives while the model is
not loaded may be answered late.

The miner's screen shows **AI processed**, the answers your pool or node accepted, and in solo
**AI paid**, the AI rewards the network paid to your wallet and their KRX. A reward arrives about
12 hours after its answer; one that arrives while the miner is stopped is paid but not counted.
Both counts are kept per wallet across restarts. Rigs that mine to the same wallet each count all
of that wallet's rewards.

## More

- [Solo mining](docs/en/solo.md)
- [Keryx options](docs/en/options.md) (after `--`)
- [Keryx troubleshooting](docs/en/troubleshooting.md)
- [Miner options and general troubleshooting](../../docs/en/options.md)
