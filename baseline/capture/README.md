# Baseline screenshot capture

Drives RTL against its regtest fixture and captures the screens listed in
`../shot-list.md`.

The point is that the capture conditions live in code rather than in someone's
memory: viewport, device scale factor, browser and screen list are all pinned in
`capture.mjs`. A capture taken today and one taken after the 2.0 redesign differ
only by the design.

## Requires the fixture

The fixture lives in the **RTL app repo** at `docker/`, not here. It is a runtime
dependency only — this script imports no RTL code, it just drives
`http://localhost:3000`.

```bash
cd /path/to/RTL/docker
docker compose up -d
```

## Use

```bash
npm install
npx playwright install chromium
```

Empty states are captured **before** seeding, populated screens **after**. The
fixture starts with three fully-wired but empty nodes, so both states come free
from the same run — the order is what matters.

```bash
# 1. empty states, against a fresh unseeded network
cd /path/to/RTL/docker && docker compose down -v && docker compose up -d
cd -                                      # back here
OUT_DIR=.. node capture.mjs empty

# 2. seed, then the populated screens
cd /path/to/RTL/docker && ./scripts/seed.sh
cd -
OUT_DIR=.. node capture.mjs full
```

`OUT_DIR=..` writes into `baseline/` alongside the notes. Without it output goes
to `./shots`, which is gitignored.

## Conditions

| | |
|---|---|
| Viewport | 1440×900 (mobile 390×844) |
| Device scale factor | 2 — files are therefore 2880×1800 |
| Browser | Chromium via Playwright |
| Password | `rtldev` — must match `multiPass` in the fixture's `rtl/RTL-Config.regtest.json` |

Record these in `../README.md`. Device scale factor especially: re-shooting at a
different ratio invalidates before/after comparison, and nobody remembers it a
year later.

## Notes

- Routes were verified against a running RTL by checking page **content**, not the
  URL. Angular renders its 404 component without changing the URL, so a route can
  look fine while being a "Page Not Found". Three plausible-looking ones are 404s
  and are deliberately absent: `/rtl/settings/config`, `/rtl/settings/nodesettings`,
  `/rtl/settings/pglayout`. Node Config is `/rtl/settings/bconfig`.
- The password must not be one of RTL's blacklisted weak passwords (`password`,
  `changeme`, `moneyprintergobrrr`) or login is redirected to a forced password
  change and never reaches the dashboard.
- Loop and Boltz are not configured in the fixture, so those shots record the
  unconfigured state. See `../shot-list.md`.
- Night mode and persona are per-node settings on `/rtl/settings/bconfig` and are
  not yet scripted.

## Cross-repo coupling

This script depends on RTL's routes and DOM, which live in another repo, and
nothing in RTL's CI exercises it. When RTL changes a route this rots silently,
and whoever runs the next capture finds out. That is a real cost of keeping it
here, accepted because the baseline is a design deliverable and the artifacts
land in this repo. If it starts rotting often, revisit.
