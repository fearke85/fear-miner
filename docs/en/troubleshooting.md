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

On Windows, `start-keryx.bat` starts the miner again after such a crash. A `start-keryx.bat` from
an older release stops at `Press any key to continue` instead: copy your line into the new one.

## "Permission denied" on the miner's files or folders

- **Linux, files owned by root:** a miner started with `sudo` before 1.2.1 left `keryx`, the escrow
  folder and `log.txt` owned by root. Start this version once with `sudo` from your own login: it
  gives them back to the owner of the miner folder. A systemd service or a root login keeps root's
  files; run `sudo chown -R "$USER": .` in the miner folder. More in
  [Linux, with sudo](linux.md#with-sudo).
- **HiveOS or another root run, `Failed to create escrow key directory ... Permission denied`:**
  1.2.1 stopped like this when the miner folder belonged to a regular user. Fixed in 1.3.0:
  update the miner.

## Asking for help

Ask on [Discord](https://discord.gg/uK93NPAhbd) or
[open an issue](https://github.com/fearke85/fear-miner/issues/new/choose). Include the miner
version, the platform, the coin, your cards, pool or solo, and attach `log.txt`.
