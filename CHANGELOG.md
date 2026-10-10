# Changelog

What changed in each version, newest first. Versions before 0.0.22 are invalid since the H14 hard
fork (2026-10-09) and are not listed.

## 0.0.31 (2026-10-09)

- Cards on narrow PCIe links that mine a tier larger than their memory get much faster, with
  nothing to set. They settle about two minutes after start. Measured: RTX 5070 Ti on a 3.0 x1
  riser ~120 → 419 kH/s, RTX 3070 on 3.0 x1 117 → 346 kH/s, RTX 5070 Ti on 3.0 x4 ~490 → 876 kH/s.
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

- Higher hashrate on narrow risers for cards just short of their tier's memory. A card that was a
  little short now mines its tier at full speed.
- Linux and Windows get 0.0.29's change.

## 0.0.29 (2026-10-09, HiveOS only)

- Every card mines until an AI request arrives. A request pauses only the cards it needs, and they
  go back to mining once it is answered.
- When loading the AI model is slow for the request window, the log says so at start.

## 0.0.28 (2026-10-08)

- A card that mines a tier larger than its memory now needs another card, or two together, that
  can answer that tier's AI requests. Without one, the card does not mine that tier, and the log
  and TUI say why. This avoids strikes for requests the rig could not answer.

## 0.0.27 (2026-10-08)

- Choose which cards mine with `--device`, by the numbers the miner shows: `--device 1,6 -- --tier
  3,3` in HiveOS Extra config, `DEVICES=` in `run.sh` and `start.bat`.

## 0.0.26 (2026-10-08)

- Windows: cards that mine a tier larger than their memory now use all of it. Measured on an
  RTX 5070 Ti, tier 3: 95% → 97.8% of the model on the card.
- The miner version shows in the TUI header and on every log line.

## 0.0.25 (2026-10-08)

- Cards that mine a tier larger than their memory are faster on every PCIe link and use less RAM.
  Measured on two RTX 5070 Ti, tier 3: PCIe 5.0 x4 1.63 → 2.68 MH/s.

## 0.0.24 (2026-10-08)

- A card the AI engine cannot run on no longer stops the miner. It keeps mining, the other cards
  answer AI requests, and the log says which card and why.

## 0.0.23 (2026-10-08)

- 6 GB cards mine tier 0. Have 2 GB of RAM free at start. A faster PCIe link gives more hashrate.
- `--tier 1` (every card) or `--tier 2,0,2` (per card) forces a higher tier. A card forced above
  its memory mines instead of failing.

## 0.0.22 (2026-10-08)

- Ready for the H14 hard fork (DAA 121,985,000). Solo miners need keryx-node 1.6.4 or newer.
- Tier 3 (24 GB cards) moves to Qwen3.8-27B at the fork. The new model downloads in the background
  before the fork, and the miner switches by itself.
- Private AI requests after the fork, answered solo and on the pool.
- Long AI requests get an answer instead of failing.
- A model another miner on the rig already downloaded is reused, with no new download and no
  second copy on disk.
