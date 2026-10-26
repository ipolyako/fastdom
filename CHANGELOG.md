# Release notes

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
