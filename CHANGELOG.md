# Release notes

## Beta 20261031-170828-3f40354e — October 31, 2026

- Market Movers now tries the selected broker's native APIs first: Schwab movers and Alpaca gainers/losers/most-actives. Unsupported, empty, failed or timed-out native requests use the existing fallback, with the source and reason displayed. NINJA MD keeps discovery on the primary broker.
- Schwab discovery retains its established sequential-request workaround and equity-universe selector to avoid repeated cached responses.
- FAST < $30 becomes Momentum Scan with Min price, Max price and Apply. Defaults to $1–$30; positive sub-dollar ranges are supported. Other filters remain visible: +5%, 100K shares, $500K dollar volume, spread no more than 2% when available. The range survives Refresh and resets on reopening the window.
- Risk-sized script entries reject missing or invalid risk/stop inputs and unavailable executable-side quotes instead of falling back to the selected share quantity. A rejected zero-size risk entry stops subsequent script commands. Existing custom scripts need an explicit valid STOP; updates preserve saved customizations.

Verification: 3,085 Developer and 3,065 Beta automated tests passed, including 700 exact trading-workflow and 41 safety cases. Independent source/evidence reviews completed. Published controls were checked with synthetic data; no real or paper orders were placed. The package and downloadable bytes are verified separately.

Limits: native API authentication/entitlements and new native order/fill acceptance were not exercised by this release. Ranked discovery lists are not a whole-market scan or exact reproduction of broker rankings. Alpaca uses native SIP rankings with IEX enrichment; missing volume excludes momentum candidates. Clean-machine onboarding remains unverified. Synthetic stops require FastDOM running and fresh quotes.

Unsigned Windows x64 Beta. Close Beta and run the installer to update; saved settings and activation remain separate. Review custom risk scripts before using them. FastDOM does not guarantee fills or maximum loss.

Installer: FastDOM-Beta-20261031-170828-3f40354e-Setup-UNSIGNED.exe

SHA-256: `d1c193846b73576c1f7de5254eb80993ec97d23d53ed63a58a4f983220bd33bb`

Size: 116,589,448 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/) · [Momentum Scan guide](https://github.com/ipolyako/fastdom/blob/main/docs/market-movers.md)

## Beta 20261031-165748-0e29da47 — October 31, 2026 (superseded)

Superseded the same day by 20261031-170828-3f40354e, which restores Schwab’s original sequential movers requests and equity-universe selector.

- Market Movers now tries the selected broker's native APIs first: Schwab movers and Alpaca gainers/losers/most-actives. Unsupported, empty, failed or timed-out native requests use the existing fallback, with the source and reason displayed. NINJA MD keeps discovery on the primary broker.
- FAST < $30 becomes Momentum Scan with Min price, Max price and Apply. Defaults to $1–$30; positive sub-dollar ranges are supported. Other filters remain visible: +5%, 100K shares, $500K dollar volume, spread no more than 2% when available. The range survives Refresh and resets on reopening the window.
- Risk-sized script entries reject missing or invalid risk/stop inputs and unavailable executable-side quotes instead of falling back to the selected share quantity. A rejected zero-size risk entry stops subsequent script commands. Existing custom scripts need an explicit valid STOP; updates preserve saved customizations.

Verification: 3,084 Developer and 3,064 Beta automated tests passed, including 700 exact trading-workflow and 41 safety cases. Independent source/evidence reviews completed. Published controls were checked with synthetic data; no real or paper orders were placed. The package and downloadable bytes are verified separately.

Limits: native API authentication/entitlements and new native order/fill acceptance were not exercised by this release. Ranked discovery lists are not a whole-market scan or exact reproduction of broker rankings. Alpaca uses native SIP rankings with IEX enrichment; missing volume excludes momentum candidates. Clean-machine onboarding remains unverified. Synthetic stops require FastDOM running and fresh quotes.

Unsigned Windows x64 Beta. Close Beta and run the installer to update; saved settings and activation remain separate. Review custom risk scripts before using them. FastDOM does not guarantee fills or maximum loss.

Installer: FastDOM-Beta-20261031-165748-0e29da47-Setup-UNSIGNED.exe

SHA-256: `d572e1620b77a37de70afd759249a93a5e0c7b7e4055aa5fe0b486b12c2ee1bd`

Size: 116,589,542 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/) · [Momentum Scan guide](https://github.com/ipolyako/fastdom/blob/main/docs/market-movers.md)

## Beta 20261030-093817-685bdeac — October 30, 2026

Schwab stop-replacement and Stop BE fixes:

- Confirm a replacement's concrete native order ID, working status and requested terms before reporting success. An HTTP acknowledgement alone is insufficient.
- Report rejected, cancelled, mismatched, executed or unconfirmed replacements honestly. Do not automatically retry or recreate protection when the outcome is uncertain.
- Preserve terminal states and confirmed fills when late replacement responses, exceptions or stale snapshots arrive.
- Check fresh executable bid/ask quotes before regular-session Schwab Stop BE changes. Stop further tranche changes after a failure and warn that remaining protection needs checking.

Verification: 2,858 Beta and 2,878 Developer tests passed, including all 546 required trading-workflow and 41 safety cases. Regression includes a sanitized native Schwab rejection sequence. Independent source/evidence review completed. The Developer build was installed and its Schwab connection, positions, execution history and advancing quotes checked. No live orders were submitted by this repair's QA.

Limits: the repaired replacement path has not been accepted with a new live Schwab trade. Stop BE checks the supplied quote throughout the batch but does not fetch a new quote per tranche; market movement can still cause rejection. Unknown outcomes do not trigger automatic reconstruction of protection. Clean-machine onboarding remains unverified. Synthetic stops still require FastDOM running and fresh quotes.

Unsigned Windows x64 installer. Close Beta and run the installer to update; settings and activation remain separate. Installer mechanics are unchanged; isolated install/update/uninstall/hash and folder/process-guard evidence from October 29 is reused. Packaging and downloadable bytes are checked for this build.

Installer: FastDOM-Beta-20261030-093817-685bdeac-Setup-UNSIGNED.exe

SHA-256: `1970aa372e306937cae05d4a09df88c80de51be10bcd74c258fdbf45435d8980`

Size: 116,572,728 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/)

## Beta 20261029-172909-482196fa — October 29, 2026

Protection lifecycle fixes:

- Validate position side and account before cancelling competing protection; recheck exposure after cancellation.
- Side-specific cancellation disarms pending synthetic intent. Explicit re-arm can recover a verified cancelled or rejected exit with residual exposure; uncertain outcomes remain held.
- Serialize bracket placement and synthetic exits. Preserve a valid stop crossing during management work and stop remaining target submissions once a trigger is claimed.
- Reject delayed, stale, future-dated, crossed or missing executable quotes before effects.
- Use the shared holiday and early-close calendar for brackets and Stop BE. Revalidate manager quotes and position lifecycle after intervening waits.

Verification: fresh full gates passed 2,834 Beta and 2,854 Developer tests, including all 546 required trading-workflow and 41 safety cases. Independent source/evidence review approved the repairs. Eight bounded Alpaca paper long/short create, cancel, re-arm and manually triggered exit cases passed, with native broker/app order-state comparisons and flat cleanup. Tests used actual Schwab REST quotes and deterministic management proposals; they did not validate AI decision generation or physical chart markers. The initial stale-quote attempt remains recorded as incomplete with verified cleanup.

Limitations: Schwab protection lifecycle, native partial-fill races, on-screen session transitions and clean-machine onboarding remain unverified. The separate owner-operated Schwab one-share entry/exit is not protection acceptance. Synthetic stops require FastDOM running and fresh quotes, do not survive shutdown, and limit exits can remain unfilled. Independent bid/ask field timestamps are unavailable. Unexpected exchange closures require calendar updates.

The installer is unsigned. Close Beta and run the installer to update; settings and activation remain separate. Unchanged installer mechanics reuse same-day isolated install/update/uninstall/hash/guard checks; packaging and public bytes are verified for this build.

Installer: FastDOM-Beta-20261029-172909-482196fa-Setup-UNSIGNED.exe

SHA-256: `cf0d55d210fda20f4f802b6babeddbfbb3ad88f72de626f4f627ae48c10d28f4`

Size: 116,570,085 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/)

## Beta 20261029-160802-998b3762 — October 29, 2026

- Position Manager receives the trading session and existing synthetic stop. Existing protection is preserved or tightened; regular-session native stops are not counted as active after-hours protection.
- New supported extended-hours protection uses an app-managed synthetic stop and limit targets. Verified existing native stop levels transfer to local monitoring at close, including during AI waits and review pauses. Existing orders remain; existing targets are not automatically converted to extended-hours orders.
- Fresh position, quote and order checks guard partial fills, changed exposure, duplicate protection and uncertain acknowledgements. Explicit disarm cannot resurrect an older stop.
- Scheduled equity holidays and early closes are included.

Verification: 104 focused regression tests, 2,820 Beta tests and 2,840 Developer tests passed, including 546 required trading-workflow and 41 safety cases. Independent source/focused review approved the repair. Isolated installer install/update/uninstall verified all 635 installed file hashes; overwrite guards passed. No live orders were sent for this repair's QA.

Not yet verified: native Schwab after-hours execution, on-screen session-transition acceptance, and clean-machine onboarding. Synthetic stops need FastDOM running and fresh quotes and do not survive shutdown. Limit exits can remain unfilled. Exceptional exchange closures require calendar updates.

Correction to the earlier release's limitation: native Schwab spread replacement was verified on the earlier same-day Developer build (seven accepted replacements and broker working readbacks). That evidence does not validate this after-hours repair or replace tests of later guards.

Unsigned Windows x64 installer: 116,568,286 bytes.
SHA-256: `1c85515869e62c7dc1fc70acdbb8333b55c771e7128f59d8ef1d843285a2bc97`.

[Official download and checksum](https://fastdom.decoglobal.us/download) · [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/).
Close Beta and run the installer to update. Settings remain separate.

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
