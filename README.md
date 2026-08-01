# ◆ NEON SERPENT — Endless Drain

A minimal, addictive neon puzzle in the **NEON BASTION / NEON ROGUE** family: eject arrow blocks from the board, turn them into collectors, and **drain the serpent of energy orbs before it reaches the core** — across endless procedurally generated levels that get progressively harder.

Everything lives in a single dependency-free `index.html`. Open it in any browser (works great on phones) and play.

| Menu | Level 14 |
|---|---|
| ![Menu](docs/screenshot-menu.png) | ![Gameplay](docs/screenshot-play.png) |

## How to play

- The **serpent starts offscreen** and advances along the runway toward the core, its body streaming in behind it. If the head reaches the core, you lose.
- **Tap a block** to eject it. A block only slides in its **arrow direction** (diagonals appear at higher levels), and only if the path to the edge is clear — blocked taps flash the piece in the way.
- An ejected block becomes a **collector**: small blocks hold 2 charges, big ones 4.
- Every collector automatically drains its color from **any orb visible on screen** — orbs zip out of the body, the body closes up, and each one **drags the serpent back**. Collectors all drain at once; chain them for streaks.
- A full collector discharges (+coins) and frees its slot. A collector with no on-screen match sits **dimmed**, blocking its slot until its color arrives.

### Boosters (cost ◆)

| Booster | Effect |
|---|---|
| ◀◀ Back | Pushes the serpent back down the runway |
| ⌁ Purge | Instantly deletes the two lead orbs |
| ⊕ Pull | Ejects a block matching the orb nearest the head |
| ▣ +Slot | Extra collector slot for the current level |

Coins come from discharged collectors and finished levels (with a no-booster bonus). You can unlock a permanent slot, and revive after a defeat with a big push-back.

## Infinite levels & difficulty

Every level is generated on the fly with balanced totals: collector capacity exactly matches the serpent's orbs, and a feasibility simulation guarantees the whole board can always be emptied.

Difficulty ramps with the level number:

- the serpent advances faster, while drain pushback weakens
- the visible window shrinks (more of the body hides offscreen)
- board grows **~16 → ~52 cells** (serpent ~32 → ~104 orbs)
- colors **3 → 7**, and same-color runs shorten
- arrows point outward early, then get increasingly knotted; **diagonals** appear from level 9
- harder board shapes (triangle, ring) only appear at higher levels

Progress (level, coins, unlocked slots, sound) is saved in `localStorage`.

## Development

No build step, no dependencies — edit `index.html` and refresh. A small debug API is exposed on `window.__wool` (state inspection, tapping pieces, fast-forward stepping, level generation), which the Playwright-based checks used during development: generation was verified across levels 1–999 (charge/orb parity, solvable order found in ≤ 11 ms), and a slightly-imperfect planning bot at human tap-speed — no boosters, no revives — wins ~100% of levels up to ~32, ~38% at 40, and ~13% at 50, where boosters and revives become part of the strategy.
