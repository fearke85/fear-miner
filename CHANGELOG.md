# Changelog

What changed in each version, newest first. One version of fear-miner covers every coin; a change
for one coin names it. Every change listed so far is for Keryx.

Keryx: versions before 0.0.22 are invalid since the H14 hard fork (2026-10-09) and are not listed.

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
