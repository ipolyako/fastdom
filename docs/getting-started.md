# Getting started with FastDOM Beta

## Install

Download from https://fastdom.decoglobal.us/download and verify the published SHA-256. Run Setup, then open FastDOM Beta from Start. The installer includes .NET and installs separately from the Developer edition. It does not launch the app automatically.

Fresh installations start in Simulation using SQLite, with live trading disabled. Initial Beta activation needs internet access. There is no FastDOM signup or payment step. Beta activation does not authenticate you with a broker or provide a data subscription.

Use **More > Help** for the detailed, searchable offline guide. Explore simulated order entry, cancellation, and position controls before connecting an account.

## Configure a connection

### Schwab

Open **Configuration > Brokers > Set up Schwab applications**. Supply your own approved Accounts and Trading Production and Market Data Production application credentials. Register the callback shown by setup in both applications and complete both browser authorizations.

Manual authorization opens your default browser. Optional automatic sign-in requires installed Playwright Chromium or Microsoft Edge; browser binaries are not bundled. No developer TokenRenewal task or shared browser profile is required.

### NinjaTrader

Install NinjaTrader 8 separately and follow the bundled `integrations/NinjaTrader/NinjaTrader-Setup.txt`. The installer supplies the matching FastDOM bridge source for import into NinjaTrader; it does not install NinjaTrader itself.

Fresh Beta defaults permit simulation/playback accounts and have no preset personal account or futures contract mappings. Configure the exact contracts you intend to use and review them at rollover. Keep live-account access disabled while testing.

**NINJA MD changes market data only. It does not change the selected trading account or order destination.** Required market depth and trade data must be supplied by the connected feed.

### Alpaca

Configure your own API credentials under Brokers and verify whether each connection uses a paper or live endpoint. Data access depends on your subscription. Begin with paper trading; do not assume a working account connection provides full market depth.

See the dedicated [Alpaca setup guide](alpaca.md) for the connection checklist and data limitations.

## Optional AI

Chart Codex features require your own installed, signed-in Codex CLI and provider access. Ask FastDOM support chat can use hosted AI instead. Select the provider in chat. Do not enter credentials or authorization codes into any AI prompt.

## Settings and updates

Settings and activation are stored in `%LOCALAPPDATA%\FastDOM\Beta`, separately from the installed program. Keep that folder private.

Close Beta before running a new installer. Updates preserve saved settings; uninstall also retains them. Automatic updates are not implemented. Recheck broker identity, contract mappings, data freshness, and risk settings after an update.

No profitability or live-trading acceptance is implied by successful installation. Read [known limitations](known-limitations.md) and the in-app Help before connecting a live account.
