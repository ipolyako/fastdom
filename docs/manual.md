# Start here | Welcome and first-session checklist
FastDOM combines order entry, charting, market depth, tape, options context, archives, and optional AI tools in a Windows desktop application. This guide describes the current shared Developer/Beta code. Availability depends on your build, broker, permissions, data subscriptions, and configured services. A visible control does not prove its data source is connected.

## Learn the terminal in this order
1. Read Trading account versus market data before changing connections.
2. Configure your broker. For Schwab, complete both application authorizations; accounts appearing is only the trading half of setup.
3. Confirm the selected account, symbol, position quantity, buying power, and quote timestamp. Compare positions and working orders with the broker's own interface.
4. Open a chart and verify history loads. Enable only a few indicators initially. Open Time & Sales and depth views if your feed supplies those data types.
5. Review order size, hot-button scripts, keyboard bindings, flatten offset, and protection templates before using any live order control. Button labels can be customized and are not a complete order specification.
6. Use Simulation or a broker paper account to learn the controls. FastDOM Simulation is not proof of a live broker's fill behavior, market-data entitlements, or supported order combinations.
7. Add optional AI (Codex or Claude Code), audio, SMTP alerts, and archives after the basic connection is working.

## Using this help
Open More > Help. Search matches all words anywhere in a topic, not just its title. For example, search "Schwab chart", "risk stop", or "Camarilla". Home restores all topics. A− and A+ change reading size. Copy topic copies the current article. Ctrl+F focuses search; Escape closes Help. Help is offline and does not connect to a broker, send orders, or invoke AI.

## Three kinds of feature
**Display and analysis:** charts, indicators, Watch, depth, tape, options analytics, Check Trend, Partner, Desk, and Learn primarily present information.

**Manual execution:** DOM clicks, order tickets, hot buttons, keyboard shortcuts, Flatten, Take 1, stop/target changes, and chart order commands can affect real orders immediately.

**Active management:** Manage, explicitly enabled Momentum Swing Auto-Trade, protection reconciliation, and Trade Copier can produce additional order actions. Read their individual topics before enabling them. Squawk is audio narration, despite its AI badge.

# Setup | Trading account versus market data
The selected broker mode and account own your orders, positions, buying power, and account history. The market-data provider supplies quotes, trades, depth, and other observations. These are separate responsibilities.

## What NINJA MD changes
The NINJA MD checkbox requests the effective NinjaTrader feed for live quotes, native trades, depth, Footprint, and Bookmap. It does not move your trading account to NinjaTrader. A Schwab account can remain the order destination while the display consumes Ninja data. Conversely, selecting a different broker changes the trading connection; it is not merely a display preference.

Before every order, read the selected account and symbol. Do not infer the destination from the color of a chart, the open window, or the source of its candles. Futures aliases and contract mappings must refer to the intended contract month.

## Different data can succeed independently
Account access does not prove market-data authorization. Historical candles do not prove a live stream is running. A best bid/ask quote does not prove full Level 2 depth is available. A loaded options chain does not prove native trade classification is available. An archived chart can remain visible after a disconnection.

Use provider labels, timestamps, quote age, and activity messages together. If a panel is blank, identify which data class it needs before repeatedly reconnecting everything. Market closure, a quiet symbol, an entitlement issue, and failed authentication are different conditions.

## Switching brokers
Select the desired enabled broker, allow account discovery to finish, then select the correct account. Confirm positions and buying power again. If switching away and back leaves the account selector empty, stop using execution controls, inspect the activity message, and use that broker's reconnect/setup flow. Existing orders remain a broker concern; a disconnected view is not a cancellation.

# Onboarding | Schwab: register, create two keys, and connect
Use this walkthrough for a first-time FastDOM installation with your own Schwab brokerage account. You need a developer portal account, two approved applications, and two browser authorizations. Accounts/positions and market data are separate connections: completing only trading will not make charts work.

## 1. Register your developer account
Open https://developer.schwab.com/ and choose account registration. Complete the requested details, then follow the time-sensitive email verification link. Finish registration and sign in to the Developer Portal. If you already have a portal account, use it.

Choose **Individual Developer** on the welcome page and Continue. If you skipped that choice, open Profile, locate Individual Developer, and choose Add Individual Developer Role. Schwab requires a brokerage account for Trader APIs. The developer profile manages API applications; it does not create a brokerage account.

## 2. Request access to the Trader API products
Open API Products and find **Trader API - Individual**. Review Schwab's terms and request access as prompted. Wait until your profile is approved to create apps for the relevant products. An unapproved request is not an error FastDOM can fix. Check the portal for status; approval time is controlled by Schwab.

You need both **Accounts and Trading Production** and **Market Data Production**. The first supplies account access and trading; the second supplies market data. Follow the portal's access prompts for both products.

## 3. Create the trading application
Open Dashboard > Apps > Create App.

![Open the Apps dashboard and click Create App. Existing registrations are hidden in this example.](SchwabPortalCreate.png)

Enter a recognizable application name, for example **TraderApp**. This name is your choice; it is not a credential.

Select **Accounts and Trading Production**. For Callback URL, paste this exact value:

**https://auth.decoglobal.us/fastdom/v1/callback**

Leave **Order Limit** at **120** as shown. Description is optional.

![Trading application: production product, order limit, example name, callback, and Create button.](SchwabPortalTrading.png)

Submit the application. Select the production product, and follow any approval steps shown by Schwab. Do not substitute a sandbox app for a production connection.

## 4. Create the market-data application
Return to Dashboard > Apps > Create App. Use a different descriptive name, for example **MarketDataApp**. Select **Market Data Production** and enter the same callback URL:

**https://auth.decoglobal.us/fastdom/v1/callback**

Leave **Order Limit** at **120** as shown and leave Description blank if you wish.

![Market-data application: create a separate app with the same callback.](SchwabPortalData.png)

Submit. You should now have two separate apps, each with its own Client ID (App Key) and Client Secret. Do not use the trading app's key in the market-data column.

## 5. Check approval and collect the two credential pairs
On Apps, find both applications. In the example dashboard, the usable status is **Ready For Use** and Environment is **Production**. Pending apps may appear under Apps Pending Approval. Wait for approval before attempting the FastDOM connection.

![Both apps must show Ready For Use. Open View Details separately for each credential pair.](SchwabPortalApproved.png)

The approved dashboard uses different example names from the creation forms; match the product, not the example name.

Open **View Details** for each app. Confirm its product and registered callback, then copy its Client ID/App Key and Client Secret into the matching FastDOM fields. Keep the pairs separate. Never send your secret, passwords, access tokens, refresh tokens, or a completed callback URL containing a code to support or include them in screenshots.

## 6. Enter the applications in FastDOM
Open FastDOM application configuration (the gear button), select the Brokers tab, and choose **Set up Schwab applications...**. Use the Accounts and trading column for the trading app and Market data for the data app. Enter each application's name, Client ID, Client secret, and Registered callback URL. Click **Save application setup**.

The two registered callback fields must each equal the URL above, including HTTPS and the full path. Do not add a trailing slash, your Client ID, a query string, or a login authorization code. The same callback handles both apps. This is a FastDOM authorization relay, not a webpage you need to host yourself. A browser visit to the callback alone does not authorize an account.

![FastDOM application setup: example names and the shared callback; credential fields deliberately empty.](SchwabSetupWindow.png)

This is an actual FastDOM screen captured with an empty local profile. Use your own keys in the blank fields. Show values reveals protected fields for review; hide them again before sharing a screen. Browser setup uses local SQLite storage. If Connect is unavailable and the window says Derby, follow your installation's storage setup before proceeding; changing storage does not migrate existing archives.

## 7. Authorize trading, then market data
From the setup window, click **Connect trading**. Complete Schwab sign-in, identity checks, and account consent in your browser. Wait for FastDOM to confirm the result. Next click **Connect market data** and complete that authorization too.

Alternatively, **Reconnect to Schwab... > Login** guides you through the required connections. Login uses the browser flow; Try automatic sign-in is a separate option that uses saved brokerage sign-in details. The username/password boxes are not where developer keys belong.

![FastDOM reconnect screen: Login opens browser authorization; Open connection setup returns to the two application profiles.](SchwabRecoveryWindow.png)

The introductory page identifies the **Trading Key** or **Market Data Key** about to be authorized. Use Continue if you do not want to wait for its countdown. Seeing a second sign-in is expected: you are authorizing the other application. Finish both flows. A browser callback confirms receipt of an authorization response; the app must still complete the exchange and report the outcome.

Keep FastDOM open while authorizing. If you close the browser before finishing, the default browser cannot reliably tell FastDOM that you closed a tab. Cancel the pending connection in FastDOM or wait for its timeout, then retry the incomplete key. Do not create new keys simply because you closed a tab.

## 8. Verify both halves without placing an order
Select Schwab Live and confirm that an account is selected and positions and buying power load where provided by Schwab. Compare the selected account with the one you approved. This checks the trading connection.

Open a chart for a supported stock symbol and press Refresh. History should load without a market-data authentication error. Verify a fresh quote timestamp during the relevant market session. This checks data; an account list alone does not. Market closures and data entitlements can affect what updates. No test order is required for onboarding.

## Troubleshooting
**Accounts load but charts say authentication is unavailable:** check the Market Data Production app and its saved key/secret, then authorize market data. Refreshing a chart cannot supply a missing authorization.

**Callback or redirect error:** compare the portal and FastDOM callback fields character for character. After editing an app, check its status again. Avoid legacy callbacks from another installation.

**Credentials rejected:** verify the product, approval status, and the correct Client ID/secret pairing. If you regenerated a secret, update FastDOM before reconnecting. A rejected or expired authorization needs a new sign-in.

**Another PC stopped connecting:** authorizing the same applications on another installation can affect saved grants. Reconnect the affected installation; do not assume one pair of saved refresh tokens remains valid on every PC. Use separate application pairs for independent installations where Schwab permits them.

**Need help:** contact support@decoglobal.us with the FastDOM version, which key failed, the stage, and a redacted error. Keep credential values and callback codes private.

## Reference and screenshot notes
Portal steps checked October 24, 2026. Schwab can change labels and approval rules. Official references:
https://developer.schwab.com/user-guides
https://developer.schwab.com/user-guides/individual-developer/become-individual-developer
https://developer.schwab.com/products/trader-api--individual
https://developer.schwab.com/user-guides/apis-and-apps/create-an-app

Open **More > Schwab setup guide** for the short, one-step-at-a-time walkthrough. Annotated portal examples show Create App, both application forms, and the approved dashboard with View Details highlighted. The private credential-details screen is intentionally omitted. Click any screenshot to enlarge it. Example app names may differ between screenshots; use your own applications and credentials.

# Setup | Schwab: two applications and first connection
FastDOM uses separate Schwab developer applications for **Accounts and Trading Production** and **Market Data Production**. You supply your own application credentials. Your brokerage username/password and your developer client ID/secret serve different purposes and are not interchangeable.

## Before entering details
Have both applications approved and usable in your Schwab Developer Portal. For each, identify its application name, client ID, client secret, and registered callback URL. The callback must match the relay callback expected by the FastDOM connection flow and registered with Schwab. Use the deployment's supplied callback; do not invent a different URL or copy credentials from another user. Provider approval and access are prerequisites outside FastDOM.

## Set up the application profiles
1. Open the main configuration gear, then Brokers > Set up Schwab applications.
2. Fill the Accounts and trading column using the trading application's details.
3. Fill the Market data column using the data application's details. Keep the two profiles separate.
4. Select Save application setup. Show values can reveal saved fields for checking; keep that view private.
5. Use Connect trading and complete Schwab sign-in, any verification, account selection, and approval in the browser.
6. Use Connect market data and complete its separate approval. The general Login recovery flow can guide you through both sequentially.
7. Return to FastDOM and wait for the application to validate/apply the authorization. A browser callback message alone is not proof that account discovery or market-data requests succeeded.

## Acceptance checks
Select Schwab Live and your intended account. Confirm positions and buying power. Open Chart, select a supported symbol, and press Refresh. Confirm history and current quotes both work. A successful account list with "market-data authentication is unavailable" means the data side still needs attention.

The SQLite setup stores protected application profiles and tokens for the current Windows user. Copying protected token files to another Windows user or computer is not a supported substitute for signing in there. Never share client secrets, token stores, or screenshots with revealed fields.

# Setup | Schwab: Login, reconnect, and browser cancellation
Open Configuration > Brokers > Reconnect to Schwab when authorization needs attention. **Login** uses the browser flow. **Try automatic sign-in** uses saved sign-in details when available. **Open connection setup** edits the developer application profiles. **Close** dismisses the recovery window; use **Cancel sign-in** for an in-progress attempt when offered.

## Why two logins appear
Trading and market data have independent OAuth approvals. The introduction page identifies the Trading Key first. After its approval, the next introduction identifies the Market Data Key. Continue manually or let the introduction's countdown advance. This is a second permission grant, not necessarily a failure of the first login. Finish both.

## Automatic sign-in
The remember option stores brokerage sign-in details securely for this Windows user. Automatic sign-in attempts recognized forms and approval steps. Identity verification, account selection, a changed Schwab page, or a rejected password can still need your intervention. Do not confuse these brokerage fields with developer API credentials. Saving a password does not permanently authorize either API application.

## If you close the browser
A system browser may reuse an existing process or tab; FastDOM cannot always reliably detect that you closed only the authorization tab. An application status saying "opening" or "complete approval there" may therefore outlast the tab. Cancel the pending attempt in FastDOM and start a new one rather than assuming the account is connected. If the UI remains stuck, record the step and status for support.

## Invalid or expired saved tokens
When Schwab rejects a refresh token, a new interactive authorization is needed. Repeated Refresh clicks cannot repair a revoked grant. Signing in on another installation with the same developer applications can coincide with invalidating older saved grants; do not assume authorizations on two computers are independent. Verify each installation after a new approval and avoid repeated alternating logins while diagnosing.

If the browser says the authorization response was received but the recovery window has closed, inspect FastDOM's account selector, chart, and activity log. The callback acknowledges delivery, not the final result of every service.

# Setup | Alpaca accounts and paper/live selection
Open Configuration > Brokers and enable Alpaca. Each account row has its own API key, secret, name, and Paper setting. Paper determines which Alpaca trading endpoint that row uses. The account dropdown determines which configured account you trade.

## Setup procedure
1. Obtain the credentials for the intended paper or live account from Alpaca. Keep paper and live keys distinct.
2. Add an account row with a recognizable name, matching credentials, and the correct Paper checkbox.
3. Save configuration and select Alpaca in the broker switcher.
4. Choose the account and verify its balance, positions, and buying power before trading.
5. Load a chart and inspect quote age. Data coverage is independent of whether account access succeeds.

Do not interpret the word Alpaca alone as paper mode. Inspect the account row and selected account. Removing a configuration row removes that local connection choice; it does not close broker positions or cancel orders.

## Extended hours and data
The order ticket's Ext flag is for supported extended-hours limit orders. A market order is not converted into a valid extended-hours order just because Ext is selected. The installed adapter and your account/data permissions determine symbol and data coverage; do not assume all-exchange depth from a top-of-book quote.

If a connection fails, check the selected account's paper/live flag and credentials first. If trading works but charts do not, inspect the market-data path separately. When using NINJA MD, verify the Ninja bridge and instrument mapping in addition to Alpaca account health.

# Setup | NinjaTrader bridge, feeds, and futures mappings
FastDOM connects to NinjaTrader through its bridge. NinjaTrader must be running with the required bridge installed and an appropriate data/account connection active. Enabling NinjaTrader in FastDOM alone does not start an external data subscription.

## Connection procedure
1. Install and open NinjaTrader 8 once, then close it. In FastDOM Configuration > Brokers, choose **Install / repair NinjaTrader bridge…**. Select the NinjaTrader user-data folder containing `bin\Custom` and install. Redirected Documents folders are supported. An existing bridge source is backed up under `FastDOM-Bridge-Backups` before replacement. If NinjaTrader is not installed yet, return to this option later. The FastDOM installer's optional final-page checkbox opens the same setup window. In NinjaTrader, open New > NinjaScript Editor, press F5 to compile, resolve any errors, then restart NinjaTrader. The setup window also opens the bundled source and guide for manual use.
2. Start NinjaTrader and connect the desired live, simulation, or playback account/data feed.
3. In FastDOM Configuration > Brokers, enable NinjaTrader and check the bridge URL and default account. Reconnect after changing the bridge URL.
4. Review allowed accounts. "Allow ALL live accounts" broadens access; when it is off, the allowed list matters. A familiar default name is not proof that the selected account is simulated.
5. Check symbol-to-instrument mappings in the NinjaTrader configuration. A root such as /MNQ must resolve to the contract you intend to trade. Review these mappings when contracts roll.
6. Select the account or enable NINJA MD for market data only. Verify quote timestamps, depth levels, and actual prints.

## Depth versus tape
Bookmap and L2 tools need market depth. Footprint needs native executions with bid/ask classification. A connection that supplies one may not supply the other. The bridge's feed must be active, the instrument subscribed, and the upstream entitlement available.

If NinjaTrader's trade feed stops delivering prints while prices keep moving (this can happen after NinjaTrader restarts while its price feed is still connecting), the bridge detects it. It records trades from price updates in the meantime and restarts the trade feed automatically, at most every 30 seconds. If restarts keep happening, check NinjaTrader's data connection. The account list shows only accounts NinjaTrader currently reports as connected, including connected accounts with no balance. After installing a new bridge version, recompile it in NinjaTrader (NinjaScript Editor, F5) and restart NinjaTrader before expecting the new behavior.

Never fix an empty display by guessing a different contract while a position is open. Identify the broker's exact instrument name and compare it with the configured alias. Different contract months are different instruments, even when their root names match.

# Setup | Optional AI: choose Codex or Claude Code, installation and models
FastDOM's AI features use a command-line tool installed on the same Windows environment, signed in with your own account. You choose which one in **Configuration > General > AI PROVIDER**: **Codex (OpenAI)** or **Claude Code (Anthropic)**. FastDOM does not bundle a model locally or provide a shared account. A model name in a selector is a requested model identifier, not proof that the software is installed or authenticated.

## Choose the provider
1. Open Configuration > General and find AI PROVIDER.
2. Select Codex or Claude Code.
3. Use **Validate installation** to check that the selected tool is installed and signed in. It shows Ready or Not ready, the reason, and the tool's location. It sends no AI request.
4. Select Save. From then on every AI feature uses that provider: Check Trend, Manage, Trading Partner, Market Desk, Learn, the Options Trader AI score and recommendations, and local Ask FastDOM help. There is no per-feature mix.

Switching provider does not change what the features are allowed to do. Both run read-only, with no tools, and Manage still sends every protection change through the normal order checks. A model saved for one provider is not sent to the other: after switching, reopen AI windows or start the next Partner/Desk request to refresh their model controls. An in-flight request retains its original provider. Active Manage keeps its original provider, CLI path and model until you disengage and start it again.

## Set up Codex
1. Use **Download Codex desktop** in the AI setup window to open https://chatgpt.com/download/ (Codex is now part of the ChatGPT desktop app). Alternatively, **CLI install instructions** opens https://developers.openai.com/codex/cli/.
2. Follow the current installation instructions there for your environment. Install the CLI in an environment FastDOM can launch; a CLI available only inside a separate WSL shell is not automatically a native Windows executable.
3. Open a terminal under the same Windows user and run codex login, then complete the supported sign-in flow.
4. Return to FastDOM and choose Check again (or Validate installation). If the CLI was just installed and is still missing, restart FastDOM so it receives the updated PATH.

## Set up Claude Code
1. With Claude Code selected, the AI setup window's **Claude Code install instructions** opens https://code.claude.com/docs/en/setup. Follow the Windows instructions there.
2. Open a terminal under the same Windows user and run claude auth login, then complete the sign-in flow with your own Claude account or subscription.
3. Return to FastDOM and choose Check again (or Validate installation). FastDOM finds claude.exe on PATH, next to an npm installation, or in the native installer's location. If it was just installed and is still missing, restart FastDOM.
4. Claude model choices are sonnet, opus, and haiku (each uses the current model of that tier), plus the model set in your Claude settings if you have one.

FastDOM runs Claude Code without your personal Claude settings, hooks, plugins, MCP servers, or tools, so your own Claude Code customizations do not apply inside FastDOM.

## Readiness states
Missing means the CLI was not found. Sign-in required means an account login is needed. Unavailable means it could not start or complete the readiness check. Ready means the preflight succeeded; a later request can still fail because of account limits, connectivity, or unavailable model access.

Check Trend, starting Manage Position, Trading Partner, Market Desk, and Learn open the same setup dialog when the selected provider is not ready. Your question stays in Market Desk so you can retry after setup. Finishing setup does not automatically start an analysis or a position-management lifecycle; retry the AI action yourself. Ask FastDOM's Automatic/hosted support routing is separate and remains available without a local provider.

The chart MODEL selection applies to chart AI functions such as Check Trend and Manage. Do not assume it controls every separate AI service. Squawk uses local rules and Windows speech, regardless of its AI badge.

## Data and access
AI analysis can send the supplied market/account context and your question through the selected provider. Do not enter passwords or developer secrets into prompts. Account availability, usage limits, and external service terms are controlled by the provider. Optional AI is not required for ordinary charting and manual trading.

FastDOM reuses the selected CLI's existing sign-in, which is why you may not see another login prompt. A supported account-plan login can use that plan's allowance without entering a separate API key in FastDOM. This is not unlimited or guaranteed free usage: API-key or other metered authentication can incur separate charges. Check authentication, allowances and permitted usage with your provider. FastDOM does not display your complete provider billing balance. Official authentication guidance: https://learn.chatgpt.com/docs/auth and https://code.claude.com/docs/en/authentication.

# Setup | Installation, editions, updates, and local data
Developer and Free Beta are built from shared source with separate edition behavior. Developer is unrestricted by the Beta activation service. Beta uses its activation/access status. A shared source fix affects an edition only after that edition is rebuilt and distributed.

## Installing or updating
Use the intended release installer from the official FastDOM distribution page. Check the publisher/release information and follow the supplied unsigned-build instructions if the package is explicitly labeled unsigned. Do not assume a Beta installer is an update to a separate Developer deployment. Close the intended application before updating and verify which shortcut you launch afterward.

A new upload does not itself prove that an already installed copy has updated. Compare the release information and actual installation you launched. If a fix appears absent, report the installed edition/build and the shortcut used.

## Activation versus broker login
Beta activation controls access to FastDOM features; it does not log you into Schwab, Alpaca, NinjaTrader, Codex, or Claude Code. An Active Beta can still have expired broker authorization. A successful broker login does not override an application access restriction. Follow the status shown by your build rather than assuming a fixed trial duration.

## Local files
Runtime settings, workspace layouts, archives, logs, and protected authentication are separate data categories. Their resolved locations depend on the installation and configuration. Do not assume every edition uses one universal AppData directory. Storage settings show the selected archive provider and SQLite path; a relative path is resolved against that installation's configuration folder.

Never copy example configuration files over working personal settings. Never distribute your live configuration, authentication store, or archive as part of an installer. For a new computer, configure and authorize it as a new installation.

# Setup | Storage: SQLite, Derby, and the preview window
Open Configuration > Storage > Choose database to inspect the archive provider. Beta uses SQLite only, with native Schwab authentication; no Derby server, Java, Python, or external token process is required. Developer also supports the legacy Derby server arrangement. Storage is not a broker account selector. Changing the database does not migrate existing records.

## Switching providers
Choose the intended provider, review the file path or server configuration, and save for restart. The change takes effect after restart. Switching providers does not import, synchronize, or merge the history in the previous database. Existing records remain where they were collected. If a panel has no historical data afterward, first confirm which archive it is reading.

For SQLite, Check SQLite file validates the configured file path. It is not a complete test of broker authentication, quote streaming, or archive coverage. Protected Schwab credentials use an associated authentication store and are scoped to the Windows user.

## Preview window
A window titled "FastDOM SQLite experiment - isolated storage preview" is launched by the development publisher's storage-preview mode. It is a configuration preview, not the main trading terminal and not a required recurring sign-in step. Close it without saving if you did not intend to change storage, then launch the normal application shortcut.

## Dependencies and limitations
Other archive-dependent views require actual collected records for the requested symbol/time range. Selecting SQLite does not manufacture historic native prints or Level 2 snapshots.

Close the application before deliberate maintenance of its database files. Do not delete an authentication store to troubleshoot an empty chart; first inspect the provider and reconnect status. Include file paths only when needed for support, and never send token contents.

# Workspace | Main window and daily orientation
The top bar selects the trading broker, symbol, optional NINJA MD feed, and account. It also shows account buying power and opens Configuration, Chart, Orders, OPT, and More. The account positions area, DOM, order ticket, hot buttons, watchlist, and activity log serve different jobs.

## Read the screen in this order
**Broker/account:** establishes the order destination. **Symbol:** establishes the instrument. **Position:** establishes whether an action would open, add, reduce, or reverse exposure. **Quote/age:** establishes whether displayed prices are current. **Size and risk:** establish the inputs used by the selected execution control.

The position list shows account holdings; the DOM's position summary concerns the current symbol. Day P/L, realized P/L, and open/unrealized P/L are different measures. They can also differ from a broker's reporting convention or update cadence. A blank value is not necessarily zero.

## Navigation
Chart opens a separate chart. Orders displays working orders. OPT opens the options chain. More contains Watch, L2 Heat, BookMap, FootPrint, Time & Sales, Movers, Options Trader, Partner, Desk, Performance, Margin, Pulse, Trade Copier, SpotGamma, Learn, Help, and About.

The main configuration gear controls application settings. The hot-buttons gear controls actions and their keyboard assignments. Indicator gears inside a chart control the indicator's parameters, not broker configuration.

## Status and activity
The status line gives a concise current message; the timestamped activity log provides context such as subscription, authentication, order result, or analysis failure. A request being sent is not the same as a confirmed fill. Use Orders and the broker's own order state to resolve uncertainty.

# Workspace | Linking, Watch, watchlists, and saved layouts
The small watchlist in the main window is a symbol list with price/change information. Use its add/remove controls and sortable headings. A chart's star adds its symbol to this watchlist. Removing a symbol from a watchlist does not cancel its orders or close its position.

## Watch multi-chart window
More > Watch opens a grid of small charts. Enter a symbol and Add, choose the timeframe/history range, and use Refresh to reload. Each tile has a symbol header and close control; drag headers to rearrange tiles. The counter indicates current tiles and the supported capacity. Watch is a scanning layout, not proof that every symbol has authorized historical data.

If all tiles show authentication unavailable, troubleshoot the shared history/data connection first. If only one tile fails, check that symbol's format, provider coverage, and timeframe. Changing tile order does not change the main trading account.

## Symbol linking
The chain-link control on a chart follows the main DOM symbol when enabled. Footprint and Pulse also support linking; typing a symbol into those windows unlinks their symbol selection. Read the symbol in each window before interpreting a signal. An unlinked chart can show a different instrument from the main DOM.

## Layout persistence
FastDOM saves supported workspace positions and view state. Restored charts keep their saved indicator choices; changing default indicators affects newly opened charts rather than necessarily changing every restored chart. The application saves workspace state during normal shutdown, so allow it to finish closing.

If a window restores in the wrong position, note whether monitors, scaling, or maximized state changed. Report the affected window and whether it was closed individually or as part of full shutdown. Do not replace a workspace file with an example file as a first troubleshooting step.

# Trading | DOM ladder and one-click controls
The DOM is the price ladder for the selected instrument. BID and ASK display quoted liquidity; BUY and SELL areas show execution controls and working-order information. Last price, best bid/ask, and position-related highlighting convey different facts. A large displayed size is resting liquidity, not a completed trade.

## Navigation controls
The − and + controls change the number of displayed levels. Z− increases the price step so more range fits; Z+ reduces the step for finer detail. The reset control returns to the original tick step and recenters. Center returns the ladder to current price. Lock/follow changes how the viewport follows price; inspect its state before interpreting movement on screen.

## Clicking the ladder
Order-side clicks can submit immediately using the current account, symbol, size, and configured behavior. A working-order cancel control requests cancellation at that level. Read the order ticket and hot-button topics before trying these actions live. Hovering or seeing a level does not reserve a price.

A buy limit at or above the ask can execute immediately; a sell limit at or below the bid can also execute immediately. The limit is a worst acceptable price, not a guarantee that the execution occurs exactly there. A limit away from the market may remain working indefinitely or only partially fill.

## Reading depth honestly
Dragging a working-order marker moves the orders at the grabbed row. Hold Shift through release when dragging a stop to include the other stops for the same account, symbol and side. A DOM drag is admitted as a group: while its broker replacements are pending, another DOM drag on that account/symbol is blocked in full. Wait for the completion message before dragging again. Broker replacements are separate operations; an incomplete result lists how many orders were confirmed and requires checking the remaining orders. The app does not automatically retry or roll back a partial move.

Some feeds provide only best bid/ask while others provide many levels. An L2/depth indicator describes available data, not a promise that all exchanges or orders are represented. When zoomed, multiple prices may aggregate into one displayed row. Use the selected price step when comparing sizes.

After any execution action, verify the order ID/status and resulting position. A marker is a visualization of state, not independent evidence of an accepted broker order.

# Trading | Order ticket, quantity, TIF, and extended hours
The ticket constructs a specific order for the selected account and symbol. **Side** chooses buy or sell. **Qty** is the number of instrument units, such as shares or contracts. **Type**, **Limit**, **Stop**, and **TIF** define how the order may execute. Available combinations depend on the broker and instrument.

## Order types
**Market:** requests execution against available liquidity without a specified limit price. **Limit:** caps a buy price or floors a sell price; execution is not guaranteed. **Stop market:** a trigger activates a market exit/entry and does not guarantee the stop price. **Stop limit:** a trigger activates a limit order and can fail to fill after a gap. **Marketable limit:** a limit priced to cross the current market; it still has a price boundary.

The Limit field is not a stop trigger. For a stop-limit order, the trigger and execution limit are distinct. Check which fields the selected type uses before pressing SUBMIT. A broker rejection should be read rather than worked around with a different order type without understanding the consequence.

## Size controls
The main Size field and preset buttons provide convenient quantities. The 1–10 presets are labeled for option contracts. Quantity is not dollar risk: ten shares, ten options contracts, and ten futures contracts have different economic exposure. Risk-based buttons use a different sizing path; read their topic.

## TIF and Ext
Day and GTC govern order lifetime where supported; IOC/FOK or other choices are broker-specific. Ext requests extended-hours handling for supported limit orders. Alpaca needs its extended-hours flag and Schwab uses the corresponding session handling. Do not expect market orders or every stop/bracket combination to work outside regular hours.

Clear clears ticket inputs; it is not Cancel. SUBMIT and the adjacent Buy/Sell buttons are execution actions. Cancel Sym and Flatten have separate meanings described in their own topic.

# Trading | Flatten, Cancel, Reverse, and Take 1
These controls have different scopes and consequences. Read the configured hot-button script as well as the label, because a customized button can behave differently from a built-in chart command.

## Cancel
Cancel Sym requests cancellation of working orders for the current symbol. Cancel All has broader scope according to the invoking control/account context. Cancellation does not close an existing position, and removing a protective stop can leave a position unprotected. A cancel request may race with a fill. Verify the final broker state.

## Flatten
Flatten cancels relevant working orders and attempts to close the current symbol position. Do not assume it always sends a pure market order. The General configuration includes **Flatten limit offset (cents)**, and configured actions can use bid/ask-relative limits. Inspect the current policy and actual submitted order.

For example, a sell limit below the current bid allows execution at that limit or a better price; it does not require the broker to fill at the lower limit. A fast market, spread, depth, route, and timing can still affect execution. A successful click or submission message is not proof the position is flat. Confirm quantity reaches zero and no unwanted working exits remain.

## Reverse
A reverse action can close one side and establish the opposite side. It is not merely a protective exit. The needed order quantity can exceed the existing position because it must both close and reopen. Review the configured script, confirmation settings, account permissions, and resulting position.

## Take 1
The chart Take 1 action reduces the current position by one unit through the shared order service and coordinates the associated take-profit/protection adjustment. The toolbar describes a one-contract market reduction and removal of the farthest one-contract target. Actual eligibility and order reconciliation depend on the current instrument and bracket state. Read the result if refused; do not assume a target disappeared or a fill occurred merely because the button was pressed.

If any of these actions is uncertain, inspect Orders and your broker's interface before submitting another order. Repeated clicks can create additional requests while earlier ones are still resolving.

# Trading | Risk Buy/Sell, staged stops, and Secure
Risk Buy, Risk Buy STP, Risk Sell, Risk Sell STP, Secure Buy, and Secure Sell are entry/protection workflows backed by configured actions. They are not chart annotations. Their effective risk, offsets, stop types, and target template come from your configuration.

## Risk-sized entry
Risk-sized scripts require a valid positive risk budget, a valid stop and an executable-side quote. Missing or invalid inputs reject the action; they do not fall back to the selected share size. A zero-sized risk entry stops subsequent commands. Saved custom scripts are preserved on update: inspect the configured script and supply an explicit STOP when required.

The basic sizing relationship is risk budget divided by loss per unit between entry and stop, including the instrument's point/tick value where appropriate. A smaller stop distance can produce a much larger size. Price movement, gaps, fees, and slippage mean actual loss can exceed the nominal budget.

1. Confirm the account, symbol, intended direction, and risk budget.
2. Stage the stop on the chart (the chart workflow uses a double-click), or enter the stop in the action's dialog when requested.
3. Check that a long stop is on the intended side below entry, or a short stop above it. Inspect the displayed risk and quantity before execution.
4. Choose the appropriate Risk action. The STP variants and stacked-target variants are separate configured buttons; inspect their scripts rather than inferring all differences from the abbreviation.
5. After a fill, verify the actual position, stop coverage, and target quantities against broker state.

A chart context command can place a Risk Buy/Sell limit at the selected chart price. This differs from buying at a current quote and may remain unfilled. A staged stop is an input to the workflow; it is not by itself a live protective order.

## Secure
Secure actions apply the configured protection/target workflow to a position. They are not an assurance that the position becomes risk-free. Confirm the direction, stop reference, active target template, and actual accepted exits. Do not treat a displayed stop line as proof of broker protection.

Read Order-management templates and reconciliation for how remaining percentages and resizing work. If an action is rejected because the stop, position, or account state is invalid, resolve that state rather than repeatedly pressing the button.

# Trading | Order-management templates and reconciliation
Configuration > Order Management defines reusable take-profit templates for stacked Risk and Secure workflows. Exactly one template is active. New, Duplicate, Delete, and the active-template control manage the list. Targets are ordered nearest entry first.

## R multiples and remaining percentages
R is the absolute distance between entry and stop. A long 2R target is two such distances above entry; a short 2R target is below entry. The target percentage applies to the **remaining unsold quantity**, not always the original position.

Example: starting with 100 units, a 50% remaining target allocates roughly 50. Another 50% remaining target allocates roughly 25 of the remaining 50. A final 100% remaining target takes the tail. Integer rounding and minimum unit sizes affect small positions; review the actual generated quantities.

The last target should normally consume 100% of the remainder if the intention is to exit all units. The template is a plan, not proof of fills. Partial fills, rejected children, and broker-specific OCO handling can change the live state.

## Reconciler
General > Enable Reconciler allows existing protective quantities to be resized after confirmed fills to match broker position. It may increase, decrease, or cancel existing protection. It does not create missing protection or change prices. Enabling it is therefore a real order-management choice, not simply a display preference.

## Verification workflow
After entry and after every partial exit, compare position quantity with accepted protective orders. Ensure no exit quantity could unintentionally reverse the position and that remaining exposure is protected as intended. Review the activity message if reconciliation cannot establish broker truth. OCO/bracket behavior is not interchangeable across brokers, and app-managed protection may depend on FastDOM remaining connected.

# Trading | Hot buttons, scripts, and keyboard shortcuts
Open the hot-buttons gear to edit visible actions. Each button has a label, appearance, and execution definition. Templates cover market and limit orders, dollar sizing, scale-outs, cancellation, risk entries, brackets, dialogs, and position management. Add/Delete and Up/Down change the layout; Apply inserts a selected script template. Save commits changes; Cancel discards the dialog edits.

## Reading a script
BUY SIZE LMT ASK means a buy using the configured size at an ask-referenced limit. SELL PCT:25 MKT requests a partial-position market sell. A bid/ask offset changes the acceptable limit. CANCEL and BRACKET lines introduce additional operations; a multi-line button is not necessarily one atomic broker action.

These examples explain the notation, not recommended live orders. Use the template description and actual script as the source of truth. The words on the button can be changed independently of its logic. A "Sell" percentage action is not automatically appropriate for a short position; inspect whether it sells or covers.

## Keyboard-only actions
Use Keyboard-only shortcuts from the hot-button editor or the hotkey settings dialog. Add a binding, choose the action, capture a key gesture with the capture button, set its enabled and double-press options, then Save. Escape cancels key capture. Reset Defaults replaces your custom bindings; review before saving.

FastDOM has focus and typing protections, but do not rely on remembered factory shortcuts after customizing them. Read the actual assigned gesture. Double-press requirements and confirmation settings are action-specific. A keyboard binding can target a chart-context action; focus the intended chart and verify its symbol/account before pressing it.

Practice configuration in simulation, including a focused text field, a different chart, and an open auxiliary window. Confirm exactly which window/context receives the action before relying on it live. Opening Help does not intentionally execute any trading command.

# Trading | Orders, positions, risk gates, and failure handling
Orders lists working orders and supports individual cancellation plus Cancel All. Read account, symbol, side, quantity, type, price, and status together. An order can be pending, working, partially filled, filled, cancelled, or rejected; these are not interchangeable. A locally drawn line may lag the broker during reconciliation.

## Risk controls
Execution goes through shared validation/risk paths. Depending on configuration, gates cover account permission, symbol restrictions, quantity/notional limits, quote freshness, spread, short selling, extended hours, daily loss, rate limits, and confirmation thresholds. A permitted order is not a guarantee of a safe position or an acceptable fill.

Do not disable a risk gate merely to make a rejection disappear. Identify its reason, intended account/symbol, input size, and current market data. Data staleness and missing prices can invalidate a risk calculation. Closing/reducing actions may have different eligibility from opening actions.

## Disconnection during an order
An HTTP timeout or missing acknowledgment does not establish that the broker rejected the order. The request may have reached it. Check the broker's open orders and position before resubmitting. Likewise, closing FastDOM does not by itself cancel broker-held orders or close positions.

## Daily verification
Before trading, reconcile open positions and working protection. After a partial fill or manual broker-side action, refresh and verify FastDOM catches up. At session end, confirm the intended remaining positions, GTC orders, and protection directly with the broker. App-managed features require a running connection; broker-held orders have their own lifetime.

When reporting a failure, provide the time, edition/build, broker mode, action label, instrument, and redacted status. Never include access tokens, API secrets, or full account credentials. Do not place a real test order solely to demonstrate a UI bug.

# Charts | Chart toolbar, history, timeframes, and navigation
Open Chart from the main window. The chart has its own symbol, link state, timeframe/history selection, drawing state, indicator selections, and execution controls. Confirm its account context before using the order row.

## Top toolbar
The symbol box changes the instrument. Star adds it to the main watchlist. Chain-link follows the DOM symbol. The timeframe/range selector controls candle aggregation and requested history. Refresh reloads data. Z− shows more candles; Z+ shows fewer, larger candles; reset returns to the default latest view.

Configs contains display/session settings such as Extended, extended-hours background, and Show Trades. Extended affects included history; Ext BG shades the extended-session background. Show Trades marks supported closed/standalone trades for the symbol with realized P/L. Do not confuse this with a live order acknowledgment.

Indicators opens the indicator list. A gear beside an indicator edits its supported parameters, color, width, or line style. Chart defaults in Application Configuration apply to new charts; restored workspaces keep their saved selections. Custom timeframe definitions are managed by the timeframe configuration dialog, which supports adding/deleting rows and saving the list.

## Reading the plot
The top quote/candle header describes the selected or current candle. The legend identifies enabled overlays. Candles show open, high, low, and close; volume occupies its own area. Auxiliary indicators can add panels beneath price. The Older/Newer scrollbar controls the visible historical region. A chart scrolled into history can show old bars while the live quote continues elsewhere.

The chart's time axis, provider timestamps, and session-specific calculations are not all interchangeable clocks. Opening-range/session features follow their documented exchange-session conventions. Check the timeframe before interpreting a completed-bar signal: one bar on a 1-minute chart is not one bar on a 1-hour chart.

# Charts | Drawing tools, context menu, and price alerts
The drawing-tools button opens chart annotation tools. Drawing and order placement share the same plot, so read the active tool and context menu carefully. A visual line is not a broker order unless it belongs to an actual accepted order.

## Annotations
Use the available drawing tools for price levels, trend/structure annotations, and measurements. Select the intended timeframe context where offered. Saved chart drawings are visual context; changing a drawing does not inherently replace a broker order. A measurement is a distance calculation, not a prediction.

## Tool-by-tool reference
**Trend Line** joins two anchors over a finite span. **Ray** continues beyond an anchor in one direction. **Extended Line** projects the same relationship beyond both anchors. These extrapolations do not confirm future support/resistance.

**Horizontal Line** marks one price. **Vertical Line** marks a time/candle reference. Each is a single-point placement. **Text** prompts for a note and places that annotation on the chart.

**Rectangle** marks a zone across time and price. **Ellipse** highlights a region. **Arrow** draws directional emphasis. **Freehand** follows your drawing gesture. These shapes do not create orders or change indicator calculations.

**Fibonacci Retracement** calculates reference fractions between chosen anchors. Reversing the anchors changes the direction of the measurement. **Percentage Measure** reports a price-range change over the chosen span; the result is a measurement, not realized account P/L.

Select a tool, then place its required anchor(s) on the plot. Undo last drawing (shown as Ctrl+Shift+Z in the tool menu) removes the last annotation. Clear all drawings removes the drawing set, not broker orders. Do not use drawing deletion to try to cancel an order.

## Chart price actions
Right-click at the desired price to inspect the actual menu. Depending on position/context, actions include risk-sized limit entries, partial position limit exits, a full-position stop loss, and Set price alert. Menu labels include the selected price and sometimes quantity. Recheck these before choosing: the clicked chart coordinate can be far from the live market when zoomed or scrolled.

Double-click is used by the staged-stop workflow. Staging a stop feeds Risk/Secure actions; it does not mean an order is already working. Dragging an actual order marker can invoke order modification. Verify the broker's accepted replacement and quantity afterward; an optimistic marker movement is not final confirmation.

## Price alerts
Choose Set price alert at the selected price. Select Above or Below and choose app sound, email, or both as supported. Create Alert records the trigger. App sound needs FastDOM running and audio available; email needs verified, enabled email preferences in Beta or configured SMTP settings in Developer. An alert is a notification and does not enter or exit a trade.

In Beta, open Configuration > General > Email communications, enter your receiving address, and send a verification code. Enter that code, verify the address, then save Receive price alerts. Product updates are a separate optional choice and default to off. Email changes take effect immediately; Remove email clears the address and both subscriptions. FastDOM must be running for chart price alerts to fire.

Developer retains personal SMTP setup and Send test email. Those sending credentials are not used or included in Beta.

# Indicators | EMA, VWAP, Bollinger Bands, and ATR
These are descriptive calculations on available data. Enable them from Indicators. The gear controls supported parameters and styling; labels may retain familiar names such as EMA9 even when a customized period is used, so inspect the displayed period/settings.

## EMA fast and slow
An exponential moving average weights recent closes more heavily. A shorter period reacts faster but changes direction more often; a longer period is smoother and lags more. Price crossing an EMA or fast/slow crossing can describe a change in recent trend, but is not an automatic entry signal. Changing timeframe changes what a period represents. Both EMA overlays are display-only.

## VWAP
Volume-weighted average price summarizes traded price weighted by volume within the calculation's session/data scope. It is useful as a location reference, but the result depends on available bars, volume, and included session. Missing or different feed coverage can produce a different VWAP from another platform. VWAP is neither a guaranteed support level nor a broker execution benchmark supplied by FastDOM.

## Bollinger Bands
The center is a moving average and the envelope reflects dispersion over the configured period and multiplier. Wider bands indicate greater recent variation; narrower bands indicate less. Touching an outer band alone does not establish reversal. The default label is 20,2, but settings can change it.

## ATR gadget
ATR measures typical true range, including gaps, over its input series. Enabling ATR exposes a movable timeframe picker. FastDOM projects ATR High/Low from yesterday's close for the selected timeframe. These are volatility-based distances, not guaranteed daily boundaries. A daily ATR and a five-minute ATR measure different horizons. Read the selected timeframe and source before comparing levels.

# Indicators | Prior OHLC, premarket, opening range, and Location
These features organize price by session and nearby reference levels. They do not independently submit orders.

## Prev OHLC and Pre Mkt H/L
Prior-session open, high, low, and close provide historical reference prices. Premarket high/low describe the configured premarket session's extremes. The calculation needs the appropriate historical session, not just today's visible candles. If source data is absent, do not substitute an arbitrary visible bar for yesterday's session.

## ORB 15/30/60
Opening-range boxes begin at 08:30 Central Time and cover 15, 30, or 60 minutes for the supported regular-session convention. Until a range completes, its developing high/low can change. A later break of the range is a price event, not proof of a profitable breakout. Futures overnight ranges and equity regular-session ranges are different concepts.

## Location chip
Location compares price with enabled anchors such as previous-session levels, premarket levels, and VWAP. It indicates whether price is at a reference and estimates room in ticks to the next level above/below. It respects each contributing level's display toggle, so switching an anchor off can change the result.

NO LOCATION means the feature has no qualifying nearby anchor; it is not missing account authentication. Green/red room coloring compares space with the approximate round-turn cost wall. It is a contextual estimate, not a promise that a trade clears costs or reaches the next level. Move the chip if it obscures the plot.

Practical workflow: load enough history, enable only the references you use, verify their session labels, and compare current location with both next levels. Do not confuse a chart's historical crosshair value with the current market price.

# Indicators | Camarilla levels and Camarilla Plays
Camarilla projects intraday reference levels from the prior regular-session high, low, and close. FastDOM prefers its dedicated prior-RTH calculation and can fall back to available prior-daily data. The legend identifies RTH or prior-daily so you can see the source.

## Reading the levels
R levels are upper references; S levels are lower references. The chart emphasizes R3/R4/R6, S3/S4/S6, and CP. CP is the central pivot. BC and TC define the central pivot range (CPR), shown as a band where visible. Price tags identify a level and its value. Levels outside the visible price range may not be drawn.

The context label classifies CPR width relative to the prior range as "trend day (narrow CPR)" or "range day (wide CPR)." These labels describe a heuristic expectation, not a known outcome for the current day. A narrow range does not guarantee trending price.

## Camarilla Plays study
Enable Camarilla first, then Camarilla Plays. The study looks for documented fades: price tags an R3/R4 or S3/S4 reference and closes back across it, with B/S order-flow tilt supporting the direction. The visual shows the entry-to-target area toward CP and marks target/stop outcomes.

The Alerts option adds a sound/activity message when a qualifying setup first appears live, with deduplication per session/level. It does not submit an order. This is a visual study; its edge did not pass the project's validation. Historical shaded successes must not be treated as a validated trading strategy.

## Setup and troubleshooting
Use a symbol with prior-session history, Refresh, and inspect the source label. If values differ from another platform, compare session boundaries, close definition, daily/RTH source, and included history before assuming arithmetic is wrong. The caption shares the indicator legend so it does not overwrite EMA text.

# Indicators | Higher-timeframe support/resistance and trendlines
Show 1H Levels, Show 4H Levels, and Show Daily Levels use independently fetched higher-timeframe bars, even when the visible chart is on a shorter timeframe. They derive structure from swing fractals and prior-period references. Changing the visible chart timeframe does not simply relabel its candles as higher-timeframe data.

## Support/resistance zones
Zones are bands rather than exact guaranteed turning prices. Their displayed role can change as price crosses/retests them. Multiple nearby zones may overlap; highlighted or selected subsets emphasize relevant structure. A chart zoom can reveal or hide zones because rendering considers the visible price range.

Confirmed swings require subsequent bars. A level that becomes known later must not be interpreted as if it had been available at its original turning candle. Missing higher-timeframe history can leave these overlays empty while the main chart still works.

## Trendlines 5m + 1H
This feature projects support/resistance from confirmed swing anchors in five-minute and one-hour series. Lines are visual context and can become stale or invalidated. A projected line is not a scheduled order price. The legend counts the relevant displayed families.

Check Trend optionally asks the selected AI model to review completed-candle anchors. It is display-only and does not execute a trend-following trade. If the AI provider is unavailable or the review fails, inspect the activity result; retained existing lines are not evidence of a newly successful AI review.

Recommended setup: enable one higher-timeframe family first, identify its source, then add another only if it helps distinguish immediate and broader structure. Too many enabled overlays can obscure candles even when every calculation is correct.

# Indicators | MACD, RSI, Vortex, and Chop Detector
These indicators summarize momentum or market condition. Their panels and traffic lights are observations, not broker instructions.

## MACD
MACD compares fast and slow exponential averages. Its signal line smooths that difference; the histogram shows their separation. Standard defaults are 12/26/9 and the gear changes supported periods/style. A positive MACD is not the same statement as a rising histogram. Crossovers in a sideways market can repeatedly reverse.

## RSI
The RSI panel uses Wilder RSI, conventionally a 14-period measure, with configurable overbought/oversold thresholds commonly shown as 70/30. An extreme reading describes recent directional imbalance, not a guarantee of immediate reversal. Strong trends can remain extreme. The RSI panel is separate from RSI × Book, which additionally requires resting-book data.

## Vortex
VI+ and VI− compare directional movement over the configured period, with a 1.0 reference. Crossovers can suggest a change in trend structure, but frequent crossings can also indicate chop. The chart uses cyan/red lines. This overlay is display-only and does not create orders or standalone alerts.

## Chop Detector
The traffic light represents the current chop/whipsaw danger estimate: green means lower indicated danger, yellow caution, and red higher danger. Green does not mean a trade is safe or has positive expectancy. Read it together with volatility, spread, trend structure, and the timeframe used.

If an oscillator differs from another platform, compare warm-up history, input prices, period, smoothing method, and session inclusion. A short history can produce a different initial value even when later values converge.

# Indicators | Coverage and B/S Detector
These features transform candle/volume observations into visual context. They are different from native bid/ask trade classification and should not be treated as interchangeable evidence.

## Coverage projection
Coverage estimates a probable next-candle retracement using completed-candle history. The plot/legend can show a retracement ratio, historical hit rate, and sample count. These describe the calculation's sample, not a calibrated promise that the next candle follows the projection. A small sample, changed volatility, or missing history can make the context weak. The projected area is not a working order.

## B/S Detector
The buy/sell detector is an EMA-25 signed-volume oscillator on an approximately ±100 scale. The zero line separates its estimated buying/selling tilt; ±10 bands identify stronger sustained phases. The selector switches Tick rule and Movement classification modes. A mode change changes how volume is assigned or weighted and can change the line without any new trades.

Unlike a footprint built from native bid/ask executions, candle/tick-rule estimates cannot recover every actual aggressor. Use the source appropriate to the question. Camarilla Plays can use the B/S tilt as confirmation, but that does not transform the study into an automated or validated strategy.

# Indicators | Cumulative Delta and Delta Scalper
Executed delta compares volume traded at the ask with volume traded at the bid. Cumulative Delta aggregates that difference through the session and can display bar values and price/delta divergence markers. It needs usable classified trade data; ordinary OHLC candles alone do not provide true execution-side detail.

## Interpreting divergence
Price making a new low without a matching delta low can indicate a difference between price movement and aggressive selling. It does not prove absorption or guarantee reversal. Session reset, missing prints, provider coverage, and a change in contract can also change cumulative totals. Compare the same instrument and session when comparing platforms.

## Delta Scalper Signals
This is a deterministic completed-bar setup detector combining location such as VWAP/recent structure, normalized delta, divergence or reversal evidence, and price confirmation. It plots LONG/SHORT context. It does not send a broker order, and its eligibility rules are not replaced by an LLM.

## Practical setup
Confirm native trade collection and a populated footprint/delta series. Enable Cumulative Delta, then Delta Scalper if desired. Wait for completed bars rather than treating a still-forming bar as confirmed. Read signal time and direction alongside the price chart and source freshness.

An absent signal can be a valid result when the conditions are not satisfied. Do not infer a broken indicator solely because candles are moving. Conversely, a blank delta series should prompt a data-source check rather than a parameter change. A marker is a historical or current analytical event, not a position or fill.

# Indicators | Liquidity, Volume Levels, and L2 Imbalance
These tools examine different kinds of activity. **Liquidity** uses resting orders. **Volume Levels** uses executed volume. **L2 Imbalance** compares resting bid-side and ask-side quantities. A resting order can be cancelled without trading; executed volume has already occurred.

## Liquidity bands
The chart highlights concentrated resting depth as possible support/resistance context. Distance filters and displayed depth determine which concentrations qualify. A wall can move or disappear, so its presence does not guarantee support. If the provider offers only top-of-book, do not expect a complete deep-book structure.

## Volume Levels
Volume Levels estimates high-volume price areas from the loaded candles by spreading each candle's volume evenly across its low-to-high price buckets. It is not an exact execution-by-price profile or native bid/ask classification. Distance filtering keeps nearby noise from dominating, and the visible price scale determines which nodes can appear. The bands are not pending orders. An old node may matter as context, but the chart does not know whether participants still hold those positions.

## L2 Imbalance panel
The symmetric imbalance compares bid and ask resting size around a zero center. Positive/green is bid-heavy; negative/red is ask-heavy. Live sub-bar sampling can show changes within a candle. The panel's history begins with available collection; enabling it does not guarantee full historical backfill. Archive availability in other tools does not mean this indicator reconstructs the same history automatically.

## Absorption Alerts
This separate toggle combines a completed-bar price/delta divergence at an extreme with a persistent opposing book lean. It can show a chip and play a sound. It is independent of whether the imbalance line is displayed, so turn off Absorption Alerts itself to silence it. It never submits an order.

If a large wall appears without corresponding tape, it is still resting liquidity. If price moves despite the wall, avoid concluding that the display predicted a guaranteed reversal.

# Indicators | Near/Deep Book and RSI × Book
These features relate resting-book structure to other observations. They need real multi-level depth and enough live samples; a price chart alone is insufficient.

## Near/Deep Book
Near depth covers a narrow neighborhood around price (approximately ±0.1%); deep depth uses a broader region (approximately ±0.7%). The deep series is an area, the near series a line, and orange columns mark stronger opposition. ALIGN and N/D state tags summarize their relationship.

The header estimates rolling lead/lag relationships of near/deep imbalance and spread with forward one- and three-minute returns over roughly 90 minutes. DEPENDENCY turns amber only when the configured test identifies a relationship; gray means no qualifying relationship is established now. A sample correlation is not a permanent market law.

When qualifying dependence and a stable lean are present, one-shot direction markers/sounds can occur. Direction incorporates the sign of correlation, so a mean-reverting relationship can invert the raw lean. Cooldowns, drift gates, and minimum stability suppress repeated/conflicting calls. This remains display-only, not auto-entry.

## RSI × Book states
- **CUSHIONED DIP:** oversold with bids stacked; mean-reversion confluence.
- **NO FLOOR:** oversold without a qualifying cushion; warning against assuming support.
- **CAPPED:** overbought with supply overhead; potential fade context.
- **SQUEEZE FUEL:** overbought with bids stacking; warning against mechanically fading strength.

The Alerts option adds chart state-change markers and requires RSI × Book enabled. A state label explains a combination of inputs, not a guaranteed next move. Missing depth or insufficient persistence can mean no state is available even with a valid RSI value.

# Indicators | Big Trades and Momentum Swing
## Big Trades
Big Trades groups same-side native prints within a short interval (500 ms) into larger trade clusters and draws bubbles. Green denotes classified buying and red classified selling; bubble numbers represent instrument units/contracts according to the feed. Top 10/25/50 controls the displayed selection.

The grouping is an estimate of related prints, not proof that one institution submitted a single order. A large sell cluster with little downward progress can suggest absorption; a large buyer followed by sustained progress can suggest initiative. The Signals option adds battle-outcome markers based on subsequent price behavior, including an absorption marker. It is display-only.

## Momentum Swing
Momentum Swing is a one-minute momentum/breakout composite. It has **Alerts Only** and **Auto-Trade** modes. Alerts Only is the default; explicitly choosing Auto-Trade authorizes bracket-entry behavior through the shared order service and risk checks. This is an important exception to the display-only nature of most indicators.

Historical validation in the project was instrument/data-specific. It is not a promise of future performance or permission to transfer the same assumptions to another symbol, feed, or timeframe. Confirm input coverage, eligibility, account, size, and protection before enabling active execution.

When active, inspect the strategy's lifecycle and actual broker position/orders. A visual signal does not prove an entry was accepted; risk gates or lifecycle conditions can prevent submission. Switch back to Alerts Only to stop requesting new automated entries, and independently verify the treatment of any already open position/protection. Do not assume closing a chart cancels every broker-held order.

# Options | OPT chain and contract selection
OPT opens the options chain for an underlying. Enter/check the underlying, use Load Expiries, choose an expiration, and Load Chain. Read calls and puts, strikes, bid/ask, and the fields provided by your data source. The selected contract is a distinct instrument from the underlying stock.

## Workflow
1. Verify the underlying and current underlying price.
2. Load available expirations and choose the intended date. Similar-looking contracts with different dates are not interchangeable.
3. Inspect call/put, strike, spread, quote age, and liquidity for the specific row.
4. Use Add to Watchlist for a contract you want to track. Adding a contract does not submit an order or grant options trading permission.
5. Before any later order, confirm the complete contract symbol and quantity in the execution context.

Contract quantity is not share quantity. Premium, contract multiplier, exercise/assignment conditions, and broker permissions affect exposure. FastDOM's displayed analytics do not replace the broker's option approval or order validation.

## If the chain is empty
Check market-data authorization separately from account login, the underlying format, expiration selection, and whether the provider returns that chain. Use the displayed error or activity message. A stock chart loading successfully does not prove options-chain entitlement.

Chain snapshots are point-in-time observations. They are not an event-level record of all option trades. Open interest and volume have different meanings and update schedules; do not treat a volume change as verified new open interest or confirmed buying pressure.

# Options | Options Trader: spreads at one net price
More > Options Trader builds a multi-leg option spread and sends it as one order at one net price. The supported strategies are vertical (call or put), iron condor, iron butterfly, butterfly (1-2-1), condor, straddle, strangle, calendar, and diagonal. Spreads can be sent only on a Schwab account. On any other broker, the order is refused before anything is sent.

## Build a spread
1. Enter the SYMBOL and press Load. Choose the EXPIRATION, and for a calendar or diagonal also a BACK MONTH.
2. Choose the STRATEGY, then Call or Put where it applies, and Buy or Sell. Buying usually means paying a net debit; selling usually means receiving a net credit.
3. Set the center STRIKE, the WIDTH and, for condors and strangles, the GAP with the − and + buttons.
4. Check the legs table: action, expiration, strike, type, bid, ask, mid, and delta for each leg.
5. Set QTY (number of spreads) and TIF (Day or GTC). Each leg trades its ratio multiplied by the quantity.

## Net price and risk
NET PRICE is always entered as a positive number per spread. Mid prices every leg at the middle of its bid/ask. Natural buys legs at the ask and sells legs at the bid. Natural is an indicative crossing price, not a guaranteed fill. The ±.01 and ±.05 buttons adjust the price.

AT EXPIRATION shows max profit, max loss, breakevens, a payoff chart, and a model profit estimate for the entered price and quantity. A max loss of UNLIMITED means the spread has undefined risk (for example, a short straddle or strangle). Calendars and diagonals depend on the back month's remaining value, so only their debit max loss is stated. The profit estimate is a lognormal model based on the legs' implied volatility, without drift. It is a model estimate, not a forecast or a success rate. It is shown as n/a when two expirations are involved or no implied volatility is available.

## Review & Send
Review & Send shows the complete order text, including the account, every leg, quantity, net price, and risk. Nothing is sent until you approve it. The order then passes FastDOM's normal risk checks:
- Symbol restrictions apply to the underlying.
- Max order risk is compared with the larger of the premium and the spread's max loss.
- When a max order risk is configured, an undefined-risk spread is refused.

Sending needs a fresh quote snapshot (under 60 seconds old). A leg whose own quote is 1-5 minutes old can still be sent, and the warning is shown in the quote status and in the confirmation. A leg quote older than 5 minutes blocks sending; use Refresh quotes. Adjusted or non-standard contracts (for example, ones that deliver cash or a basket instead of 100 shares) are not supported and cannot be sent.

## Closing an existing spread
Tick Closing to close legs you already hold. Before sending, FastDOM reads your current positions and working orders from the broker, and it refuses the close if:
- a leg would open or reverse a position;
- a leg asks for more than you hold;
- another working order already covers the same contracts;
- the positions or orders cannot be confirmed.

If the broker's answer to a close is unclear (for example, a timeout), the order is marked Unknown. Check your broker's order list before trying again, because the first order may have been accepted. Max profit, loss, and breakevens show n/a for closes, because the original entry cost is not known here.

## Scan & score and AI
SCAN & SCORE checks every strike, width, and gap combination of the selected strategy within RANGE ± strikes of the price, up to MAX WIDTH. Each combination is priced a third of the way from mid toward natural, which is closer to a realistic fill than mid. Combinations with wide leg markets, no possible profit at the natural price, undefined risk, or two expirations are skipped. Each remaining combination gets a 0-100 SCORE from probability, reward/risk, and the cost of crossing the market. Results at or above MIN SCORE and MIN PROB % are listed, and SORT changes the order. Use loads a row into the ticket at its listed entry price; it does not send anything.

AI score list and AI Score (AI SETUP REVIEW) ask the optional AI to grade the listed combinations or the current spread. The AI sees only the spread's data, not your account. Its score is advice only: it never sends, blocks, or sizes an order. It is marked out of date when the legs, price, or quantity change. MIN AI SCORE hides rows below it and rows the AI did not score. These buttons are hidden in builds without the AI assistant. A high score is not a calibrated success rate.

Clear resets the window to how it opened, keeping only the symbol. It never cancels or changes orders.

## After sending
Open Orders shows each spread as one row, with a summary line (strategy, quantity, net debit or credit) and one line per leg below it: green for buy legs, red for sell legs. Confirm the legs in your broker's order list as well.

## Change the price of a working spread
To improve your chance of a fill, use **Change price…** under the spread in Open Orders. Set the new net debit or credit with the price box or the −.05/−.01/+.01/+.05 buttons. The MARKET box shows the spread's live **natural** (indicative crossing price: buy legs at the ask, sell legs at the bid; not a guaranteed fill), **mid**, and **last**, plus each leg's bid, ask and last, refreshed every 5 seconds with the oldest quote time. A spread has no single last fill: last combines each leg's own last trade, which may be from different times, so treat it as indicative. Use mid, Use natural and Use last copy that price into the box (mid is rounded to the cent that is more likely to fill). The dialog shows what you will pay or receive and the maximum loss at the new price before you confirm. The dialog stays open after each change and shows whether the broker accepted it, so you can adjust again; it closes only when you choose Close. If the spread fills or is cancelled meanwhile, the dialog says so and no longer sends changes. Paying a higher debit, or accepting a lower credit, makes a fill more likely but raises the maximum loss and never guarantees a fill.

Only the price changes: the legs and quantity stay the same. A spread cannot switch between debit and credit this way, and a partly filled spread cannot be repriced; cancel it and enter a new one instead. The new price passes the same risk checks as a new order, including the kill switch and max order risk. The order can still fill at the old price while the change is in flight, so confirm the result in your broker's order list. Rolling a spread is not available yet. Chain quotes are snapshots. Use Refresh quotes before pricing, because they do not update on their own.

# Options | SpotGamma menu and options hedging map
More > SpotGamma opens FastDOM's options hedging map. The menu name does not mean FastDOM has received SpotGamma's proprietary dealer positions or proprietary Hedge Wall. The view computes estimates from available option-chain snapshots and the configured sign model.

## Reading the window
Gamma by strike shows concentrated sensitivity around strikes. Estimated levels summarize reference points. Exposure by expiration separates maturities. Context and Change explain the comparison with an earlier compatible snapshot. Refresh requests a new map; check source time, coverage, partial-chain status, and warnings before interpreting it.

## Sign assumptions
Option-chain data does not reveal who owns each contract or actual dealer inventory. Call/put sign settings impose assumptions on the calculation. Signed totals can change materially when those assumptions change. Absolute exposure answers a different question: concentration without netting direction.

Gamma transition is a modeled balance point, not a certain price barrier. The estimated Hedge Wall is a transparent FastDOM calculation under quality/threshold rules. A pin candidate identifies concentration and does not assert price attraction. Amplification/dampening labels are conditional on the model.

## Snapshot comparisons
Compare only the same symbol and sign methodology. Changes can reflect price, greeks, expiration coverage, or open-interest inputs, not necessarily new trading. The system does not label chain volume as verified aggressor flow or opening/closing intent. Missing event-level option trades and quote ordering limit what can be inferred.

<!-- feature:OptionsArchive -->
Set up collection under Configuration > Options Archive. Confirm that the correct storage backend, symbols, expiration range, and refresh interval are active. A persistence warning can coexist with a freshly computed map; it means historical storage should be checked separately.
<!-- endfeature -->

# Options | Options Levels, Gamma Strikes, Gamma Flow, and Pressure
These chart overlays use shared options snapshots but answer different questions. Select the expiration scope deliberately: 0DTE, 0–7 DTE, or Aggregate. A change of scope changes the population of contracts, so levels can move even with unchanged underlying price.

## Options Levels
Displays estimated call/put concentrations, gamma transition, Hedge Wall, expected-move context, and quality/regime information. These are modeled references. Inspect data freshness and coverage, particularly around expiration changes or incomplete chains.

## Gamma Strikes
Shows per-strike exposure independently of other options overlays. Choose Top 3, Top 5, or All, and Call/Put, Signed, or Absolute exposure. Bars adds proportional right-edge bars. Signed exposure nets according to the sign model; absolute exposure highlights total concentration. A longer bar is a modeled magnitude, not the number of pending market orders.

## Gamma Flow Buy/Sell
Combines actual multi-level depth/native trades with direct or explicitly mapped options-gamma context. It can use NinjaTrader or Schwab input where supported. Futures require the configured proxy/mapping rather than an invented direct equity chain. The signals are display-only and do not send orders.

## Options Pressure
Estimates directional pressure from one-minute changes in Schwab option-chain snapshots. Choose 1 minute, 5 minutes, 15 minutes, or Session. It can use a configured options proxy for Ninja futures. It is not exact aggressor flow and cannot establish the intent of individual trades.

If stock candles work but these overlays do not, check options collection, chain permissions, scope, proxy mappings, and quality warnings. Reconnecting the trading account alone may not repair a missing options data dependency.

# Order flow | L2 Heat and current depth
More > L2 Heat opens the depth-oriented view. It represents currently available resting liquidity and price aggregation. It should be distinguished from the time-history BookMap window and from executed Footprint volume.

## Controls
Add Symbol opens or pins another instrument view where offered. Finer/compressed price bins control how prices aggregate; compression makes more range visible but merges detail. The other zoom/reset controls change presentation. Center returns the view to current price. Lock/follow governs viewport tracking. MAP switches between supported ladder and current-snapshot presentations.

## Reading the picture
Intensity or bar length represents resting quantity under the selected normalization. Compare the legend and bin size before comparing two displays. A large bright region means liquidity is displayed there now; it does not prove it will remain when price approaches. Orders can cancel, move, or replenish.

## Setup
Use a data provider that supplies real multi-level depth for the selected instrument. Check its subscription and bridge health. A quote with only one bid and ask is not full depth. Changing the trading account does not automatically change data entitlements, and NINJA MD changes the feed without changing the order destination.

If the display is blank, inspect provider/source status and depth counts before changing colors. If depth is present but too faint or compressed, adjust the presentation and price bins. Do not interpret an empty historical region as proof the book had no orders; this view cannot infer uncollected data.

# Order flow | BookMap heatmap
More > BookMap opens the time-based liquidity heatmap. It visualizes how resting depth evolves, with price and other supported trade overlays. Unlike a static ladder, the horizontal dimension shows history over the selected window.

## Controls
WINDOW selects the visible history horizon, from seconds through longer minute/hour ranges. HEAT adjusts intensity normalization. LIQ RANGE limits the visible price neighborhood. Add Symbol creates a pinned tab; use the tab close control to remove it. These choices affect presentation and subscriptions, not your broker account.

## What the heat means
Persistent bright bands indicate repeatedly observed resting liquidity. A band disappearing can mean cancellation, price movement outside the view, a subscription gap, or a change in normalization. A heatmap alone does not distinguish all those causes. Compare current depth and tape before assigning intent.

Real prints and trade bubbles, where provided, represent executions; heat represents resting orders. An execution at a level can consume liquidity, but replenishment and hidden quantity complicate the picture. Neither display identifies a trader by name.

## Empty or stale BookMap
Confirm the selected symbol, correct futures month, active provider, depth entitlement, and whether the bridge is delivering updates. A "waiting for ... depth" message should be resolved at the source. History starts with available collected/restored samples; changing WINDOW to an hour does not create an hour of missing data.

Use a modest visible history and sensible range while learning. Very dense displays can hide the distinction between near-market changes and distant resting liquidity. A large wall is context, not an instruction to buy or sell.

# Order flow | FootPrint and delta clusters
More > FootPrint opens executed bid/ask volume by price within each candle. It answers where trading occurred, unlike L2 which describes orders resting in the book. Native trade data and classification are prerequisites.

## Controls and navigation
The symbol box selects the instrument. Chain-link follows the DOM; typing a separate symbol unlinks it. BM opens the Bookmap depth view. Timeframe offers one-, five-, and fifteen-minute aggregation. Zoom controls change density. The style button switches Δ Cluster and Bid × Ask pairs. Mouse wheel changes candle density; left-drag moves/squishes the view; right-drag shifts price vertically.

## Reading the cells
Bid volume is executed selling into bids under the feed's classification; ask volume is executed buying at asks. Net delta is ask minus bid. A positive net number does not mean price must rise: passive sellers can absorb aggressive buying. The green volume-POC bar marks the highest-volume price area within the footprint's presentation, not a future target.

Header information distinguishes stored and live data and shows update times/counts. Missing classified prints can produce empty cells even when an OHLC candle exists. Do not use candle volume as a substitute for a complete bid/ask breakdown without an explicit estimation label.

## Comparing with the chart
Match instrument, timeframe, and session before comparing delta with price. A five-minute footprint sums several minutes of executions; a one-minute Squawk read is a different cadence. Provider gaps or contract mappings can make totals differ from another platform.

If you see price bars but no footprint values, verify native trade collection and archive coverage. If older candles exist but the newest stalls, inspect the live feed and timestamp rather than repeatedly zooming.

# Order flow | Time & Sales tape
More > Time & Sales shows individual or feed-provided execution prints over time. Read time, price, size, and side classification together. Tape describes completed executions, while BID/ASK depth describes resting orders.

## Pause and Clear
Pause freezes the displayed tape while prints keep collecting; resuming reveals the continuing stream. It does not pause the broker, market, order routing, or archive collection. Clear clears the visible tape view according to the control; it is not a cancel-orders command.

## Interpretation
A large print may be important but does not reveal whether it opened or closed a position. Same-side sequences can be grouped by analytical features such as Big Trades; grouping is a heuristic. Trade classification depends on feed information and ordering, so unknown or ambiguous prints should not be silently treated as certain buyers/sellers.

## Setup and diagnosis
Use a symbol actively trading on the selected feed. Check time progression and provider status. A quiet or closed market can legitimately produce no new prints. If quotes move but tape stays empty, investigate the native-trade subscription; OHLC history and top-of-book quotes are separate data classes.

When comparing with Footprint, align the aggregation interval and session. The tape can help explain the newest footprint changes, but a screenful of prints is not the entire history of a bar. Do not infer fills of your own orders from tape prints at the same price; use your broker's execution records.

# Analysis | Market scanners
## Movers
More > Movers presents the available mover/universe data and offers Refresh. Treat the displayed ranking as a screen of the supplied universe, not a complete scan of every tradable security. Confirm symbol, quote freshness, volume/liquidity, and the reason a candidate is listed before opening a chart.

The selected broker's native discovery APIs are tried first: Schwab equity movers or Alpaca gainers, losers and most-actives. If unavailable, empty or unsuccessful, the scanner uses its configured fallback and displays the source and reason. NINJA MD changes quote delivery, not the trading account or primary broker discovery source. Yahoo ranked screens have limited coverage. Optional external providers require their own configuration; FastDOM does not create subscriptions for you.

Momentum Scan replaces FAST < $30. Enter Min price and Max price, then Apply; defaults are $1–$30. Bounds are inclusive and positive sub-dollar values are allowed. Additional filters are at least +5% change, 100K shares, $500K dollar volume, and no more than 2% quoted spread when available. Missing spread is not a pass on liquidity; unknown spreads remain included. Missing volume excludes a candidate. Apply filters the available discovery rows, not the entire market. Refresh retains the range while the window stays open; reopening restores the defaults. Invalid input leaves the last valid results in place. Selecting a row loads a symbol and never places an order.

A fast percentage change can result from a small base price, sparse trading, or a session change. A ranked name is not a recommendation and does not establish that your account can trade it. If the list is empty, check the configured universe/source and connection before assuming there are no movers in the market.

<!-- feature:MorningScanner -->
## Morning Scanner
More > Scan is a legacy Derby-backed scanner. It is optional, globally controlled under Configuration > Services, and currently disabled with SQLite storage. This dependency is intentional; selecting SQLite does not migrate the scanner's source.

The view offers Refresh, Warnings only, and policy/session selections such as premarket, one-minute ORB, five-minute ORB, and momentum windows. These labels identify different evaluation snapshots/policies. "Selected by best policy" is a scanner selection, not an assurance of a profitable live trade.

To use it, configure the supported Derby source, enable the scanner, set its universe file and refresh interval, and verify records exist for the requested session. Read warnings and timestamps. Do not switch a working storage provider just to remove a disabled-menu appearance without arranging the other archive/authentication dependencies.
<!-- endfeature -->

# Analysis | Pulse archive time slices
More > Pulse summarizes archived market observations into time slices: range/ATR context, book delta, and tape delta. It is an archive-analysis view, not a continuous guarantee of live data coverage.

## Workflow
1. Select or type the symbol. Chain-link follows the DOM; typing an independent symbol unlinks it.
2. Choose LOOKBACK, such as one hour through 48 hours, then AGGREGATION, such as one minute through one hour.
3. Press Refresh and inspect the source/coverage status.
4. Compare slices within the same symbol and consistent data coverage. Distinguish quiet trading from missing rows.

## Understanding the columns
Range measures actual observed price span; ATR is a range-derived volatility context. Book delta describes resting-side imbalance under the archive's sampling, while tape delta describes classified executed activity. They can legitimately disagree. A bid-heavy book with negative tape delta can mean aggressive selling into resting bids, not an arithmetic contradiction.

Longer aggregation reduces detail and can conceal short-lived changes. Short aggregation can look noisy with sparse prints or depth samples. Archives may retain only a limited recent window; selecting a longer lookback cannot restore already absent data.

If "No data loaded" persists after Refresh, confirm the selected storage backend, collection history, symbol/contract mapping, and requested range. A working chart history endpoint does not populate native-trade or L2 archives retroactively.

# Analysis | Margin and overnight exposure
More > Margin estimates distance to a margin call, conditional call prices, and position size that survives a specified adverse move. It uses account data and configured assumptions. It is a planning calculator, not a broker promise to maintain margin requirements.

## Setup and use
Confirm the selected account and current positions. For contract-based instruments, inspect the margin-per-contract assumption and use Save margin only when the value is appropriate for that symbol. A blank value clears the saved override. Select Buy or Sell, enter the scenario inputs, and use Check size.

## Read the assumptions
A call-price estimate assumes a relationship between account equity, position movement, and margin requirements. Multiple positions, correlated moves, intraday versus overnight schedules, broker house requirements, and changing maintenance rules can invalidate a simple estimate. A maximum modeled size is not a recommended trade size.

The main window's overnight-margin information highlights exposure relevant to carrying positions beyond intraday treatment. Buying power and overnight capacity are not interchangeable. A position permitted intraday can require more equity later.

If values are blank, stale, or inconsistent, refresh account data and compare with the broker's own margin display. Do not invent a margin value to make the calculator accept a desired quantity. Record the assumptions used when comparing two scenarios.

This view does not place a trade merely by running Check size. Any resulting order still needs an execution action through the usual paths. Broker requirements and account restrictions remain authoritative.

# Analysis | Performance calendar and Learn trade review
## Performance
More > Performance opens calendar-style results. Use previous/next, Today, and Month/Week/Day to select the reporting period; Refresh reloads supported account/execution history. Read whether a value represents realized trade P/L, day/account P/L, or an aggregate before comparing it with another panel.

Trade pairing, partial exits, fees, timestamps, broker corrections, and session boundaries can affect totals. A missing day can mean missing import/coverage rather than zero trading. An open position's unrealized movement is not necessarily part of a closed-trade result.

## Learn
More > Learn opens trade review for a selected date. Previous/next and Today move through sessions. ANALYZE WITH AI sends the available review evidence for a read-only analysis. It does not change historical fills or place corrective trades.

## Review workflow
1. Select the correct account and date.
2. Verify executions/trades are present and quantities/prices agree with broker records.
3. Identify a specific question: entry timing, exit management, oversized risk, or deviation from a plan.
4. Run the optional AI review if your AI provider is ready.
5. Separate observed facts from model interpretation. A model cannot recover missing execution context or know your unrecorded intention.

For discrepancies, report the date, symbol, reporting scope, and redacted trade details. Do not "fix" a result by deleting live archive records. Historical price touching an exit level is not evidence your actual order filled there.

# AI and audio | Check Trend, Partner, and Desk
These features are advisory/read-only. They help interpret supplied evidence and do not themselves authorize a trade. They are distinct from the chart's active Manage control.

## Check Trend
Uses the chart's selected AI model to review completed-candle trendline anchors. The purpose is validating/refining displayed structure, not predicting a guaranteed target. Existing lines may remain after failure; read the completion message to know whether a new review succeeded.

## Partner
More > Partner opens a focused thesis workspace. Quick questions cover long/short entry assessment, management discussion for an existing position, and comparing long versus short versus waiting. Add your specific thesis and use ANALYZE THESIS. CLEAR removes the conversation/display context in the window; it does not alter the account.

The result depends on the market evidence provided. Ask for invalidation, missing evidence, and contrary scenarios, not just agreement with a desired direction. A written suggestion to move a stop does not mean FastDOM submitted that modification from Partner.

## Desk
More > Desk supports broader research questions: what is moving, ORB opportunities, relative strength, regime/sentiment, catalysts, watch planning, and review of trading history. REFRESH RESEARCH refreshes the evidence; ASK THE DESK submits a question; CLEAR CHAT clears the conversation.

Read source times and gaps. A stale research snapshot does not become current because a model's response is newly generated. If your AI provider is missing, unavailable, or not signed in, follow Optional AI setup. Model access and request limits are separate from FastDOM's broker authorization.

## Daily watchlist from the Desk
CREATE WATCHLIST, next to REFRESH RESEARCH, opens a **daily watchlist** window with every symbol currently on the LIVE OPPORTUNITY BOARD, in board order. It becomes available once the board has loaded. The window is the same watchlist as the main window's: click a row to switch the DOM to that symbol, and the last price, change, sorting, add (+) and remove (×) work the same way. Trading hotkeys work while it has focus, as in the main window. Changes there never alter your main watchlist.

Pressing CREATE WATCHLIST again replaces its symbols with the current board and keeps the window's position. If the daily watchlist is open when you close FastDOM, it reopens with the same symbols next time. If you close the window yourself, it is forgotten. The board is research, not a recommendation: a symbol on the daily watchlist is not a signal to trade it.

# AI and audio | Manage: active AI position management
The chart's **Manage** control is an execution-capable exception to the generally advisory AI tools. It operates on an existing position for the chart's account and symbol, using the chart-selected model and current evidence. Do not use it as a synonym for opening the read-only Partner window.

## Starting a lifecycle
Confirm an open position, the exact account/symbol, current working protection, and fresh market data. Click Manage only when you intend to delegate the supported protection-management actions. The service first checks broker/account position state. If flat, it reports that an open position is required rather than opening one for you.

Read the management status, last check, next check, and detail messages. AI proposals pass through deterministic validation, the order service, and risk/broker checks; a proposal can be rejected or withheld. An accepted analysis response is not proof every requested protection order was accepted.

## Stopping and monitoring
Toggling management off cancels its ongoing lifecycle. Going flat causes disengagement. Verify existing broker-held orders independently afterward; stopping the analysis loop is not the same operation as canceling every stop or target. Avoid competing manual or copier changes without understanding how they affect the current lifecycle.

## Limits
AI does not know unseen liquidity, future news, or your intentions beyond the supplied context. Connectivity failures, stale evidence, and model errors can interrupt management. Broker-state verification remains essential. Never assume a protective line on the chart is a native accepted stop solely because Manage is active.

Complete AI setup first, then retry Manage explicitly. The setup dialog deliberately does not start management automatically after checking readiness. Keep read-only research and active order management conceptually separate even though both carry an AI badge.

# AI and audio | Squawk voice narration
Squawk is the chart's spoken event narrator. Toggle it on to hear "squawk on"; toggle it off to stop new chart callouts. It uses deterministic detection plus Windows text-to-speech and the default audio device. **It does not call any AI provider or use the selected AI model**, despite the current AI badge/tooltip wording.

## What it calls
Price action includes confirmed higher/lower highs and lows, double tops/bottoms, session extremes, and prior-day breaks. Its initial history pass is silent. Swing pivots are confirmed two completed bars later, so a call is intentionally delayed relative to the turning candle.

Footprint narration reads the newest completed one-minute footprint bar, regardless of the chart timeframe, after a short settling delay. It uses the same deterministic classification family as Footprint. It requires classified execution data and can describe climax, exhaustion, drives, or other qualifying patterns. Confirmation-dependent labels are not all available immediately.

Other enabled chart signals can contribute absorption or book-state callouts. Calls are deduplicated and paced by symbol/category; urgent events can bypass ordinary pacing. One shared speech worker keeps chart windows from speaking simultaneously. Already queued speech can briefly continue after a toggle change.

## If it is silent
Check Windows output device, volume, and speech availability. Confirm the toggle is on and new completed bars/data are arriving. Silence during initial history load or when no qualifying event occurs is expected. Read SQUAWK activity entries to distinguish event detection from audio output problems.

Squawk is not a news service, does not identify institutions, and never places orders. A voice call is an event interpretation, not a command to buy or sell.


# Automation | Trade Copier and follower verification
More > Trade Copier configures replication of supported FastDOM master actions to follower accounts. It starts **COPY OFF** at application startup. This is execution-capable: enabling it can cause one action to generate orders on more than one account.

## Setup
1. Identify the current master account shown by the window.
2. Add follower rows from available accounts. Set each row's enabled state and quantity multiplier.
3. Check that no unintended account is selected and that each follower has appropriate permission, buying power, and instrument support.
4. Learn the behavior in simulated/paper accounts before enabling live copying.
5. Turn copying on explicitly and inspect per-follower result/status after each supported action.

## Scope and limitations
The copier follows supported hot-button/DOM/chart actions through application paths. Do not assume it mirrors every broker-side manual order, every external platform action, or every account state change. A master fill is not proof of a follower fill. Multipliers, rounding, limits, latency, and rejection can create different quantities or prices.

Changing the master account or removing a follower is not a command to flatten existing follower positions. Turning COPY OFF stops new replication; it does not erase orders already accepted by a broker. Manage those positions and orders explicitly.

## Monitoring
Read individual follower messages rather than relying solely on the COPY ON indicator. If one follower fails, compare that account's actual working orders and position before repeating the master action. Repeating the master order to "fix" one follower can duplicate exposure elsewhere. Use account-by-account reconciliation to resolve differences.

# Configuration | Application settings reference
Open the main configuration gear. Save commits changes; some are applied immediately and others require reconnect/restart as labeled. The dialog focuses on application settings, with separate secure Schwab setup and broker-account configuration where needed.

## Brokers
Enable the brokers you use; the currently running broker cannot simply be disabled. NinjaTrader settings include bridge URL, default account, allowed accounts, and live-account access. Alpaca uses account rows with credentials and Paper selection. Schwab links to application setup and reconnect. These choices affect which connections are available, not the contents of external broker accounts.

## General
Default symbol, default quantity, DOM visible levels, and flatten offset define initial display/execution inputs. Order sounds toggle audio feedback. Reconciler controls automatic resizing of existing protection after fills. Confirm first live order is a confirmation aid, not a complete trading lock. Always on top and font scale affect windows. Logging controls file output, size, and retention; some logging changes require restart.

Beta requires only a receiving email address and its verification code. Save email preferences separately from the rest of the dialog. Refresh status retrieves the server's current verification and subscription state. Product updates are optional; verification alone never opts you in. Developer keeps its personal SMTP controls. Email failures do not disable in-app sounds or submit orders.

<!-- feature:OptionsArchive -->
## Options Archive
Enable options analytics, persistence, and optional background collection. Set symbols, expiration scope, refresh seconds, maximum expirations/DTE, and minimum open interest. The UI limits the symbol list and enforces a minimum refresh interval. Call/put signs and transition/rate settings are modeling assumptions, not discovered dealer positions. Background collection can operate without an open requesting chart and does not submit orders.
<!-- endfeature -->

## Services and Indicators
Services includes universe and refresh settings for Movers. Available features depend on the installed edition. Indicators chooses defaults for new charts. Saved charts restore their own settings. Order Management contains the active take-profit template. Storage selects the archive/authentication backend and requires restart; it does not copy history.

# Troubleshooting | Accounts work but charts or Watch do not
Start by identifying what succeeds. A populated Schwab account and positions prove trading/account access, not the independent Market Data Key. "Waiting for price history" plus "Schwab market-data authentication is unavailable" points toward history/data authorization rather than missing account discovery.

## Recovery checklist
1. Confirm the intended broker/account and data provider, including NINJA MD state.
2. Open Schwab setup/reconnect and inspect the market-data application profile. Do not replace trading credentials with data credentials or vice versa.
3. Complete both browser approvals if either grant was rejected. Wait for FastDOM's result after the callback.
4. Refresh a supported symbol's chart. If all Watch tiles fail similarly, investigate the shared data path first.
5. If only one symbol/timeframe fails, inspect format, provider coverage, available session history, and contract mapping.
6. Check whether the executable/shortcut points to the intended edition and whether storage selection changed. A different configuration folder may have a different authentication store.

If both approvals completed but Refresh still fails, collect the failure time and redacted activity message. Do not repeatedly delete tokens or re-enter credentials without evidence. A rejected refresh grant needs fresh authorization; a network outage needs connectivity recovery; an unsupported symbol needs a different data request.

Live quotes can work while historical requests fail, and historical candles can remain on screen while live data is stale. Verify both independently before relying on a chart for current decisions.

# Troubleshooting | Missing depth, tape, options, or archive data
Match the missing panel to its dependency. L2 Heat, BookMap, imbalance, Near/Deep, and RSI × Book need depth. Footprint, true delta, and Big Trades need native trades/classification. Options overlays need chain snapshots and valid mappings. Pulse and Performance need the relevant archived records.

## Check in order
1. Correct symbol and futures contract month.
2. Correct effective data provider and healthy upstream connection.
3. Entitlement and actual messages for the required data class.
4. Timestamp progression and sample/level counts, where shown.
5. Selected storage backend and historical coverage for archive queries.
6. Feature-specific scope, timeframe, filters, and confidence/quality gates.

Do not treat a quiet market as a guaranteed outage. Do not treat an empty archive as evidence that the market had no trading. Enabling collection now cannot retroactively create uncollected native prints or depth history.

For options, compare expiration scope, chain completeness, and source time. For mapped futures options context, verify the configured proxy.

When reporting the problem, include the panel, symbol, timeframe/range, provider label, last update time, and whether other panels using the same data still work. This is more useful than only saying "the chart is empty."

# Troubleshooting | AI errors, audio, slow windows, and shutdown
## AI
If a model name is visible but analysis fails, inspect AI readiness (Configuration > General > AI PROVIDER > Validate installation). Missing CLI, missing sign-in, inaccessible executable, network problems, model access, and account usage limits are different failures. Install/sign in under the same Windows environment, Check again, and explicitly retry the action. Do not start Manage just to test a read-only AI setup; use a read-only feature.

## Audio
Squawk and order sounds depend on Windows audio output. A logged event without speech suggests output/synthesizer trouble; no event can simply mean no qualifying condition. Check the specific toggle, completed-bar cadence, and volume. Email alerts use SMTP and are unrelated to Windows speaker settings.

## Responsiveness and closure
Large charts, archives, and external services can take time, but an indefinitely unresponsive window is not a normal completion state. Record the exact window, preceding action, timestamp, and error message. Allow normal shutdown to save workspace state. Closing the app is not a substitute for canceling orders or flattening positions at the broker.

If a fatal error appears, preserve a redacted screenshot and report it. After restart, reconcile account positions and working orders before resuming. The caret-style cyclic-reference error is a UI failure; it does not itself establish anything about order acceptance or authentication.

## Unexpected storage window
The isolated storage-preview window can be launched by development verification. Close it without saving unless you deliberately intend a storage change, then use the normal shortcut. If it appears on every ordinary launch, report the shortcut target/arguments rather than changing database providers.

# Reference | Glossary, limitations, and support
**Bid / ask / spread:** highest displayed buy quote, lowest displayed sell quote, and their difference. **Last:** latest reported trade, which may differ from either quote. **Depth/L2:** resting quantities beyond or around best quotes. **Tape:** execution prints.

**OHLC:** candle open, high, low, close. **Timeframe:** duration of one candle. **Completed bar:** interval has ended; the forming bar can still change. **RTH:** regular trading hours under the feature's session convention. **Premarket/extended:** trading outside that regular window.

**Delta:** meaning depends on context. Tape/footprint delta is classified buy volume minus sell volume. Options delta is price sensitivity. Book delta/imbalance concerns resting liquidity. They are not interchangeable units.

**R:** entry-to-stop distance in risk/target workflows. **OCO:** linked orders where one cancellation/execution relationship manages the other under broker/application rules. **Bracket:** entry/protection/target arrangement. **GTC:** good till cancelled subject to broker rules. **TIF:** time in force.

**POC:** price with highest volume in the relevant profile/footprint. **CP/CPR:** central pivot and central pivot range. **DTE/0DTE:** days to expiration / expiring today. **OI:** open interest. **Gamma:** sensitivity of options delta to underlying price under the calculation. **Proxy:** a mapped instrument used to supply context for another symbol.

## About and support
More > About contains the application's identity and support contact. Include edition/build, Windows environment, broker/data provider, reproducible steps, timestamps, and redacted messages when asking for help. Never include API secrets, passwords, refresh/access tokens, or a live authentication database.

## Scope of this first edition
This manual covers the current user-facing windows, major controls, indicators, setup paths, and common failures. It is not an exhaustive broker API reference or a guarantee of every configuration's behavior. Customized scripts, provider changes, experimental features, and future releases can differ. The actual configured script, current status, and broker-confirmed state take precedence over a generic example.

The guide is bundled with the build so it works offline. Future releases can expand it with screenshots, walkthroughs, and revised behavior. The original older UserGuide file is not the authoritative description of new controls; this in-app guide is the first consolidated help edition for the current implementation.


# Support | Ask FastDOM AI help

## Ask a question

Click the **chat AI icon after the More dropdown**, or open **More > Help > Ask FastDOM**, to ask about setup, features, or errors in plain language. Click an example, or type a question and select **Send** (Enter or Ctrl+Enter; Shift+Enter adds a new line). Questions and streamed answers appear in separate chat bubbles. Ask follow-up questions in the same conversation, or use **Copy answer** to copy a reply. Use the numbered buttons below the answer to open the related offline Help topics.

This optional assistant uses your selected AI provider (Codex or Claude Code) or FastDOM hosted DeepSeek, with relevant sections of this Help manual. It does not see your screen, read account details or logs, or perform actions. With **Include app context** checked, each question includes the selected DOM symbol, instrument type, trading mode, data provider, connection flags, and quote timestamps. The assistant uses that snapshot to explain likely causes; hosted AI also has a maintained equity calendar. It does not know whether a separate chart shows a different symbol. Uncheck the box to send the question without live app context. No local AI installation is needed for hosted help. Chart AI features remain separate.

## Choose an AI provider

Click **AI: Automatic · change** at the top of the chat to cycle the provider setting. The selection is remembered for this installation.

- **Automatic** checks whether your selected AI provider's CLI is installed and signed in. It uses that connection when ready, otherwise FastDOM hosted AI. The provider is shown for each request.
- **Local only** uses your selected AI provider and never falls back to the FastDOM server. Codex and Claude Code process requests in the cloud using your own account; local does not mean offline.
- **FastDOM hosted** uses the supplied DeepSeek service and its usage limits.

If a local AI request fails after starting, Automatic offers **Retry with hosted AI**; it does not silently send the conversation to the server. Local only requires an explicit mode change. For Codex, automatic discovery prefers the Codex desktop CLI over an older VS Code CLI on PATH. An explicitly configured CLI path is respected. Support chat always uses the provider's default model, independently of the chart model and saved model selection. Support chat does not inherit the provider's action tools or integrations. Arbitrary local model servers are not supported by this selector.

## Privacy and controls

The question, enabled app context, and up to four recent conversation messages are sent through the selected provider, together with relevant documentation. Hosted mode sends these to FastDOM's help server and DeepSeek. Local mode sends them through your AI provider account without contacting FastDOM hosted help. Never include passwords, API keys, authorization URLs, tokens, or account details. The chat is kept in memory and cleared when this window closes. **New chat** clears the current conversation. **Cancel** stops waiting; any partial answer is incomplete.

Answers may be wrong or incomplete. Verify important instructions against the linked Help. If authorization, connectivity, provider availability, or a usage limit prevents an answer, offline Help and search remain available. Contact support@decoglobal.us for unresolved issues.


# Help | Report a problem and support IDs

## Prepare and review the report

Open **More > Report a problem**, use **Report a problem** in Help, or attach diagnostics from Ask FastDOM. Describe what happened and what you expected. The window freezes an incident snapshot: build, features, connection/quote context, and up to 1,000 redacted diagnostic events from the last 30 minutes. Events are memory-only; restarting the app loses the prior timeline.

Review the report before sending. Account and order identifiers become session aliases. Raw log/config files, credentials and balances are excluded. Trade details are optional. You may attach a small PNG screenshot after cropping/redacting private information; it is previewed before upload. A reply email is optional and used for support only. Check the consent box, then **Send report**. Nothing is uploaded merely by opening the window.

## Keep the support ID or save locally

Keep or copy the returned **FD- support ID** and include it when contacting support@decoglobal.us. Reports expire after 30 days. If uploading fails or reaches a limit, choose **Save local copy** or retry the same report. A retry does not create a duplicate. Local exports can contain the trade details and screenshot you selected; keep them private.

## Analyze the report in Ask FastDOM

**Analyze in Ask FastDOM** opens a separate chat with this report attached; press Send to request analysis. The selected AI provider receives the report text and at most the last 100 retained events, not the reply email or screenshot. Local AI still uses cloud processing. The assistant can explain observations, hypotheses and missing evidence. It cannot trade or change settings. A historical report, UI marker or accepted request does not establish a current broker fill or working order; verify broker state. Contact support for unresolved issues, using the support ID.
