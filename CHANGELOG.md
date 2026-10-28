# Release notes

## Beta 20261027-191122-9dcec7c0 — October 27, 2026

- **Workflow responsiveness:** background account refresh reduces submission waits. Stale or invalidated account data still requires refresh. The DOM can seed from available streamed prices; cached chart history can draw while fresh history loads. Watchlist history prefetch is paused in NinjaTrader mode.
- **Chart Risk Buy/Sell:** target markers appear together. Moving a tracked, unfilled Risk limit recalculates quantity against the staged stop, subject to risk checks and available funds. Partly filled entries retain their size; DOM moves and trade-copier follower sizing are unchanged. Chart status explains missing stops and funds caps.
- **Account Details:** More > Account Details shows the selected account summary and positions, plus additional fields supplied by Schwab. Other brokers show their available shared summary fields.
- **Workspace:** watchlist sort field and direction persist between launches; More-menu items are alphabetical.
- **Schwab stop fills:** OCO stop legs, including replacement children, are parsed for filled quantity and price. Stop fills trigger reconciliation when Enable Reconciler is on.

Installer SHA-256:

```text
28b03c9b1ea90cbe9d611fd9a8e567b5d4d4393125cb1e736505448c85ba3f8b
```

[Official download and checksum](https://fastdom.decoglobal.us/download). Unsigned Windows installer, 116,400,120 bytes. Existing saved settings are preserved. The candidate Beta regression gate passed 2,416 tests. Automated checks do not certify every native broker workflow; clean-machine onboarding remains under verification. Installer tests were not rerun for this application-only release.

## Beta 20261026-162226-ca8c2cea — October 26, 2026

- **Chart timeframes:** select a row in Chart Timeframes, use Move Up or Move Down, then Save. The chart dropdown keeps your chosen order.
- **Shutdown reliability:** closing FastDOM uses bounded cleanup, so stalled background services or child windows can no longer block shutdown indefinitely. Cleanup timeouts are logged.
- **Trading safety:** Secure, Bracket, Flatten and Reverse stop when earlier orders cannot be confirmed resolved. Missing order status counts as unresolved, and position direction and quantity are refreshed before replacement orders. Incomplete actions are reported.
- **NinjaTrader:** account discovery follows the connected-account list from the updated bridge, including connected unfunded accounts. Install or repair the bundled bridge, compile and reload it in NinjaTrader, then reconnect. Older bridges keep the previous account filter until upgraded. Trading permissions are unchanged.
- **Alpaca:** switching accounts reconnects streaming and restores quote subscriptions; connection and quote-age indicators refresh correctly.
- **Privacy mode:** shows only the last 3 characters of account numbers and Alpaca API keys. API secrets stay fully hidden.

Installer SHA-256:

```text
139fd7d0f529af571694689f331610a307582f8a221b7dd167af17f7fe65f053
```

Download and checksum are published on the [official download page](https://fastdom.decoglobal.us/download). The installer is unsigned. Clean-machine onboarding remains under verification. Existing saved settings are preserved.

## Beta 20261026-004726-eea7c609 — October 26, 2026

The current public installer includes the earlier installation and packaging fixes, a MACD/cumulative-delta chart crash repair, and options-view improvements: readable Levels selection, a responsive visible-strike count and correctly grouped call/put columns.

Installer SHA-256:

```text
a24944c390864f3a3fa78f817c37e42e9967098e0273518fb6026136a4f5c54d
```

Download and checksum are published on the [official download page](https://fastdom.decoglobal.us/download). The installer is unsigned. Clean-machine onboarding remains under verification. Newer training lessons can show display improvements not yet in this public installer; their build notes identify that distinction.

## Beta 20261025-150447-934ac48b — October 25, 2026

- Removed owner-specific NinjaTrader account defaults and expired contract mappings from fresh Beta installs.
- Disabled live-account discovery by default for fresh NinjaTrader configurations.
- Included the NinjaTrader bridge and installation instructions.
- Made Beta fallback settings use Simulation and SQLite.
- Improved optional legacy Derby support-code path isolation.
- Clarified local Codex, hosted Help, and browser requirements.
- Strengthened packaging checks for SQLite components, NinjaTrader defaults, and credentials.

Existing saved settings are preserved. Review account permissions and exact contract mappings before connecting.

Validation: 114 focused Beta tests, 88 Developer regression tests, and 13 packaging/isolation tests passed. Isolated installer install/update/uninstall and runtime preview checks passed. These checks do not replace clean-machine acceptance or customer broker onboarding.

Installer SHA-256:

```text
9fccbe0d36f9b4e0d66b13c70067462e6ee6f3d912975891039e61ba68f9335e
```

[Official download and checksum](https://fastdom.decoglobal.us/download)
