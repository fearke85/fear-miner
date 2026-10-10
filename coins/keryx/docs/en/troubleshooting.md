# Keryx troubleshooting

**English** · [Português (Brasil)](../pt-BR/troubleshooting.md) · [Back to Keryx](../../README.md)

Problems specific to Keryx. Problems that can happen with any coin (old version on HiveOS, "no
CUDA device", risers, crashes from overclock) are in the
[general troubleshooting](../../../../docs/en/troubleshooting.md).

## Shares are rejected since 2026-10-09

Versions before 0.0.22 are invalid since the H14 hard fork. Install the
[current version](../../../../README.md). Solo: update your node to keryx-node 1.6.4 or newer.

## "no device fits a tier"

The message lists each card's memory and what the smallest tier needs.

- Cards under 8 GB need another card on the rig that can answer tier 0, and 2 GB of free RAM.
- Pascal (GTX 10xx, P104/P106) and older are not supported.
- On Linux or Windows, a monitor and open programs take card memory. Close them, or use a rig
  with no monitor and `--headless`.
- Remove a `--tier` that asks more than the cards can give.

## Not enough disk

The miner checks the disk before it downloads the model and says what it needs, for example
`it needs 10.1 GB free in /var/lib/fear-miner/models/..., 4.1 GB available`. Free space, or move
the models with `--models-dir`. Sizes per tier are on the [Keryx page](../../README.md#which-tier-does-my-card-mine).
An interrupted download continues where it stopped.

## Strikes or `MISSED` lines

Each AI request has a line in `log.txt`, and a `MISSED` line names the step a request was stuck in
when its time ran out. Common causes: a card that crashed, a slow disk or little RAM, a rig
restarted in the middle of a request. Send the log on [Discord](https://discord.gg/uK93NPAhbd) if
strikes continue.

A card that crashes while answering AI requests keeps mining but is kept off AI requests for a
while, and the other cards answer them. The crash report in `log.txt` names the card.

## Low hashrate on a card

- A card on a narrow PCIe link (x1 riser) that mines a tier larger than its memory reaches its
  hashrate about two minutes after start. A faster link gives it more hashrate.
- Compare with other cards of the same model on [Discord](https://discord.gg/uK93NPAhbd).
