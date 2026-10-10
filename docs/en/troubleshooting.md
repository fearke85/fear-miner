# Troubleshooting

**English** · [Português (Brasil)](../pt-BR/troubleshooting.md) · [Back to README](../../README.md)

Start with `log.txt`: `/var/lib/fear-miner/log.txt` on HiveOS, next to the miner on Linux and
Windows. It keeps warnings, errors, why the miner stopped, one line per AI request, and a crash
report after a crash. Each line carries the miner version.

## Shares are rejected since 2026-10-09

Versions before 0.0.22 are invalid since the H14 hard fork. Install the
[current version](../../README.md). Solo: update your node to keryx-node 1.6.4 or newer.

## HiveOS keeps running an old version

The version is in the Installation URL file name. Change both places in the URL
(`v0.0.XX` and `fear-miner-0.0.XX.tar.gz`) and apply the flight sheet.

## "no CUDA device"

The message says which case applies:

- cards disabled in HiveOS (disabled in the rig settings, or power limit 1 in the OC profile);
- cards too old for the driver or for this miner (Pascal and older are not supported);
- a driver update that needs a reboot.

## "no device fits a tier"

The message lists each card's memory and what the smallest tier needs.

- Cards under 8 GB need another card on the rig that can answer tier 0, and 2 GB of free RAM.
- On Linux or Windows, a monitor and open programs take card memory. Close them, or use a rig
  with no monitor and `--headless`.
- Remove a `--tier` that asks more than the cards can give.

## Not enough disk

The miner checks the disk before it downloads and says what it needs, for example
`it needs 10.1 GB free in /var/lib/fear-miner/models/..., 4.1 GB available`. Free space, or move
the models with `--models-dir` (HiveOS) or `FEAR_DATA_DIR` (Linux, Windows). Sizes per tier are in
the [README](../../README.md#which-tier-does-my-card-mine). An interrupted download continues where
it stopped.

## A card is named as stuck while loading

A log line names the card and its PCI address and ends with `Reseat or swap its riser`. The other
cards keep mining. Reseat or replace that card's riser or cable.

## The miner restarted after a crash

The next start writes a crash report into `log.txt`: the card, its overclock offsets, temperature,
power, PCIe link, the GPU errors the system logged, and the likeliest cause. The most common fix is
a lower memory or core overclock on that card. A card that crashes while answering AI requests
keeps mining but is kept off AI requests for a while, and the other cards answer them.

## Strikes or `MISSED` lines

Each AI request has a line in `log.txt`, and a `MISSED` line names the step a request was stuck in
when its time ran out. Common causes: a card that crashed, a slow disk or little RAM, a rig
restarted in the middle of a request. Send the log on Discord if strikes continue.

## Low hashrate on a card

- A card on a narrow PCIe link (x1 riser) that mines a tier larger than its memory reaches its
  hashrate about two minutes after start. A faster link gives it more hashrate.
- Compare with other cards of the same model on the [Discord](https://discord.gg/uK93NPAhbd).

## Asking for help

Ask on [Discord](https://discord.gg/uK93NPAhbd) or
[open an issue](https://github.com/fearke85/fear-miner/issues/new/choose). Include the miner
version, the platform, your cards, pool or solo, and attach `log.txt`.
