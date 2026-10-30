# Linux

**English** · [Português (Brasil)](../pt-BR/linux.md) · [Back to README](../../README.md)

How to install fear-miner on a plain Linux machine, outside HiveOS, for any coin. The values for
your coin are on its page: [Keryx](../../coins/keryx/README.md#start-keryxsh-linux-and-start-keryxbat-windows), [Vela](../../coins/vela/README.md#start-velash-linux-and-start-velabat-windows), [Numen](../../coins/numen/README.md#start-numensh-linux-and-start-numenbat-windows).

## Before you start

- x86-64 Linux with glibc 2.35 or newer (Ubuntu 22.04, Debian 12 and newer).
- NVIDIA driver 580 or newer. Check with `nvidia-smi`. The package brings the CUDA libraries.
- A card your coin supports, and the free disk your coin's page asks for, next to the miner.

## Install

```
wget https://github.com/fearke85/fear-miner/releases/download/v1.5.1/fear-miner-linux-1.5.1.tar.gz
tar -xzf fear-miner-linux-1.5.1.tar.gz
cd fear-miner
nano start-keryx.sh        # Vela: start-vela.sh
```

## Settings in the start script

Each coin has its own script: `start-keryx.sh` for Keryx, `start-vela.sh` for Vela, `start-numen.sh` for Numen. Leave one line
uncommented, the pool line or the solo line, and put your address in `-wallet`. The pool, the node and the other
values are on your coin's page.

Other options go on that same line. Miner options: [options.md](options.md).

## Run

```
./start-keryx.sh           # Vela: ./start-vela.sh
```

To keep the miner running after you log out, start it in `screen` or `tmux`, or as a systemd
service.

### With sudo

The overclock flags (`-cclock`, `-mclock`, `-lock-cclock`, `-lock-mclock`, `-fan`) need root:

```
sudo ./start-keryx.sh      # Vela: sudo ./start-vela.sh
```

Started with `sudo` or `su` from your own login, the miner creates its files (`keryx`, `vela`,
`log.txt`) as the owner of the miner folder, so you can still edit and delete them. It also gives
back what an earlier root run left there. A systemd service or a root login keeps root's files; to
take them back, run `sudo chown -R "$USER": .` in the miner folder.

## Update to a new version

Unpack the new archive over the old folder, then copy your line into the new start script.
What the miner keeps is in `./keryx` (Vela: `./vela`) and stays. An older `./data` is picked up from there.

## Where things are

| What | Where |
| --- | --- |
| Log with warnings, errors and crash reports | `log.txt` next to the miner |
| Data the miner keeps | `./keryx` (`models/`, and `escrow/<wallet>/`), `./vela` (`models/`). Set `FEAR_DATA_DIR` to move it |
| Hashrate and shares | `curl 127.0.0.1:4060/stats` |
