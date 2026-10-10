# Troubleshooting

**English** · [Português (Brasil)](../pt-BR/troubleshooting.md) · [Back to README](../../README.md)

Problems that can happen with any coin. Problems of one coin are on its page:
[Keryx](../../coins/keryx/docs/en/troubleshooting.md).

Start with `log.txt`: `/var/lib/fear-miner/log.txt` on HiveOS, next to the miner on Linux and
Windows. It keeps warnings, errors, why the miner stopped, and a crash report after a crash. Each
line carries the miner version.

## HiveOS keeps running an old version

The version is in the Installation URL file name. Change both places in the URL
(`v0.0.XX` and `fear-miner-0.0.XX.tar.gz`) and apply the flight sheet.

## "no CUDA device"

The message says which case applies:

- cards disabled in HiveOS (disabled in the rig settings, or power limit 1 in the OC profile);
- cards too old for the driver or for this miner;
- a driver update that needs a reboot.

## A card is named as stuck while loading

A log line names the card and its PCI address and ends with `Reseat or swap its riser`. The other
cards keep mining. Reseat or replace that card's riser or cable.

## The miner restarted after a crash

The next start writes a crash report into `log.txt`: the card, its overclock offsets, temperature,
power, PCIe link, the GPU errors the system logged, and the likeliest cause. The most common fix is
a lower memory or core overclock on that card. Juliano Caju's
[overclock table](https://www.julianocaju.com.br/en/overclocks/) lists settings per card and coin.

## Asking for help

Ask on [Discord](https://discord.gg/uK93NPAhbd) or
[open an issue](https://github.com/fearke85/fear-miner/issues/new/choose). Include the miner
version, the platform, the coin, your cards, pool or solo, and attach `log.txt`.
