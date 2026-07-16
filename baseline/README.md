# RTL 1.0 Baseline

Screenshots of RTL as it shipped on the date below, captured as the "before"
reference for the 2.0 design overhaul.

## What the v1.0 tag covers

The tag bundles two things produced roughly five years apart:

- **The Sketch mockups under `lnd/`** — design *proposals* from 2019–2021. They
  predate the shipped UI and are not a record of what was built.
- **The screenshots in this folder** — the *as-built* RTL interface on the
  capture date below.

Where the two disagree, the screenshots are the accurate record of the app.

## Capture provenance

| Field | Value |
|---|---|
| RTL app version | 0.15.8-beta (`shahanafarooqui/rtl:v0.15.8`) |
| RTL app commit | `6a01e96c` (`master`), plus the fixture password fix from PR #1623 |
| Node implementation | LND 0.20.0-beta (`polarlightning/lnd:0.20.0-beta`) |
| Backend | Bitcoin Core 30.0 (`polarlightning/bitcoind:30.0`) |
| Network | regtest |
| Capture date | 2026-07-16 |
| Fixture | RTL repo, `docker/` — see its README |
| Capture harness | `capture/` in this folder |

## Capture conditions

| Field | Value |
|---|---|
| Browser | Chromium 149.0.7827.55 via Playwright 1.61.1 |
| OS | macOS 26.5.2, arm64 |
| Viewport | 1440×900 |
| Device scale factor | 2 — **files are 2880×1800** |
| Mobile viewport | 390×844 @2 — file is 780×1688 |
| Theme / skin | Purple (default) |
| Mode | Day |

Re-shoot the 2.0 "after" under these same conditions, using `capture/`. Device
scale factor especially: at DPR 1 the same viewport produces a 1440×900 file, and
a re-shoot at a different ratio makes before/after comparison invalid.

## Data provenance

All data is **fabricated**. Captures were taken against a local regtest network
with three LND nodes (alice, bob, carol) created by the fixture's `scripts/seed.sh`,
which uses fixed amounts so a fresh run reproduces identical state. No real node,
no mainnet or testnet data, nothing redacted — there was nothing sensitive to
redact.

Topology: `alice --[5,000,000 sat]--> bob --[3,000,000 sat]--> carol`. bob routes,
which is what populates the routing and forwarding screens.

## Screens

35 screenshots. Filenames follow `lnd-<screen>-<variant>-<mode>.png`. See
`shot-list.md` for the routes and the reasoning behind the list.

### Empty states — captured before seeding

| File | Screen |
|---|---|
| `lnd-login.png` | Login |
| `lnd-dashboard-operator-empty.png` | Dashboard, no data |
| `lnd-channels-empty.png` | Channels, none open |
| `lnd-peers-empty.png` | Peers, none connected |
| `lnd-payments-empty.png` | Payments, none |
| `lnd-invoices-empty.png` | Invoices, none |

### Populated — captured after seeding

| File | Screen | Node |
|---|---|---|
| `lnd-dashboard-operator-day.png` | Dashboard, operator persona | alice |
| `lnd-dashboard-merchant-day.png` | Dashboard, merchant persona | carol |
| `lnd-dashboard-routing-day.png` | Dashboard, routing node | bob |
| `lnd-dashboard-operator-mobile.png` | Dashboard at mobile width | alice |
| `lnd-channels-open.png` | Channels, one open | alice |
| `lnd-channels-open-routing.png` | Channels, two open | bob |
| `lnd-channels-pending.png` | Channels, pending | alice |
| `lnd-channels-closed.png` | Channels, closed | alice |
| `lnd-peers.png` | Peers | bob |
| `lnd-payments.png` | Payments, 7 sent | alice |
| `lnd-invoices.png` | Invoices, 5 settled + 2 open | carol |
| `lnd-onchain-receive.png` | On-chain receive | alice |
| `lnd-onchain-send.png` | On-chain send | alice |
| `lnd-wallet.png` | Wallet | alice |
| `lnd-routing-forwardinghistory.png` | Forwarding history, 5 forwards | bob |
| `lnd-routing-peers.png` | Routing peers | bob |
| `lnd-reports-routing.png` | Routing report | bob |
| `lnd-reports-transactions.png` | Transactions report | alice |
| `lnd-graph-queryroutes.png` | Query routes | alice |
| `lnd-graph-lookups.png` | Lookups | alice |
| `lnd-network.png` | Network info | alice |
| `lnd-messages-sign.png` | Sign message | alice |
| `lnd-messages-verify.png` | Verify message | alice |
| `lnd-channelbackup.png` | Channel backup | alice |
| `lnd-settings-app.png` | Settings, application | alice |
| `lnd-settings-auth.png` | Settings, authentication (2FA) | alice |
| `lnd-settings-nodeconfig.png` | Settings, node config | alice |
| `lnd-services-loop-unconfigured.png` | Loop, unconfigured | alice |
| `lnd-services-boltz-unconfigured.png` | Boltz, unconfigured | alice |

## Caveats

Facts a reader needs in order to interpret these correctly.

- **Loop and Boltz are unconfigured.** The fixture runs no `loopd` and no Boltz
  service, so those two screens show the unconfigured state. That is what an RTL
  user without those services sees, so it is a legitimate as-built record — but it
  is **not** comparable to the mockups in `lnd/loop/` and `lnd/swapservices/`,
  which assumed a configured service.
- **`lnd-channels-pending.png` and `lnd-channels-closed.png` are empty.** Nothing
  is mid-open or closed at rest in the seeded fixture. The screens are captured to
  record their empty layout; they are not examples of populated pending/closed
  channel lists.
- **Onboarding / first-run is not captured.** The fixture's config pre-configures
  three nodes, so RTL's first-run flow never appears. Capturing it needs RTL booted
  with no configured node.
- **Night mode is not captured.** `themeMode` is a per-node setting on
  `/rtl/settings/bconfig` and the harness does not yet script it. Everything here
  is day mode, purple.
- **Merchant vs operator differ by data as well as persona.** alice (operator) has
  a channel and 7 payments; carol (merchant) has one channel and the invoices. The
  two dashboards are therefore not a clean isolation of the persona setting.
- **Fiat conversion is off** (`fiatConversion: false` in the fixture config), so no
  fiat values appear anywhere.
