# Market Movers and Momentum Scan

Open Market Movers & Scanner to discover symbols without changing your trading broker or account. Selecting a row loads the symbol; it does not submit an order.

## Where results come from

FastDOM first tries the selected broker's native discovery APIs: Schwab equity movers, or Alpaca gainers, losers and most-active stocks. Using NINJA MD keeps discovery on the primary broker. If native discovery is unsupported, unavailable, empty or times out, FastDOM uses its existing fallback. The Source line names the successful source and explains fallback.

These are limited ranked lists, not an exhaustive market search. Alpaca requests up to 50 gainers, 50 losers and 100 active stocks. Its native rankings use SIP; missing fields are enriched from IEX snapshots. Missing volume excludes a symbol from Momentum Scan. Until market open, Alpaca movers can describe the previous market day. Displayed data can be delayed or cached.

Fallback can use available directory quotes, Yahoo ranked lists, or optional configured Massive/FMP data services. You do not need a Massive or FMP subscription to use the screen. Your existing broker entitlements and connectivity still apply.

## Choose a price range

The former FAST < $30 tab is now **Momentum Scan**.

1. Set **Min price** and **Max price** (inclusive).
2. Click **Apply** to filter the loaded results. This does not fetch new symbols.
3. Use **Refresh** to reload discovery. Your applied range is retained while the window stays open.

Defaults are $1–$30. Positive sub-dollar prices and equal minimum/maximum values are supported. Closing and reopening the window resets the default range. Invalid input retains the last valid range and results.

Other momentum filters still apply: at least +5% change, 100,000 shares of volume, $500,000 dollar volume, and a quoted spread no wider than 2% when available. An unknown spread is included and shown as a dash. Results are scored and sorted locally. A wider price range cannot reveal symbols absent from the loaded discovery source.

The other tabs show gainers, most-active stocks and losers within the available coverage. No scan result guarantees a trading opportunity or future performance.
