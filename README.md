# 🧶 Wool Crush — Infinite

A knitted-wool puzzle game inspired by *Wool Crush*: pull wool bolts off the board and feed the hungry yarn dragon — across **endless procedurally generated levels that get progressively harder**.

Everything lives in a single dependency-free `index.html`. Open it in any browser (works great on phones) and play.

| Level 1 | Level 12 |
|---|---|
| ![Level 1](docs/screenshot-level1.png) | ![Level 12](docs/screenshot-level12.png) |

## How to play

- **Tap a wool bolt** to pull it out. A bolt only slides in its **arrow direction**, and only if the path to the edge is clear — blocked bolts wiggle and flash the piece in the way.
- Pulled bolts land in the **tray** below the dragon.
- The **yarn dragon** eats its body from the head: wool matching the head segment's color feeds it automatically. The bubble by its head shows the color (and count) it wants next.
- **Win** by crushing the whole snake. **Lose** if the tray fills up with wool the dragon doesn't want.

### Boosters (cost coins)

| Booster | Effect |
|---|---|
| 🔀 Shuffle | Re-rolls every arrow on the board |
| 🔥 Chomp | Instantly crushes the head segment |
| 🧲 Fetch | Yanks a matching bolt out, ignoring blockers |
| 🧺 +Slot | Extra tray slot for the current level |

Coins come from finishing levels (with a no-booster bonus). You can also unlock a permanent tray slot, and revive after a defeat (return bolts to the board, or re-shuffle a gridlock).

## Infinite levels & difficulty

Every level is generated on the fly and is **guaranteed solvable**:

1. The board (diamond, heart, cross, ring, triangle, rectangle shapes) is tiled with 1- and 2-unit bolts and random arrows.
2. A full extraction is simulated to find a feasible pull order (re-rolling arrows when the simulation jams).
3. The dragon's color sequence is derived from that order, then shuffled inside a small window — so a solution always exists within the tray's buffer size.

Difficulty ramps with the level number:

- board grows **~17 → ~64 cells**
- colors **3 → 6**
- same-color runs shrink (more color switching)
- the feed order gets more scrambled
- more 2-unit bolts

Progress (level, coins, unlocked slots, sound) is saved in `localStorage`.

## Development

No build step, no dependencies — edit `index.html` and refresh. A small debug API is exposed on `window.__wool` (state inspection, tapping pieces, level generation stress-testing), which the Playwright-based checks used during development: level generation was verified across levels 1–999 (piece/segment parity, solvable order found in ≤ 11 ms), and a planning bot wins ~100% of early levels declining to ~⅔ at level 50 without boosters.
