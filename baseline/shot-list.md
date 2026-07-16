# Baseline shot list

The screens captured for the 1.0 baseline, the order they are captured in, and
what is deliberately missing.

This is the input to `capture/capture.mjs`, which holds the same list in code.
If the two disagree, the script is authoritative.

## How the routes were established

Screens were first enumerated from RTL's routing (`src/app/lnd/lnd.routing.ts`,
`src/app/app.routing.ts`), then **verified against a running RTL by checking page
content**. That second step matters: Angular renders its 404 component without
changing the URL, so a route can look fine while being a "Page Not Found". A
first pass that compared only `location.pathname` reported every candidate as OK,
including three that are actually 404s:

- `/rtl/settings/config`
- `/rtl/settings/nodesettings`
- `/rtl/settings/pglayout`

Node Config is `/rtl/settings/bconfig`. All routes are prefixed `/rtl`.

## Conventions

- Viewport 1440×900, device scale factor 2, so files are 2880×1800
- Filenames `lnd-<screen>-<variant>-<mode>.png`
- Theme purple (default), day mode

## Order

The fixture starts with three fully-wired but empty nodes, so both the empty and
populated states come from one sequence. Order is what matters:

1. `docker compose down -v && docker compose up -d` (fixture, in the RTL repo)
2. `OUT_DIR=.. node capture.mjs empty`
3. `./scripts/seed.sh`
4. `OUT_DIR=.. node capture.mjs full`

## Phase A — empty states (before seeding)

The 2019 mockups treated these as first-class (`1.1channels_nochannels.png`,
`2.1peers_nopeers.png`), and they are where an overhaul usually finds the most rot.

| File | Screen | Route |
|---|---|---|
| `lnd-login.png` | Login | `/rtl/login` |
| `lnd-dashboard-operator-empty.png` | Dashboard, no data | `/rtl/lnd/home` |
| `lnd-channels-empty.png` | Channels, none open | `/rtl/lnd/connections/channels/open` |
| `lnd-peers-empty.png` | Peers, none connected | `/rtl/lnd/connections/peers` |
| `lnd-payments-empty.png` | Payments, none | `/rtl/lnd/transactions/payments` |
| `lnd-invoices-empty.png` | Invoices, none | `/rtl/lnd/transactions/invoices` |

## Phase B — populated (after seeding)

alice holds the 5M channel to bob and has sent 7 payments. bob is the routing
node (2 channels, 5 forwards). carol holds the invoices.

| File | Screen | Route | Node |
|---|---|---|---|
| `lnd-dashboard-operator-day.png` | Dashboard, operator | `/rtl/lnd/home` | alice |
| `lnd-dashboard-merchant-day.png` | Dashboard, merchant | `/rtl/lnd/home` | carol |
| `lnd-dashboard-routing-day.png` | Dashboard, routing node | `/rtl/lnd/home` | bob |
| `lnd-channels-open.png` | Channels, open | `/rtl/lnd/connections/channels/open` | alice |
| `lnd-channels-open-routing.png` | Channels, two open | `/rtl/lnd/connections/channels/open` | bob |
| `lnd-channels-pending.png` | Channels, pending | `/rtl/lnd/connections/channels/pending` | alice |
| `lnd-channels-closed.png` | Channels, closed | `/rtl/lnd/connections/channels/closed` | alice |
| `lnd-peers.png` | Peers | `/rtl/lnd/connections/peers` | bob |
| `lnd-payments.png` | Payments | `/rtl/lnd/transactions/payments` | alice |
| `lnd-invoices.png` | Invoices | `/rtl/lnd/transactions/invoices` | carol |
| `lnd-onchain-receive.png` | On-chain receive | `/rtl/lnd/onchain/receive/0` | alice |
| `lnd-onchain-send.png` | On-chain send | `/rtl/lnd/onchain/send/0` | alice |
| `lnd-wallet.png` | Wallet | `/rtl/lnd/wallet` | alice |
| `lnd-routing-forwardinghistory.png` | Forwarding history | `/rtl/lnd/routing/forwardinghistory` | bob |
| `lnd-routing-peers.png` | Routing peers | `/rtl/lnd/routing/peers` | bob |
| `lnd-reports-routing.png` | Routing report | `/rtl/lnd/reports/routingreport` | bob |
| `lnd-reports-transactions.png` | Transactions report | `/rtl/lnd/reports/transactions` | alice |
| `lnd-graph-queryroutes.png` | Query routes | `/rtl/lnd/graph/queryroutes` | alice |
| `lnd-graph-lookups.png` | Lookups | `/rtl/lnd/graph/lookups` | alice |
| `lnd-network.png` | Network info | `/rtl/lnd/network` | alice |
| `lnd-messages-sign.png` | Sign message | `/rtl/lnd/messages/sign` | alice |
| `lnd-messages-verify.png` | Verify message | `/rtl/lnd/messages/verify` | alice |
| `lnd-channelbackup.png` | Channel backup | `/rtl/lnd/channelbackup/bckup` | alice |
| `lnd-settings-app.png` | Settings, application | `/rtl/settings/app` | alice |
| `lnd-settings-auth.png` | Settings, authentication | `/rtl/settings/auth` | alice |
| `lnd-settings-nodeconfig.png` | Settings, node config | `/rtl/settings/bconfig` | alice |

Plus `lnd-dashboard-operator-mobile.png` at 390×844.

## Unconfigured-state captures

These render, but with nothing behind them: the fixture runs no `loopd` and no
Boltz. An RTL without those services is what most users see, so these are
legitimate as-built records — but they are **not** comparable to the `lnd/loop/`
and `lnd/swapservices/` mockups, which assumed a configured service.

| File | Screen | Route |
|---|---|---|
| `lnd-services-loop-unconfigured.png` | Loop | `/rtl/services/loop/loopout` |
| `lnd-services-boltz-unconfigured.png` | Boltz | `/rtl/services/boltz/swapout` |

## Not captured

Stated here rather than left as a silent hole. See the caveats in `README.md`.

| Screen | Why | Cost to add |
|---|---|---|
| Onboarding / first run | Config pre-configures three nodes, so the flow never appears | Boot RTL with no configured node |
| Channels — pending, populated | Nothing is mid-open at rest; the captured screen is empty | Open a channel and shoot before confirming |
| Channels — closed, populated | Nothing is closed; the captured screen is empty | Close a channel in the seed |
| Channels — active HTLCs | No HTLCs in flight at rest | Hold an invoice mid-payment |
| Night mode | `themeMode` is per-node on `/rtl/settings/bconfig`; not scripted | Script the toggle, or ship a second config |
| Loop / Boltz, configured | No `loopd` or Boltz in the fixture | Add both services |
| Rates / fiat | `fiatConversion: false` in the fixture config | Flip it; needs network access |
