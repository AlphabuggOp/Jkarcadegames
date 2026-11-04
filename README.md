# PixelVault 198X — Retro Arcade Hub

A complete, self-contained retro arcade hub in **one HTML file**: 10 playable canvas games,
10 instant-swap CSS themes, a pure-CSS CRT shader overlay, a Web Audio 8-bit synthesizer and a
persistent local high-score vault. No build step, no frameworks, no external scripts, no image
or audio assets.

```
index.html   ← the whole arcade (open it in any modern browser)
```

## Run it

Open `index.html` directly, or serve the folder:

```bash
python3 -m http.server 8000
# → http://localhost:8000
```

## What's inside

### Cabinet & navigation
- Animated marquee header: glowing pixel wordmark, scrolling high-score ticker, live clock and an **INSERT COIN** button (loads a random cabinet).
- Arcade cabinet stage: CRT screen, on-screen D-pad + A/B buttons (touch/mouse), live HUD (score / hi-score / lives / level), pause, reset and mute.
- Game library: 10 cards with hand-made 8×8 pixel-art badges, descriptions, 5-segment difficulty meters, per-game hi-score and instant launch buttons.

### The 10 cabinets
| # | Game | Genre | Controls |
|---|------|-------|----------|
| 1 | **PAC-MAZE** | maze chase | arrows/WASD to move, power pellets to hunt ghosts (BFS ghost AI) |
| 2 | **SPACE INVADERS** | shoot 'em up | ← → move, Space fire; destructible bunkers, UFO bonus |
| 3 | **GALAGA** | swooping fleet | ← → move, Space fire; enemies dive on curved paths |
| 4 | **BARREL JUMP** | platform rescue | ← → run, ↑/↓ ladders, Space jump over rolling barrels |
| 5 | **FROG CROSSING** | traffic + river | hop across 5 car lanes, ride logs, fill 7 lily pads |
| 6 | **ASTEROIDS** | vector inertia | ← → rotate, ↑ thrust, Space fire; wrap-around void, splitting rocks |
| 7 | **BRICK BREAKER** | breakout | mouse/touch paddle or ← →, Space to serve |
| 8 | **CENTIPEDE** | bug blaster | move + fire up through the mushroom field |
| 9 | **DIG & BURROW** | tunnel hunt | dig tunnels, pump monsters 4× to pop them |
| 10 | **DEFENDER RUN** | side-scroller | fly, strafe drone swarms, don't clip the terrain |

Every game is a `requestAnimationFrame` loop at a fixed logical resolution, scaled cleanly with
`image-rendering: pixelated`.

### 10 themes (instant, CSS-variable driven)
80s Neon Cyberpunk · CRT Arcade Cabinet · Game Boy DMG-01 · Commodore 64 · Vaporwave 1995 ·
NES Famicom · Atari Woodgrain · Amber Phosphor CRT · Matrix Terminal · Synthwave Sunset

Theme colour changes repaint the whole UI **and** the canvas palette (each game reads its colours
live from CSS custom properties, with per-theme canvas overrides for the monochrome/light screens).

### CRT effects
Scanlines, screen curvature and screen shake are individually toggleable (persisted). Scanlines and
the vignette are drawn by a composited CSS overlay, never by per-frame canvas work.

### 8-bit audio
A tiny Web Audio synth (`OscillatorNode` square/sawtooth + filtered white noise) generates jump,
shoot, coin, explosion, game-over, level-up and theme-blip effects. No audio files, and the
AudioContext is only created after a real user gesture.

### High scores
Best score per cabinet is stored in `localStorage` (`pixelvault198x.v1`), shown in the vault panel,
on each card and in the header ticker. **WIPE** clears them.

## Keyboard
`← → ↑ ↓` / `WASD` move · `Space` / `Z` action A · `Shift` / `X` action B ·
`Enter` start / restart · `Esc` / `P` pause · `R` reset cabinet · `M` mute · `1`–`0` launch cabinet.

## Notes
- Everything runs client-side; the only network request is the optional Google Fonts stylesheet
  (`Press Start 2P` + `VT323`), which degrades to monospace if offline.
- `window.PixelVault` exposes the engine (games, input, theme, save) for debugging.
