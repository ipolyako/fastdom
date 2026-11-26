# FastDOM

FastDOM is a free Windows trading application I’m building for **Schwab, NinjaTrader, and Alpaca**. It combines chart and Depth of Market (DOM) order entry, risk-based sizing, and optional Codex or Claude tools. It’s currently in beta, and I’m looking for feedback on usability and reliability.

The AI tools can help review a trade idea or available market data. **Manage** is different: when explicitly enabled for an existing position, it can propose protection changes through the app’s validation and execution controls.

[Beta download](https://fastdom.decoglobal.us/download) · [Getting started](docs/getting-started.md) · [User manual](docs/manual.md) · [Known limitations](docs/known-limitations.md) · [Training videos](https://fastdom.decoglobal.us/training)

## Features

| Capability | Description |
| --- | --- |
| **Discuss trade ideas with AI** | Use Trading Partner to question a long/short thesis, consider invalidation, compare alternatives, and discuss managing an existing position. Use Market Desk for broader research and watch planning. |
| **Active AI trade management** | Explicitly enable Manage on an open position to review current evidence and propose supported protection adjustments. Accepted actions pass through order validation, risk checks, and broker verification. |
| **Chart and DOM order entry** | Enter and manage orders from the chart or DOM, with configurable hot buttons and keyboard shortcuts for frequent actions. |
| **Trade by dollar risk** | Set a risk budget and stop reference; Risk Buy/Sell calculates quantity from the entry-to-stop distance and relevant instrument value. |
| **Trade a specific amount** | Configure dollar-amount hot buttons to calculate an order size from your intended trade value, or use fixed quantities and size presets. |
| **Automatic session handling** | Risk/Secure equity workflows adapt supported regular/extended-hours handling; virtual stops provide app-managed OCO-style protection when needed. |
| **Protection that follows position changes** | With reconciliation enabled, existing stops and targets resize from broker-confirmed additions and reductions. |
| **Order-flow context** | Explore footprint and liquidity heatmap views when your feed supplies compatible depth and execution data. |
| **Workspace configuration** | Configure buttons, shortcuts, indicators, and layouts; review orders and positions alongside the chart. |

**Dollar risk and trade amount are different:** a $100 risk budget describes intended loss to the stop; a $5,000 trade amount describes intended position value. Actual fills, rounding, instrument multipliers, fees, gaps, and slippage affect the result. Neither is a guaranteed maximum loss or exact fill value.

AI discussions in Partner and Desk are advisory. **Manage is execution-capable**, requires an existing position and explicit activation, and disengages when flat. Execution speed depends on the broker, network, and market; no latency or fill-quality guarantee is claimed.

[AI, sizing, and execution documentation](docs/ai-and-execution.md)

## Other tools

- **Watch:** compare up to 24 symbols in a tiled chart wall.
- **Market Pulse:** align volatility, resting-book imbalance, and executed-trade delta across time.
- **Trade Copier:** deliberately enable supported action replication to follower accounts, with per-account sizing multipliers and execution status. Followers can receive real orders and can fill differently.
- **Options Hedging Map:** inspect estimated option-chain positioning and related chart levels, with coverage and model assumptions visible.
- **Margin monitor:** explore maintenance headroom and adverse-move sizing scenarios as planning estimates.
- **Performance and Learn:** review execution-based results, then discuss available trade evidence with AI.

## Workflow comparison

The [workflow comparison with thinkorswim and DAS](docs/platform-comparison.md) describes differences and links to sources. It does not claim measured speed or fill-quality advantages.

## Screenshots

### Footprint

![FastDOM footprint chart showing bid and ask volume at price](assets/footprint.png)

### Liquidity heatmap

![FastDOM liquidity heatmap and market-depth display for a futures instrument](assets/bookmap.png)

Screenshots illustrate the interface and historical market data. They are not performance claims; appearance and available features can vary by build and feed.

## Connections and requirements

| Connection | What you supply |
| --- | --- |
| Simulation | No broker account needed to explore the simulated workflow |
| Schwab | Your approved trading and market-data developer applications and browser authorization |
| NinjaTrader | NinjaTrader 8, the supplied FastDOM bridge, an active account/feed, and appropriate data entitlements |
| Alpaca | Your own account API credentials and the appropriate paper/live configuration; [setup guide](docs/alpaca.md) |

The installer is for **Windows x64** and includes the .NET runtime. Default SQLite storage does not require Python, Java, or a Derby server. Market-depth and executed-flow tools depend on the upstream data available to your account. Broker/data charges may apply; no broker endorsement is implied.

Chart AI features use your selected provider: your own installed, signed-in Codex CLI or Claude Code CLI. Hosted Ask FastDOM support chat does not require either local CLI. Offline Help requires neither AI access nor an internet connection.

## Installation

1. Download the installer from the [official download page](https://fastdom.decoglobal.us/download).
2. Compare its SHA-256 with the checksum on that page.
3. Install, then launch **FastDOM Beta** from the Start menu.
4. Start in **Simulation**. Fresh installs have live trading disabled.
5. Open **More > Help** before configuring your own broker connection.

This early Beta is **unsigned**. Windows may display an unknown-publisher warning or prevent installation under your security policy. Review the [known limitations](docs/known-limitations.md) before using it.

## Current release

**Beta 20261126-083246-dd091206** — November 26, 2026.

This build is a correction release: a full review of the program, and the faults it found. Orders: the Buy and Sell buttons size the order from the Amount box, and with no quote yet for the symbol (the moment after a symbol change) the order used to go out with the Size box quantity instead; now nothing is sent and the button says a price is needed. Reverse outside regular hours is sent as a limit at the quote instead of cancelling the exit orders and then being refused. A partial close that takes one target whole and part of the next trims the next one. Stop BE on a losing position with no stop working is refused instead of arming a virtual stop that would fire at once. Keyboard: a held shortcut key runs its button once, not repeatedly; the built-in Emergency binding (Ctrl+Shift+E twice) now flattens the symbol, it did nothing before; a built-in binding you delete stays deleted; combinations with Alt work. DOM: "Cancel Orders at this Price" on the best bid or ask cancels only the orders on that row, and "Cancel All Buy/Sell Orders" includes stops. Chart: a click on an order marker no longer moves the order, a drag starts after a few pixels, and where markers overlap the one on top is taken. On a PC set to Eastern time the opening range, the shading of extended hours and the pre-market high and low are at the right hours, and the chart accepts market orders and stops in the last hour of the session. Closing a chart cancels a resting Risk limit entry it was watching, because that chart attaches the stop when the entry fills. Schwab: a day order entered after the close stays visible through its own session; the quote stream keeps trying to reconnect; moving the target of a bracket with a stop-limit stop moves the target. Scans: a row click sends the row you pressed even when the list re-orders at that moment; the Screener keeps your sort and your selected stock from run to run, and a scan no longer interrupts "Choose filters"; when Finviz Elite is not answering, scans slow to once a minute. AI: the model chosen in Configuration is now saved; the account identifier is no longer included in Position Manager and Trade Review requests; an AI trailing stop checks its level against the price at the time of the answer. Alpaca: long intraday charts reach today, daily bars sit on their own date, option strikes read correctly on any regional format. NinjaTrader: pressing Connect again no longer doubles the polling; two contract months of one root are both shown. Hot-button scripts read numbers with a decimal point on any Windows regional format.

Also in the current build, from November 24: the built-in percentage buttons are two-way (Buy/Cover and Sell/Short 10%, 25%, 50%); Quick scans (More > Quick scans) with ordering by column and a price filter; the News window with the full Finviz headline timeline. From November 22: Volume Profile on the chart; chart drawing mode with Arrow tools; one AI model per provider in Configuration; a Validate button for the Finviz Elite token.

See the [changelog](CHANGELOG.md), [official download](https://fastdom.decoglobal.us/download), [SourceForge mirror](https://sourceforge.net/projects/fastdom/files/beta/), and [disclaimer](https://fastdom.decoglobal.us/disclaimer).

## Feedback and support

Use **Issues** for reproducible bugs and feature requests, and **Discussions**, when enabled, for setup questions and general feedback. Include your Beta build ID, Windows version, steps to reproduce, and the visible error.

**Never post account numbers, balances, positions, credentials, tokens, databases, activation files, or unredacted screenshots.** For private support, contact [support@decoglobal.us](mailto:support@decoglobal.us). See [SUPPORT.md](SUPPORT.md).

## AI access

FastDOM’s Codex-powered trading tools can use your existing eligible ChatGPT plan through Codex CLI. Sign in with your own account—no separate OpenAI API key is required when using subscription access. This uses your included Codex allowance instead of separate usage-based API billing.

You control when to request analysis, which supported model to select, and whether to enable active position management. Trading tools remain available without AI. Requests consume your plan allowance; model access and usage limits apply. API-key authentication, if chosen, is billed separately. Hosted Ask FastDOM support chat is a separate service. Local CLI execution still sends AI requests to the provider.

See [official Codex authentication documentation](https://learn.chatgpt.com/docs/auth). Claude Code is also selectable in Configuration; it requires your own working, signed-in Claude Code CLI.


### Set up Codex or Claude Code

Choose **Configuration > General > AI PROVIDER**, install the selected CLI, and sign in under the same Windows user. Codex uses `codex login`; Claude Code uses `claude auth login`. Existing CLI sign-in is reused. Validate installation, then explicitly retry the AI action. FastDOM does not install the CLI or sign you in automatically.

[Download Codex desktop](https://chatgpt.com/download/) · [Codex CLI instructions](https://developers.openai.com/codex/cli/) · [Claude Code instructions](https://code.claude.com/docs/en/setup) · [Full provider guide](docs/ai-providers.md)

## Availability and licensing

FastDOM is free. There is currently no paid version or FastDOM subscription. This repository contains documentation and release information; the application source is not published under an open-source license. Beta access may be restricted or discontinued. FastDOM does not promise trading returns.

Copyright 2026 DECO GLOBAL SERVICES, INC. All rights reserved.
