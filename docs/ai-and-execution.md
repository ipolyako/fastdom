# AI, sizing, and execution in FastDOM

FastDOM brings the conversation about a trade, the size calculation, order entry, and position management into the same workspace.

## Discuss an idea before acting

**Trading Partner** is a focused thesis workspace. Ask about a long or short idea, compare taking a trade with waiting, discuss an existing position, and challenge the assumptions behind your plan.

Example questions:

- What evidence supports this thesis, and what would invalidate it?
- What is the case for the opposite direction or for waiting?
- What should I review before adjusting this position's protection?

**Market Desk** supports broader research conversations about market conditions, relative strength, catalysts, watch planning, and trading history. **Learn** provides AI-assisted review of available trade evidence, while **Check Trend** reviews completed-candle trendline anchors.

These tools analyze the evidence supplied to them. Partner and Desk do not execute the suggestions they discuss. A fresh AI response can still rely on incomplete or stale source data; inspect timestamps and missing context.

## Delegate supported position management explicitly

The chart's **Manage** control is active AI position management for an existing position. Confirm the chart's account, symbol, open position, working protection, and data freshness, then enable it deliberately.

Manage uses the chart-selected model and current evidence to propose supported protection adjustments. Proposals pass through deterministic validation, the order service, risk checks, and broker-state verification. They may be rejected or withheld. If the account is flat, Manage does not open a new position for you.

Monitor its status and broker-accepted orders. You can stop its lifecycle, and it disengages when flat. Stopping Manage is separate from canceling broker-held protection. Connectivity, supported broker behavior, and model availability affect what can be completed.

## Size from a risk budget

**Risk Buy/Sell** uses your intended risk and stop reference to calculate quantity. For a simple share example, a $100 risk budget with a $0.50 entry-to-stop distance corresponds to 200 shares before fees, slippage, and other constraints. Futures and other contract instruments require their applicable point/tick values and sizing rules.

Set your risk amount, stage the stop or supply it when prompted, verify the proposed quantity and direction, then use the intended Risk action. Smaller stop distances can produce much larger quantities. After a fill, verify the actual position and accepted protection.

The nominal risk budget is a sizing input, not a guaranteed loss ceiling. Gaps, fill prices, slippage, fees, and rejected or unavailable protection can change the actual result.

## Size from a specific trade amount

Dollar-amount hot buttons calculate quantity from a configured trade value and reference price. For a simple share example, $5,000 at $50 per share corresponds to 100 shares before execution effects. This is position value, not $5,000 of stop-loss risk.

Choose between amount-based sizing, risk-based sizing, fixed quantities, and supported position-percentage exits. Review the selected button's actual script and instrument behavior; its label can be customized independently of its execution definition.

## Move from decision to execution with fewer manual steps

Use chart trading, the DOM ladder, hot buttons, and keyboard shortcuts for repeatable order-entry workflows. Configure frequent actions such as bid/ask limit entry, risk-sized entry, partial exits, cancellation, stop adjustments, and flattening.

FastDOM's speed proposition is direct access to configured actions and less repetitive manual entry. It is not a measured promise to beat another platform's latency. Broker response times, network conditions, market liquidity, and order type determine acknowledgment and execution.

A configured button can contain multiple operations; they are not necessarily one atomic broker action. Confirm the account, instrument, quantity, and actual order state. Practice the complete workflow in Simulation or an appropriate paper environment first.

## Automatic session handling and protection sizing

In Risk/Secure equity workflows, FastDOM detects the trading session and adapts supported order handling automatically, without a separate regular-hours or after-hours mode choice.

When native stop/OCO orders are unavailable after hours, FastDOM pairs broker-held limit targets with an app-managed virtual stop for OCO-style protection. On a stop trigger it cancels targets, confirms cancellations, checks the remaining position and submits a closing limit order. Virtual stops require FastDOM to stay running, connected and receiving current quotes; gaps, liquidity and broker/session rules still matter.

Position size follows broker-confirmed fills. With protection reconciliation enabled, FastDOM automatically resizes existing stop and target quantities as you add to or sell down a position. Verify broker-accepted protection after changes.

## AI setup

Chart AI, Trading Partner, and Market Desk require your installed, signed-in Codex CLI and provider access. Ask FastDOM support chat can use hosted AI instead. Hosted support chat is a separate help feature; it does not provide active position management.

[Return to the showcase](../README.md) · [Getting started](getting-started.md)
