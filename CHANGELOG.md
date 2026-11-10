# Release notes

## Beta 20261110-111434-93c11bce — published November 10, 2026

Adds the Earnings view (More > Earnings) that merges the Nasdaq, Finviz and Stock Analysis calendars with report timing, estimates, source agreement and a market-cap band filter. The Watchlists manager now shows symbol and company name without streaming quotes; pop-outs show last price and change. Watch charts gain a day-change dot beside the pin, the chart position line shows live P/L and entry pills again, Schwab streamer reconnect storms are prevented, identical history requests share one provider call, and the Watch layout saves reliably. Strategy Center is not included in this Beta.

- More > Earnings: one US trading day at a time merged from three public calendars; notes flag single-source listings and timing or date disagreements; filters for text, timing, market-cap band (Small, Mid, Large, Mega), watchlist symbols and two-or-more sources.
- More > Watchlists: lists capture symbols and company names and hold no quote subscriptions; Pop out streams last price and change while open. Company names are looked up once per list and saved with it.
- Watch: a green/red dot beside each chart's pin shows whether the last price is above or below the previous close; gray when the quote carries no previous close. Layout saving no longer fails on unusual window bounds.
- Charts: live P/L and entry pills are back on the position line. Identical in-flight history requests share one provider call.
- Schwab: streamer connects are cooled down when no streamer URL is available and connect storms no longer block broker switches.
- Strategy Center (ORB deployments with automatic execution) stays in the Developer edition for now; it is absent from this Beta's menu and help.

Free, unsigned Windows x64 Beta. Installer SHA-256 `27fa0c3d67066bc0b032c76ca73b580abc255be377c9a408d2c57a029d550c91`.

## Beta 20261106-165708-d51ce8bb — published November 7, 2026

Includes named watchlists, Watch crosshair support, chart-history range improvements, risk-click stop-limit behavior, and fixes for Take 1, protection resizing and optional Flatten correction. NinjaTrader users should update the bundled bridge through Install / repair, compile with F5 and restart NinjaTrader.

- Optional Flatten correction verifies that the original close has completed and obtains a fresh position before sizing a correction.
- Take 1 coordinates with concurrent Schwab order replacements. Protection resizing accounts for pending exits.
- Updated help covers named watchlists, Watch crosshair, risk-click controls and NinjaTrader history/bridge setup.

Free, unsigned Windows x64 Beta. Installer SHA-256 `46a63f354a1e25d33b4b49a11aa7a839dc046c3a301da83e65477882da2061a9`.

## Beta 20261103-185626-abd525ef — November 3, 2026

- NinjaTrader daily history uses daily-bar counts, and recent charts request the required number of bars directly.
- Subscription initialization runs outside the shared quote-reader lock. Startup avoids a duplicate account-triggered refresh.
- A verified filled or cancelled NinjaTrader order can retire its temporary-ID marker when the bridge returns its permanent ID.
- Includes the earlier Secure Buy/Sell target-spacing fixes and all previous Beta features.
- Update the bundled NinjaTrader bridge using Install / repair with NinjaTrader closed, then compile with F5 and restart NinjaTrader.

Free, unsigned Windows x64 Beta. Installer SHA-256 `04034408dce4c3e38cd6b04d9ae053be5a0a822de62e0ebf261f87f477eedadb`.
Clean-PC installation, native post-update latency and connected-screen marker removal remain pending acceptance.

## Beta 20261103-174246-9ba1a76f — November 3, 2026

- Secure Buy/Sell keeps target spacing based on average entry and the new stop. When targets have been overtaken by the market, the ladder shifts together instead of stacking at one price.
- Secure custom scripts carry the explicitly supplied stop through to the replacement bracket.
- Faster Flatten cancellation handling, post-close verification, and an optional opposite-residual correction setting (off by default).
- Includes all previous Beta features. Free, unsigned Windows x64 installer; close Beta before updating. Saved settings remain separate.

Installer SHA-256: `2cd11c5caf66002d349f270926533e6a341041c52764f8cad081a50bb3cb2ef3`.
Clean-PC and native broker acceptance of this build remain unverified.

## Beta 20261102-154235-a47a1bc2 — November 2, 2026

**Options Trader**
- Close existing spread: choose 2–4 option contracts you hold and close them together as one order at a single net price, instead of closing each leg separately (Schwab).
- Spread fills now show the true net price of the spread.
- The scanner shows expected value after costs (MKT EV), which is never positive at market prices. You can enter a thesis: your expected price at expiration and how unsure you are. The scanner then lists only spreads expected to profit after costs if the thesis is right, and otherwise says No trade. THESIS EV is only as good as your thesis.
- AI scores in the scan list and the ticket now agree for the same spread and quotes.

**Trading and protection**
- Closing FastDOM while virtual stops are active now asks for confirmation, because virtual stops are lost when the app closes.
- Schwab Take 1, order replacement and cancel results are reconciled against the exact original order.
- Chart stops are always red and targets always green, for long and short positions.
- Bracket orders play one placement sound instead of one per target, and regular DOM orders play their sound again.

**Layout**
- Hot buttons: Arrange mode lets you drag buttons into the slot you choose. Cancel All is no longer a default button on new installations.
- Charts fit smaller screens while keeping the original layout on wide windows.
- Long option names in Positions are no longer cut off.

The NinjaTrader bridge is unchanged since the previous Beta.

Free, unsigned Windows x64 Beta. Close Beta before installing; saved settings remain separate. Start new installations in Simulation.

- Installer: `FastDOM-Beta-20261102-154235-a47a1bc2-Setup-UNSIGNED.exe`
- SHA-256: `c707fa99c8ae1c0df8edbdebe7593e639755aa1f25a5b44d62333e999d6887a2`
- Size: 116,661,127 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/) · [Disclaimer](https://fastdom.decoglobal.us/disclaimer)

## Beta 20261101-165644-99f44760 — November 1, 2026

- Schwab sign-in now waits for an already-started redirect when it takes longer than the browser action timeout. It does not click again or resubmit credentials during that wait.
- Callback validation and cancellation remain enforced. This addresses a reproduced intermittent failure at confirmation; it does not bypass Schwab identity verification or guarantee that every sign-in will succeed.

24 focused browser regressions, 3,095 Beta tests and 3,115 Developer tests passed, including 700 trading-workflow and 41 safety cases. Independent review completed. The Developer build restarted connected to Schwab with account data populated. No test orders were submitted. Delayed redirects were tested with synthetic browser responses; clean-PC acceptance of this new installer remains for the owner to perform. Installer mechanics are unchanged; prior November 1 install/update/removal and guard evidence is reused.

Free, unsigned Windows x64 Beta. Close Beta before installing; saved settings remain separate. Start new installations in Simulation.

- Installer: `FastDOM-Beta-20261101-165644-99f44760-Setup-UNSIGNED.exe`
- SHA-256: `173ba9571ecc86d3677b0e1169ecd5d69c77c970c6102b499cc8cb83fbe779f7`
- Size: 116,603,946 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/) · [Disclaimer](https://fastdom.decoglobal.us/disclaimer)

## Beta 20261101-143121-4e7c1c09 — November 1, 2026

- Trading and Market Data each show their own authorization status, renewal date and expiry date. Status refreshes when application details are saved. Green describes the matching local authorization window, not a live connectivity check.
- Schwab recovery rechecks both applicable authorizations after each renewal, so a newly discovered Data-key failure joins the same flow. Completed steps are retained on retry. Main-window recovery reconnects on completion/close; Configuration recovery retains its existing reconnect behavior.
- Includes the earlier dedicated-profile trust repair and sign-in retention changes. Manual two-factor verification remains user-controlled.

Verification: 3,091 Beta and 3,111 Developer automated tests passed, including 700 trading-workflow and 41 safety cases. Live expired-key renewal and clean-PC acceptance of this update remain unverified. No broker orders were submitted. Unchanged installer mechanics reuse the November 1 install/update/removal and guard checks; this package and public download are verified separately.

Unsigned Windows x64 Beta. Close Beta and run the installer; settings and activation remain separate.

- Installer: `FastDOM-Beta-20261101-143121-4e7c1c09-Setup-UNSIGNED.exe`
- SHA-256: `8654c04dd1a27e09a7bd7599a251b120fdf969d7fb892e49bc1c01041fdc4e46`
- Size: 116,603,364 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/)

## Beta 20261101-093020-f08b0c8f — November 1, 2026

- **Trust / repair sign-in browser** now uses Schwab's normal client sign-in page instead of opening the internal SWS gateway route directly. This fixes the blank Schwab shell that could appear when the repair action was opened a second time.
- The same dedicated FastDOM browser profile is retained. Extensions and DevTools remain disabled for the repair window; manual login and two-factor verification remain user-controlled.

Verification: 3,082 Beta and 3,102 Developer tests passed, including 700 trading-workflow and 41 safety cases. Focused Schwab authentication tests passed 64/64, including two consecutive production-path repair launches. Installer install/update/uninstall and destination guards passed. No broker or order test was run.

Unsigned Windows x64 Beta. Close Beta and run the installer; saved settings and activation remain separate.

- Installer: `FastDOM-Beta-20261101-093020-f08b0c8f-Setup-UNSIGNED.exe`
- SHA-256: `52a2e27f5a77fc8c0b17d0856de786ff504621c6137269ed09985f60edb4841b`
- Size: 116,597,107 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [Complete manual](https://github.com/ipolyako/fastdom/blob/main/docs/manual.md)

## Beta 20261101-090512-8ee666bb — November 1, 2026

- On a new Windows installation, **Remember sign-in securely for this Windows user** now starts selected. The choice remains visible and can be cleared before sign-in. Credentials are protected by Windows for that user and machine; they are not transferred between PCs.
- **Trust / repair sign-in browser** now opens FastDOM's dedicated profile in a clean window with restored extensions and DevTools disabled. This avoids extension or restored DevTools state interfering with manual device-trust recovery while preserving the same FastDOM profile.
- The recovery sequence remains: complete manual Schwab login and two-factor verification, close the repair browser, then retry automatic authorization once. FastDOM does not automate 2FA or retry rejected credentials.

Verification: 3,081 Beta and 3,101 Developer tests passed, including 700 trading-workflow and 41 safety cases. Focused Schwab authentication tests passed 69/69. Installer install/update/uninstall and destination guards passed. Native device-trust recovery on the reporting clean PC remains the acceptance step; no orders were submitted.

Unsigned Windows x64 Beta. Close Beta and run the installer; saved settings and activation remain separate.

- Installer: `FastDOM-Beta-20261101-090512-8ee666bb-Setup-UNSIGNED.exe`
- SHA-256: `8ca5f1f5357a433bfbe158c9f56b029f9efc0f120ef66bccd4ab475ca9eb85dc`
- Size: 116,597,087 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [Complete manual](https://github.com/ipolyako/fastdom/blob/main/docs/manual.md)

## Beta 20261101-082038-0924b1ee — November 1, 2026

- Schwab automatic authorization now shows the same explanatory Trading Key and Data Key introduction screens as the manual flow.
- The informed-consent modal is accepted before the still-present terms controls, matching Schwab's current page order.
- A new **Trust / repair sign-in browser** action opens FastDOM's exact persistent sign-in profile as a normal browser. On a new PC, or after Schwab device trust is lost, complete manual login and two-factor verification, close that browser, and retry automatic authorization once.
- HTTP 403 and the visible “Login is temporarily unavailable” page stop automatic submission and enter the guided repair path. FastDOM does not automate two-factor verification or retry rejected credentials.

Verification: 3,081 Beta tests passed, including 700 trading-workflow and 41 safety cases. Focused Schwab authentication tests passed 65/65. Installer install/update/uninstall and destination guards passed. The owner is the independent release reviewer. Native clean-machine Schwab authorization remains pending on the owner's second PC; no orders were submitted.

Unsigned Windows x64 Beta. Close Beta and run the installer; saved settings and activation remain separate.

Installer: FastDOM-Beta-20261101-082038-0924b1ee-Setup-UNSIGNED.exe  
SHA-256: `0115f9d1bd2163a489688eaab58d02e999f0634ff62a0acd5f972b8104470d64`  
Size: 116,596,917 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [Complete manual](https://github.com/ipolyako/fastdom/blob/main/docs/manual.md)

## Beta 20261031-172834-20ac0e43 — October 31, 2026

- Updated offline Help, public documentation and hosted Ask FastDOM knowledge for Codex and Claude Code, current Momentum Scan controls and risk-script input requirements.
- Provider-specific setup and troubleshooting; Partner and Market Desk refresh their model/path controls on the next request after switching providers. Learn resolves a compatible model.
- AI requests retain their provider through readiness and response processing. Active Manage keeps its original provider/path/model until disengaged and restarted; order validation and protection rules are unchanged.
- Hosted Ask FastDOM remains a separate service. Local CLI means cloud inference through your own account, not offline models. Provider allowances, authentication and terms apply.

Verification: 3,069 Beta and 3,089 Developer tests passed, including 700 trading-workflow and 41 safety cases; 134 focused AI checks and 26 hosted-support tests. Independent source review completed. No live or paper orders were submitted. Native provider inference and clean-PC onboarding remain unverified. Unchanged installer mechanics reuse the earlier October 31 installation/update/removal and guard checks; this exact package and installer hashes were verified separately.

Unsigned Windows x64 Beta. Close Beta and run the installer; saved settings and activation remain separate. Synthetic stops require FastDOM running and fresh quotes.

Installer: FastDOM-Beta-20261031-172834-20ac0e43-Setup-UNSIGNED.exe
SHA-256: `0ad8d7613488ba452fdd54f04e9e9c7fb0c7afe5b2f6934fcffbbb478dcc9433`
Size: 116,590,967 bytes.

[Official download](https://fastdom.decoglobal.us/download) · [AI setup guide](https://fastdom.decoglobal.us/ai-providers.html) · [Complete manual](https://github.com/ipolyako/fastdom/blob/main/docs/manual.md)



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

Download and checksum are published on the [official download page](https://fastdom.decoglobal.us/download). The installer is unsigned. Existing saved settings are preserved.

## Beta 20261026-004726-eea7c609 — October 26, 2026

The current public installer includes the earlier installation and packaging fixes, a MACD/cumulative-delta chart crash repair, and options-view improvements: readable Levels selection, a responsive visible-strike count and correctly grouped call/put columns.

Installer SHA-256:

```text
a24944c390864f3a3fa78f817c37e42e9967098e0273518fb6026136a4f5c54d
```

Download and checksum are published on the [official download page](https://fastdom.decoglobal.us/download). The installer is unsigned. Newer training lessons can show display improvements not yet in this public installer; their build notes identify that distinction.

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
