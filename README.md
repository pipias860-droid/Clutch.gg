# CLUTCH.gg

A FACEIT-style CS2 matchmaking platform built as a fully client-side React app. Dark tactical UI, orange accents, and a complete simulated queue → accept → veto → live match → Elo loop.

## Stack

- React 19 + TypeScript
- Vite 6
- React Router 7
- Custom CSS (no UI framework)
- Google Fonts: Chakra Petch + Inter

## Getting started

```bash
npm install
npm run dev
```

Then open the URL printed by Vite (usually `http://localhost:5173`).

```bash
npm run build     # type-check + production build to dist/
npm run preview   # serve the production build
```

## Pages

| Route | Description |
| --- | --- |
| `/` | Landing page with hero, radar visual, map pool, rank ladder, and CTA |
| `/play` | Matchmaking flow: queue, accept, interactive map veto, live match, result |
| `/leaderboard` | Season leaderboard with rank tiers and player stats |
| `/matches` | Your match history and live matches |
| `/matches/:id` | Match detail with scoreboard, round timeline, and player comparisons |
| `/player/:id` | Player profile with Elo chart, skills, and achievements |
| `*` | Themed 404 ("Position Unknown") |

## Simulated features

- **Matchmaking loop** — search timer, 15-second accept window, best-of map veto with auto-veto fallback, then a live scoreboard that plays out rounds with a kill feed. You can play manually or toggle auto-play.
- **Elo progression** — results update your Elo, wins/losses, form, and match history. Rank badges and level tiers recalculate from your current Elo.
- **Persistence** — progress is stored in `localStorage` under `clutch.progress.v1`. A "reset progress" action restores the starting profile.
- **Deterministic mock data** — 45 players, generated matches, live games, maps, and stats are seeded, so reloads stay consistent without a backend.
- **Procedural visuals** — radar map thumbnails and gradient initial avatars are generated in SVG/CSS; no external image assets.

You start at **2,142 Elo** (Level 8 / Colonel) as the player **Vortex**.

## Structure

```text
src/
  components/   Layout, avatars, rank badges, map thumbnails, match rows, icons
  context/      AppContext — Elo, record, and localStorage persistence
  data/         Players, matches, maps, and generated stats
  lib/          Rank/Elo math and small utilities
  pages/        Home, Play, Leaderboard, Matches, MatchDetail, Profile, NotFound
  styles/       base, home, pages, responsive layers imported by styles.css
  App.tsx       Route map
  main.tsx      Entry point
```

## Notes

- This is a front-end demo: matchmaking, opponents, and results are simulated locally.
- No backend, accounts, or real-time networking are included.
