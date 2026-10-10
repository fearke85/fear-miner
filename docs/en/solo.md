# Solo mining

**English** · [Português (Brasil)](../pt-BR/solo.md) · [Back to README](../../README.md)

Solo mining sends blocks to your own Keryx node instead of a pool.

## What you need

- A synced Keryx node, **keryx-node 1.6.4 or newer** (required since H14), with its gRPC port
  reachable from the rig.
- Your wallet, to authorise the rig once.

## Point the miner at your node

| Platform | Setting |
| --- | --- |
| HiveOS | Pool URL `grpc://IP:PORT`, wallet template `%WAL%` |
| Linux | `NODE="grpc://IP:PORT"` and `POOL=""` in `run.sh` |
| Windows | `set "NODE=grpc://IP:PORT"` and `set "POOL="` in `start.bat` |

Example: `grpc://192.168.1.20:22110`. Use `grpc://`, not `http://` and not a bare `IP:PORT`.

## Authorise the rig (first start only)

1. Start the miner. Its log prints `Escrow key to authorise in your wallet: ...`.
2. In your wallet, open **Authorise a miner** and paste that key. The wallet returns a line of
   128 hex characters: the escrow cert.
3. Give the cert to the miner and start it again:
   - HiveOS, Extra config arguments: `-- --escrow-cert PASTE_THE_128_HEX_CHARS`
   - Linux: `ESCROW_CERT="..."` in `run.sh`
   - Windows: `set "ESCROW_CERT=..."` in `start.bat`

That start saves the cert. Later starts load it, so you can remove it from the settings.

The cert belongs to one wallet address and to this rig's escrow key. If you change the wallet,
authorise the rig again. Keep the escrow files when you reinstall or move the miner:

| Platform | Escrow files |
| --- | --- |
| HiveOS | `/var/lib/fear-miner` |
| Linux, Windows | `data` next to the miner |

## AI requests and strikes

The network sends AI requests to the miners of each tier, and every miner of that tier has to
answer them in time. A request your rig does not answer counts as a strike against your payout
address. The miner answers them by itself. Keep it running, keep the cards stable, and check
`log.txt`: each request has a line there, and a `MISSED` line says why one was late.

If you run several rigs on one payout address, every tier any of them mines must be answered by at
least one of them.

## Pool rigs and escrow

A pool rig can claim its matured escrow through a node while it keeps mining on the pool: add
`-- --escrow-claim grpc://IP:PORT` (HiveOS) or `--escrow-claim grpc://IP:PORT` in `EXTRA`.
