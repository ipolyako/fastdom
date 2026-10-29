# Release notes

## Beta 20261029-134259-b247e78c — October 29, 2026

- Options Trader: spread builder, payoff analysis, scanning and advisory AI review, with indicative after-hours research kept separate from fresh execution quotes.
- Spread price changes stay open and show results. Pending/partial/terminal orders and duplicate changes are guarded; ambiguous broker outcomes require reconciliation. Late responses preserve terminal states.
- Reverse calendars, diagonals and unsupported structures no longer receive a misleading premium-only risk estimate.
- Select Codex or Claude Code in Configuration using your own installed, signed-in CLI. Market Desk can create a separate saved daily watchlist.
- Includes Alpaca held-OCO visibility/status fixes, whole-cent OCO pricing, ORB display repairs, manual Watch membership, and keyboard/cancellation safeguards.

Verification: 2,796 Beta and 2,816 Developer tests passed, including 546 trading-workflow and 41 safety cases. Independent review covered the spread repairs. Isolated installer install/update/uninstall and overwrite guards passed. Native Schwab spread replacement and clean-machine onboarding remain unverified; automated tests are not native broker acceptance.

Unsigned Windows x64 installer: 116,555,185 bytes.
SHA-256: `cb3edf8a5055e1bf3781eca03182eb584b3c3e018236320b362c9fe5f880e1f1`.

[Official download and checksum](https://fastdom.decoglobal.us/download) · [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/).
Close Beta and run the installer to update. Settings remain separate.

## Beta 20261028-095331-d39a0689 - October 28, 2026

- Preserve confirmed fills when stale working updates or snapshots arrive, across Schwab, Alpaca and NinjaTrader.
- Keep Watch membership manual; positions and orders no longer re-add explicitly removed symbols.
- Enforce 41 exact safety regression cases and all 546 trading-workflow cases on every canonical publish. Missing, skipped, duplicate or failed cases block the build's release gate.
- Cover typing isolation, cancellation races, failed synchronization/recovery and synthetic Alpaca payload replay.

Beta: 2,473 tests passed. Developer: 2,493 passed. Independent review completed. No live orders used for QA. Native paper acceptance and clean-machine onboarding remain unverified; automated tests do not guarantee broker cancellation. Installer mechanics are unchanged from the previously tested installer.

Unsigned Windows x64 installer: 116,407,582 bytes. SHA-256: `84b24a35b1193c01bc75088d9631f8ef1a52ee1eb8372334b0ff226960881969`.

[Official download and checksum](https://fastdom.decoglobal.us/download) | [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/)

Close Beta and run the new installer to update. Saved settings and activation remain separate; installed applications do not update automatically.

## Beta 20261028-090613-135c93ad — October 28, 2026

- **Trading hotkeys:** typing in text-entry controls, including Shift/Ctrl combinations, cannot dispatch trading shortcuts. Market Desk and Trading Partner no longer forward trading hotkeys.
- **Cancellation status:** request acknowledgements are not cancellation confirmation. Pending cancellations remain visible; orders can still fill. Broker-confirmed fills are reported as fills.
- **Pending order actions:** chart moves, trailing updates and replacement requests are blocked for pending-cancel orders. Shift-drag preserves the original pending selection instead of moving other stops.

Installer SHA-256: `23e66899aad1cd2da294b2c0831de8322f510a1ac0f7fa52fc19e226d3ff81ad`. Unsigned Windows x64 installer, 116,409,230 bytes.

[Official download and checksum](https://fastdom.decoglobal.us/download) · [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/). Beta: 2,439 tests passed; Developer: 2,459 passed, including all 546 required trading cases. Independent source/evidence review completed. No live orders were used for testing. Clean-machine onboarding and native broker acceptance remain unverified; automated checks do not guarantee broker cancellation. Installer mechanics are unchanged and their tests were not rerun for this application-only release. Close Beta and run the installer to update; saved settings remain separate.

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
