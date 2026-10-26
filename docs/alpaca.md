# Alpaca setup

FastDOM supports Alpaca account connections using your own API credentials. Start with an Alpaca paper account to test the workflow.

1. Install FastDOM Beta and explore Simulation first.
2. Open **Configuration > Brokers** and configure an Alpaca account connection.
3. Enter that account's API key and secret privately in the app. Select the correct paper/live setting for those credentials.
4. Save the configuration and select the intended Alpaca connection.
5. Check that the displayed account and paper/live setting match your intent. Verify connection status and advancing quotes before testing order entry.
6. Review your risk limits and practice order entry, cancellation, and position controls in the paper environment before considering live use.

Each configured account has its own credentials and paper/live setting. A successful connection does not establish that live trading is enabled or that every instrument and data product is available.

## Market data

Alpaca data access depends on your account and subscriptions. Its FastDOM connection provides Level 1 data, not a full Level 2 order book. Depth-dependent views need a compatible depth source; an ordinary quote is not full market depth.

If you configure NinjaTrader market data separately, **NINJA MD changes the data feed only**. Orders still belong to the selected trading account. Confirm both selections explicitly.

## Keep credentials private

Never put Alpaca API keys or secrets into GitHub issues, screenshots, AI prompts, or support attachments. When reporting a problem, include the FastDOM build, Windows version, whether the connection is paper or live, and the redacted error text.

Alpaca accounts, market-data subscriptions, and any applicable broker fees are separate from FastDOM's free Beta. No Alpaca endorsement is implied. Paper results do not establish live performance.
