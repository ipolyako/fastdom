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


## Feature coverage

| Screen | Provider/model behavior |
| --- | --- |
| Configuration > General | Select Codex or Claude Code and validate installation |
| AI setup | Installation, sign-in and retry guidance for the provider that opened the dialog |
| Chart Check Trend / Manage | Selected provider and chart MODEL; protection remains subject to normal order checks |
| Trading Partner / Market Desk | Selected provider; controls refresh on the next request after switching |
| Learn / Options Trader | Selected provider and feature settings through AiCli |
| Ask FastDOM | Local uses selected provider default; Hosted uses FastDOM's DeepSeek service; Automatic follows the visible fallback policy |

Both CLIs process requests in the cloud. Local means the CLI runs on your PC, not offline inference. FastDOM does not sign you in automatically. Hosted help requires no local CLI. No provider switch authorizes an order or automatically begins analysis.
