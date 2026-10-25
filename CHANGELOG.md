# Changelog

What changed in each version, newest first. One version of fear-miner covers every coin; a change
for one coin names it. Before 1.3.0, every change listed is for Keryx.

Keryx: versions before 0.0.22 are invalid since the H14 hard fork (2026-10-09) and are not listed.

## 1.4.2 (2026-10-25)

Vearl is much faster on RTX 30 and faster on RTX 50, at the same overclock, and Vearl and Numen
get a new pool each. This is the first full release since 1.3.2: the 1.4.1 and 1.4.0 test
versions below are part of it.

- **Faster Vearl on RTX 30: about +40% sigma/s** at the same overclock. Measured on a HiveOS
  rig at its overclock, against 1.4.1: 3060 15.7k -> 22.3k sigma/s, 3070 24.7k -> 35.3k, 3080
  33.3k -> 45.9k (39.2k on a 3080 that its power limit holds back).
- **Faster Vearl on RTX 50: about +15 to +20%.** The same rig's 5070 Ti cards: 87.5k -> 105.0k
  sigma/s. A 5070 Ti at stock clocks: 94.4k -> 108.1k, at about 290 W instead of 299.
- The 7-card rig as a whole: 298k -> 375k sigma/s (+26%), every share accepted. RTX 40 cards run
  as in 1.4.1.
- **New pool, Vearl:** the [Vearl pool](https://pool.vearl.org/), shared on
  `pool.vearl.org:3333` (PPLNS, 1%) and solo on `pool.vearl.org:3366` (1%).
- **New pool, Numen:** [Nitopool](https://pool.nitopool.online/), shared on
  `numn.stratum.nitopool.online:3028` (PPLNS, 0.9%; 3029 for farms) and solo on port 3024 (3026
  for farms). Nitopool answers a share that arrives after its job changed with `invalid PoScan
  work`; a few of those are normal.
- No new flags.

## 1.4.1 (2026-10-24)

- **Faster Vearl:** about **+19%** sigma/s on RTX 50 cards with **+5 to +15%** sigma/J (a new tile
  kernel for them), and about **+4.5%** on RTX 30 with +1 to +2.5% sigma/J, at the same overclock.
  Measured on a HiveOS rig at its overclock: 3060 14.9k -> 15.6k sigma/s, 3070 23.2k -> 24.5k,
  3080 29.0k -> 30.0k, 5070 Ti 56.5k -> 67.1k; on a 5070 Ti at stock clocks, 73.0k -> 83.8k at the
  same 291 W. On RTX 50 the noise now runs inside that kernel too: another **+8 to +9%** sigma/s
  with **+24%** sigma/J on the rig's 5070 Ti cards (80k -> 87k sigma/s, 238 -> 208 W), and
  **+11%** at stock clocks (85.1k -> 94.4k at 299 W); RTX 30 +0.7%.
- **Vearl shows sigma/s, the pools' unit,** instead of MH/s, and its efficiency in sigma/J.
  HiveOS shows the same number as H/s, as it does for Vela. One sigma is 4096 tile attempts:
  305 MH/s is 74,500 sigma/s.
- **Vearl gives the CPU back:** the miner used one CPU core at 100% per card while it mined
  Vearl, which raised the load average with the card count. It now uses about 12% of a core per
  card, at the same sigma/s (measured on a 5070 Ti: 94.5k sigma/s either way, CPU 100% -> 12%).

## 1.4.0 (2026-10-23)

- **New coin, Vearl (VRL) public testnet:** pool mining on AriaPool and NurseryPool, and solo
  through their solo ports. RTX 30, 40 and 50 cards. On HiveOS, pick the Hash algorithm `vearl`
  and put the pool as `HOST:PORT` in Pool URL. The miner keeps the pools' signed receipts of
  your work, the proof of your testnet points. The Linux and Windows packages get a
  `start-vearl` script. Settings and rates per card: [coins/vearl](coins/vearl/README.md).
  Measured on the same RTX 5070 Ti: 305 MH/s, against 253 for the official testnet miner
  (0.1.0-rc23).
- **HiveOS:** a Pool URL written as a bare `HOST:PORT` is taken as a pool.
- **New coin, Numen (NUMN):** pool mining on rplant (Europe, North America, Asia) and
  ninjaraider, solo through rplant with the password `m=solo`, and solo on your own node with
  `-node ws://...`. On HiveOS, pick the Hash algorithm `poscan`. The Linux and Windows packages
  get a `start-numen` script. Settings and rates per card: [coins/numen](coins/numen/README.md).
- **Faster, Vela:** about +4% inf/s on RTX 20, 30 and 40 cards and about +6.7% on the RTX
  5070 Ti, with better inf/J, at the same overclock. Measured at each rig's overclock:
  - a 7-card HiveOS rig (RTX 30 at 1500 MHz, 5070 Ti at 2300 MHz): 3060 15.6 -> 16.3 inf/s
    (+4.3%, inf/J +4.2 to +4.4%), 3070 24.5 -> 25.5 (+4.1%, inf/J +4.3%), 3080 36.9 -> 38.5
    (+4.1%, inf/J +3.9 to +4.2%), 5070 Ti 59.8 -> 63.8 (+6.7%, inf/J +5.2 to +5.9%);
  - a HiveOS rig with RTX 40 cards: 4060 Ti at 2415 MHz 25.1 -> 26.1 (+3.8%, inf/J +4.1%),
    4070 SUPER at 1755 MHz 33.2 -> 34.6 (+4.3%, inf/J +4.9%);
  - an RTX 2070 Max-Q laptop at its 80 W limit: 11.0 -> 11.6 (+4.7%, inf/J +5.1%).
- **New, Vela:** mine on [AriaPool](https://pool.ariabrain.com/vela.html) with
  `-pool http://159.69.194.46:3349`; on HiveOS, put the same address in Pool URL. The HiveOS
  Hash algorithm `poi` now means Vela, so `-coin vela` is no longer needed with it.
- **New, Vela:** solo mining on your own Vela node:
  `-node http://RPCUSER:RPCPASSWORD@127.0.0.1:18743 -wallet vela1...`. The block reward goes
  to the wallet.

## 1.3.2 (2026-10-21)

Vela is faster, at the same overclock. Nothing to reconfigure.

- **Faster, Vela:** about +3% inf/s on the RTX 3060, 3070 and 3080, and about +3.3% on the RTX
  5070 Ti, with better inf/J. Measured at a HiveOS overclock: 3060 +3.2%, 3070 +3.0%, 3080
  +3.0%, and a higher inf/J on each. On a 5070 Ti at a 2300 MHz core lock: +3.3% inf/s and
  +1.1% inf/J.
- The speed in the miner and on HiveOS stays steady, instead of jumping from one result to the next. A card that stops reporting still falls to zero.
- On Vela, a card shows the model loading into VRAM.
- No new flags. Replace the package; the flight sheet stays. If this version is already installed, install the package again.

## 1.3.1 (2026-10-20)

A fix for Vela in 1.3.0.

- **Fixed, Vela:** the miner kept one CPU core busy for each card, two on most cards, all the time.
  The CPU now stays idle while the cards work, at the same inf/s. Measured on a 7-card HiveOS
  rig: the load average went from 14.8 to 0.4 and the miner from 14 cores to 15% of one, at
  225 inf/s before and after. Rigs with a small CPU, and HiveOS's load average watchdog, no
  longer see Vela as a CPU load.
- `FEAR_SYNC` is a Keryx setting; Vela does not read it.

## 1.3.0 (2026-10-20)

A second coin, Vela, and a fix for 1.2.1.

- **New coin, Vela** (`-coin vela`; on HiveOS any Hash algorithm and `-coin vela` in Extra config
  arguments, since HiveOS does not list Vela), on the suprnova pool `vela.suprnova.cc:7601`, on
  NVIDIA Turing or newer. The model (1.2 GB) downloads on the first start. Measured at a HiveOS
  overclock: RTX 3060 13.6 inf/s at 78 W, 3070 20.9 at 123 W, 3080 27.6 at 190 W, 5070 Ti 57.8
  at 211 W. The overclock per card, settings and options: [coins/vela](coins/vela/README.md).
- Vela's speed shows in inferences per second (`inf/s`) and its efficiency in `inf/J` in the
  miner's screen and in `/stats`. HiveOS shows the same number as H/s.
- The Linux and Windows packages carry `start-vela.sh` and `start-vela.bat`.
- The Linux package carries one library, `fear-miner-lib.so`; `libgomp.so.1` is gone.
- **Fixed, Linux and HiveOS:** in 1.2.1 a miner run as root (HiveOS, a service, a root login)
  from a folder a regular user owns could not create its escrow key (`Failed to create escrow
  key directory ... Permission denied`). Files now go to the folder's owner only when that user
  started the miner with `sudo` or `su`; other root runs keep root's files.

## 1.2.1 (2026-10-20)

Fixes for 1.2.0.

- **Fixed, Linux with `sudo`:** the overclock flags need root, and a miner started with `sudo`
  left `keryx`, the escrow folder and `log.txt` owned by root, so you could not change them.
  What the miner creates now belongs to whoever owns the miner folder, and the next start with
  `sudo` hands back what an earlier one left as root. HiveOS is unchanged.
- **Fixed, solo:** a busy node that takes several seconds to check each block ended the
  connection after 10 s (`the node stopped reading the stream`), and a block found meanwhile
  could be dropped as `template gone`. The miner now waits for a slow node.
- **Fixed, Windows:** the pool ping and the share round trip show again instead of `rtt ?`.
- **Fixed:** the fan showed 0% on cards whose first fan reports no speed (seen on an RTX 3070).
  It now shows the fastest fan of the card.
- A harmless tokenizer warning when tier 1 loads no longer shows in the log.

## 1.2.0 (2026-10-19)

Overclock from the miner, shorter start lines, and two Windows fixes.

- **Overclock from the miner,** on Linux and Windows: `-cclock` and `-mclock` (core and memory
  offsets in MHz, negative lowers them), `-lock-cclock` and `-lock-mclock` (locked clocks in MHz)
  and `-fan` (percent). One value sets every card. Different cards take a list, one value per card
  in `-device` order, and `*` leaves a card as it is:
  `-device 0,1 -cclock 275,250 -lock-cclock 2610,1350 -fan 75`. Linux needs root, Windows **Run as
  administrator**. On exit the miner puts back what it changed. On HiveOS, use these flags or the
  OC page for a card, not both.
- **Miner flags take one hyphen:** `-coin keryxhash`, `-pool`, `-wallet`, `-worker`, `-device`.
  Coin flags keep two (`--tier`). Older lines with `--pool` or a bare `--` still work.
- **One start line per coin:** `start-keryx.sh` and `start-keryx.bat` hold a pool line and a
  commented solo line. Linux and Windows keep their data in `keryx` next to the miner
  (`FEAR_DATA_DIR` moves it); an older `data` folder is picked up from there.
- **Solo, escrow per wallet:** escrow files now sit under `escrow/<wallet>/` (HiveOS:
  `/var/lib/fear-miner/escrow/<wallet>/`). The first start copies them there and keeps the old
  files, renamed `*.pre-layout`. A second wallet on the same rig gets its own escrow.
- **Fixed, Windows:** an 8 GB card that also drives a monitor (RTX 3070) did not mine. It now
  mines tier 0.
- **Fixed, Windows:** after a card crash the miner starts again by itself instead of stopping at
  `Press any key`. It needs the new `start-keryx.bat`: copy your line into it.

## 1.1.0 (2026-10-19)

Keryx AI requests are answered by cards that keep mining their tier, with nothing to set.

- **Faster answers.** The card that answers a request is ready in under half a second and back to
  mining about a second after the answer. Before, it loaded the model first (~15 s on tier 2)
  and needed ~9 s more before it mined again. Hashrate is the same as 1.0.3.
- **Long prompts read whole.** Every tier reads up to 32,768 tokens of a prompt (4,096 before).
- **New tier ladder:**

  | Tier | Card memory |
  | --- | --- |
  | 0 | 8 GB |
  | 1 | 10-11 GB |
  | 2 | 12-16 GB |
  | 3 | 20-24 GB |
  | 4 | 32 GB or more |

- **`--tier` above a card's size:** the card mines the forced tier when that tier's model fits in
  its memory; otherwise it mines the tier its memory holds. The log says which tier each card
  mines.
- **Cards with 6 GB or less are not supported.**
- **Fixed, low-end rigs (Celeron, 4 GB of RAM, USB stick):** HiveOS rebooted them for a high load
  average a few minutes after every start, even with its watchdog off. Measured on a rig limited
  to 2 cores, 4 GB and a USB stick's speed: load average 180 and a reboot before, at most 4 now,
  with every share accepted.
- **Fixed, solo:** a rig whose node stopped answering could stay at 0 H/s for good. It now
  reconnects.
- **Fixed, solo:** a block found around the dev-fee minute could be dropped as "template gone".
- **Fixed, pool:** right after the dev-fee minute, a few shares could show as stale or rejected
  that were not the rig's own.
- **Windows:** the miner warns at start when the paging file is too small for the memory the cards
  use, and says how much to add. Its RAM use after the cards load dropped from about 18 GB to
  about 2 GB (measured on a rig with an RTX 5070 Ti and an RTX 3060).

## 1.0.3 (2026-10-15)

Keryx: a fix for cards that could stop with an out-of-memory error while loading, most often
right after a reboot, and then did not mine. Hashrate unchanged.

## 1.0.2 (2026-10-13)

More Keryx hashrate on RTX 30, RTX 40 and RTX 50 cards, with nothing to set.
Measured on a mining rig at each card's usual overclock, against the previous version:

- RTX 30 series: about **+1.0 to +1.7%** (RTX 3060 +1.0 to +1.7%, RTX 3070 +1.1%, RTX 3080
  +1.6 to +1.7%), at about the same hashrate per watt.
- RTX 50 series: about **+1.9%** on an RTX 5070 Ti locked at 2300 MHz, for 2 to 6 W more.
- RTX 40 series: should gain like RTX 30; not measured yet. Reports are welcome.
- RTX 20 series and CMP 170HX: unchanged.

## 1.0.1 (2026-10-12)

- RTX 20 series: back to the hashrate of 0.0.32, and memory overclock raises hashrate again.
  1.0.0 lowered hashrate on desktop RTX 20 cards by up to ~13% (reported: RTX 2070 1.42 →
  1.24 MH/s). Laptops at their power limit give back the ~4.5% that 1.0.0 gave them.
- RTX 40 series: more hashrate, with nothing to set. Measured on an RTX 4090 at stock clocks
  with a 410 W power limit: about **+2.8%** (3.54 → 3.64 MH/s), at about +2% hashrate per watt.
  Other RTX 40 cards were not measured yet. Reports of the hashrate you see are welcome.
- RTX 30, RTX 50 and CMP 170HX: unchanged from 1.0.0.

## 1.0.0 (2026-10-12)

Higher Keryx hashrate on NVIDIA RTX 20 and RTX 30 cards, with nothing to set. Estimated gain over
0.0.32 by card family, at the same overclock:

- RTX 20 series: about +4.5% (measured on an RTX 2070 Max-Q laptop at its power limit; desktop
  cards that do not reach their power limit may gain less).
- RTX 30 series: about +1% (measured: RTX 3060 +1.1 to +1.3%, RTX 3070 +1.0%, RTX 3080 +1.0%),
  at the same or slightly better hashrate per watt.
- RTX 50 series, RTX 40 series and CMP 170HX: unchanged.

## 0.0.32 (2026-10-11)

- NVIDIA CMP 170HX now mines. Cards unlocked to 64 GB mine tier 4. Measured on two unlocked
  cards at a 200 W power limit: ~3.2 MH/s per card, 6.4 MH/s for the rig.
- No change for other cards.

## 0.0.31 (2026-10-09)

- Fewer strikes after a crash. An AI request the rig still owed when the miner restarted is
  answered after the restart while its window is open.
- A card that crashes the miner while answering AI requests keeps mining but is kept off AI
  requests for a day (then three days, then a week). The next start writes a crash report into
  `log.txt` with the card, its overclock, temperature, power, PCIe link and the likeliest cause.
- Tier 2 requests that arrived while a card was busy mining are no longer dropped.
- Answers use the web results a request carries, as the official miner does.
- Stats API: `--stats ADDRESS:PORT` serves `GET /stats` (default `127.0.0.1:4060`). `run.sh` and
  `start.bat` have a `STATS` line.

## 0.0.30 (2026-10-09)

- Linux and Windows get 0.0.29's change.

## 0.0.29 (2026-10-09, HiveOS only)

- Every card mines until an AI request arrives. A request pauses only the cards it needs, and they
  go back to mining once it is answered.
- When loading the AI model is slow for the request window, the log says so at start.

## 0.0.28 (2026-10-08)

- Hashrate unchanged.

## 0.0.27 (2026-10-08)

- Choose which cards mine with `--device`, by the numbers the miner shows: `--device 1,6` in
  HiveOS Extra config, `DEVICES=` in `run.sh` and `start.bat`.

## 0.0.26 (2026-10-08)

- The miner version shows in the TUI header and on every log line.

## 0.0.25 (2026-10-08)

- Hashrate unchanged.

## 0.0.24 (2026-10-08)

- A card the AI engine cannot run on no longer stops the miner. It keeps mining, the other cards
  answer AI requests, and the log says which card and why.

## 0.0.23 (2026-10-08)

- `--tier 1` (every card) or `--tier 2,0,2` (per card) forces a tier.

## 0.0.22 (2026-10-08)

- Ready for the H14 hard fork (DAA 121,985,000). Solo miners need keryx-node 1.6.4 or newer.
- Tier 3 (24 GB cards) moves to Qwen3.8-27B at the fork. The new model downloads in the background
  before the fork, and the miner switches by itself.
- Private AI requests after the fork, answered solo and on the pool.
- Long AI requests get an answer instead of failing.
- A model another miner on the rig already downloaded is reused, with no new download and no
  second copy on disk.
