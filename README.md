# Buildout Atlas

Interactive national map and inventory of publicly-announced U.S. AI infrastructure — hyperscale data centers, GPU campuses, power expansions, chip fabs, and related buildouts.

**Phase 1 MVP.** Single self-contained `index.html` — no build step, no backend, no API keys. Open in any browser.

## What's in here

- 30 sourced sites across 19 states and 20 companies
- Every entry includes: project name, company, city/county/state, lat/lon, status, project type, source URL, confidence level, last updated
- 4 views: Home (totals + leaderboards), Map (Leaflet + OpenStreetMap), List (search/filter/sort), Detail (per-location)
- Status legend: Announced · Permitting · Under Construction · Operational · Paused/Contested

## Local use

```bash
open index.html
```

Or serve over HTTP if your browser blocks `file://`:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy

Static site. Works on any static host:

- **Vercel** — connect this repo, no config needed (`vercel.json` included for clarity)
- **GitHub Pages** — Settings → Pages → Deploy from `main` branch root
- **Netlify** — drag the repo or connect via Git
- **Cloudflare Pages** — connect and deploy

## Adding sites

Open `index.html`, find `const DATA = {`, and add objects to the `locations` array. The schema is enforced by convention — every site needs the 8 required fields:

1. `project_name` + `company`
2. `city` / `county` / `state`
3. `latitude` / `longitude`
4. `status` (Announced, Permitting, Under Construction, Operational, Paused / Contested, Unknown)
5. `project_type` (Hyperscale Data Center, GPU Cluster / AI Campus, Power Plant / Energy Expansion, Transmission Upgrade, Water / Cooling Infrastructure, Chip / Semiconductor Support, Fiber / Network Infrastructure, AI Data Center)
6. `source_url` (must be a real URL — no unsourced rumors)
7. `confidence_level` (High / Medium / Low)
8. `last_updated` (YYYY-MM-DD)

Filters and dropdowns auto-populate from the data. No code changes needed.

## Roadmap

- **Phase 1.5** — push to 50 sites; add tier-2 operators (Applied Digital, Lambda, Together AI, Nebius, Crusoe non-Abilene, Switch, DataBank, QTS, Aligned); add transmission-only and water-only stories
- **Phase 2** — deep-dossier pages for the 10 anchor examples
- **Phase 3** — sponsor / media / local-opportunity layer
- **Phase 4** — admin UI for non-engineers to add sites without touching JSON
