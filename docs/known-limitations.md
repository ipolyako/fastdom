# Beta status and known limitations

- The installer is unsigned. Windows or organizational security policies may block it.
- Clean Windows-machine acceptance and customer broker onboarding remain under verification. Packaging tests on the development PC do not establish compatibility with every installation.
- The previously reported intermittent chart-focus crash remains under real-use verification.
- Initial Beta activation requires internet access. The current service policy permits a previously issued offline lease for up to seven days. Access can be restricted or discontinued.
- Restricted Beta access does not automatically cancel broker orders or liquidate positions. Review broker-reported orders and positions independently.
- Updates are manual and preserve existing settings. The safer fresh-install defaults do not reset an existing user's account permissions or contract mappings.
- Broker authorization, account eligibility, data entitlements, and third-party service availability are separate from FastDOM activation.
- NinjaTrader requires a separately installed and running NinjaTrader 8 environment and matching bridge. Configure futures contracts explicitly and review them at rollover.
- Optional automatic Schwab sign-in depends on a compatible local browser and may require manual identity verification. Manual browser authorization remains available.
- Chart AI depends on the user's own Codex or Claude Code setup. Hosted support chat depends on FastDOM's service. Neither is a guarantee of trading accuracy or returns.
- Legacy Morning Scanner and unfinished archive capabilities are excluded from the default Beta feature profile. Retired Phantom/Ghost Candle features are not included.

Please report reproducible problems using the issue templates. Share sensitive diagnostics privately, never in a public GitHub issue.


See [Codex and Claude Code setup](ai-providers.md) and the [complete user manual](manual.md) for authentication, model selection, usage limits, hosted support and provider-switch behavior.
