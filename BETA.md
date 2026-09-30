# Beta test: use your real AI model

**Start with an interactive session in Claude Code, Codex, Gemini CLI or OpenCode.** Use your own model account or gateway and submit your own prompts. Vibead supplies synthetic advertisements from a local mock service it starts automatically. You do not need a private repository, a separate ad server or a simulated test first.

The commands below work with **beta.3**. The online guide is the current procedure; the guide inside an existing archive may still put the optional simulated test first.

## 1. Download and extract

Get an archive and its `.sha256` file from [beta.3 Releases](https://github.com/gwasan/vibead-cli/releases/tag/v0.1.0-beta.3):

| Computer | Archive ending |
| --- | --- |
| Mac with Apple Silicon | `darwin-arm64.tar.gz` |
| Mac with Intel processor | `darwin-x64.tar.gz` |
| Windows x64 | `win32-x64.zip` |
| Linux x64 | `linux-x64.tar.gz` |

Compare the archive's checksum with the value in the `.sha256` file. Replace `ARCHIVE` with the downloaded filename:

| Terminal | Checksum command |
| --- | --- |
| macOS | `shasum -a 256 ARCHIVE` |
| Linux | `sha256sum ARCHIVE` |
| Windows PowerShell | `Get-FileHash ARCHIVE -Algorithm SHA256` |

Extract the complete archive and keep its files together. Open a terminal in the extracted `vibead-beta-PLATFORM-ARCHITECTURE` folder. Your chosen AI agent must already be installed and available in that terminal. Vibead itself needs no npm installation, compiler or Docker.

## 2. Connect your model account

Vibead opens the agent in a **temporary empty workspace**. Your normal saved login, provider settings and plugins are not copied. Complete the agent's sign-in/provider selection when it opens, or use a supported key already exported in this same terminal:

| Agent | Account or key for this test |
| --- | --- |
| Claude Code | Sign in inside Claude, or export `ANTHROPIC_API_KEY`. For a gateway token, use the setup below. |
| Codex | Sign in inside Codex, or export `OPENAI_API_KEY`. Review Vibead's hooks in `/hooks` if requested. |
| Gemini CLI | Select authentication inside Gemini, or export `GEMINI_API_KEY` / `GOOGLE_API_KEY` and select the matching method. |
| OpenCode | Connect/select your provider inside OpenCode. For the OpenAI route, export `OPENAI_API_KEY` and select an available OpenAI model. |

Use a model your account can access. Select or change models inside the agent. Existing credentials in the shell are passed to the live session; do not paste tokens into prompts, command arguments, reports or issues. Provider charges may apply. Temporary login state is deleted when the test exits, so another session may require signing in again.

Custom gateway environment passthrough in beta.3 is supported for the three Claude variables below. For the other agents, use the account/key methods above; their usual saved gateway settings are not imported.

### Claude Code through your gateway (beta.3 or later)

If `ANTHROPIC_BASE_URL`, `ANTHROPIC_MODEL` and `ANTHROPIC_AUTH_TOKEN` are already exported in your terminal, continue to step 3. Otherwise, this **macOS zsh** example sets them for one test. Replace the URL and model with your gateway's Anthropic-compatible endpoint and exact model identifier:

```zsh
(
  unset ANTHROPIC_API_KEY
  export ANTHROPIC_BASE_URL="https://your-gateway.example"
  export ANTHROPIC_MODEL="your-gateway-model-id"
  read -rs 'ANTHROPIC_AUTH_TOKEN?Gateway token: '; echo
  export ANTHROPIC_AUTH_TOKEN
  ./vibead-beta claude --mode interactive
)
```

Enter only the token at the hidden prompt, without a `Bearer ` prefix. This block starts Claude, so continue to step 4 afterward. The parentheses keep its settings local to this test. Beta.2 filtered these variables; use beta.3 or later. Claude adds the bearer prefix itself; see [Claude's gateway setup](https://code.claude.com/docs/en/llm-gateway-connect). Vibead does not add the token or gateway URL to its report.

## 3. Start one agent

Choose the row for your installed agent and your terminal. **Keep `--mode interactive`.**

| Agent | macOS / Linux | Windows PowerShell |
| --- | --- | --- |
| Claude Code | `./vibead-beta claude --mode interactive` | `.\vibead-beta.exe claude --mode interactive` |
| Codex | `./vibead-beta codex --mode interactive` | `.\vibead-beta.exe codex --mode interactive` |
| Gemini CLI | `./vibead-beta gemini --mode interactive` | `.\vibead-beta.exe gemini --mode interactive` |
| OpenCode | `./vibead-beta opencode --mode interactive` | `.\vibead-beta.exe opencode --mode interactive` |

Complete any onboarding, provider, model or workspace-trust prompts. The terminal prints the unique `Beta … [Ad]…` phrase to look for. Each session has a ten-minute limit.

## 4. Check the result

1. Submit: “Compare five sorting algorithms and explain their tradeoffs. Do not use tools or change files.”
2. During thinking, look for the disclosed `Beta … [Ad]…` message replacing the status text.
3. Wait for the complete answer. Check that the ad disappears and the answer remains readable. Repeat with a longer prompt if the response finishes too quickly to show an ad.
4. Exit the agent normally; for example, use `/exit` in Claude. Wait for Vibead's result and report path.

A successful run ends with `Vibead beta: passed`. Reports are saved under `vibead-beta-results` in the folder where you launched Vibead. Your visual check of the answer matters: interactive mode observes turn completion but does not compare the answer against a predefined expected response.

If a test fails, retain its report even if a retry passes. Review the JSON, then attach it to a [beta issue](https://github.com/gwasan/vibead-cli/issues) with your OS, agent version, selected model, test mode and what you observed. Reports stay local until you choose to share them. They contain versions, timings and checks, not prompt text, terminal captures, model responses or credentials. Do not share your token or private gateway address.

## If something does not work

| Symptom | Next step |
| --- | --- |
| The test submits a prompt and finishes by itself | You ran fixture mode. Add `--mode interactive` to use your real model. |
| Agent executable missing | Check that the agent starts by its normal command in this terminal. Install/fix that agent first, then retry Vibead. |
| Your usual login or provider is missing | Sign in or select the provider inside this temporary session, or use a supported exported key from step 2. |
| Claude gateway authentication fails | Check the URL, model and token with your gateway operator; use beta.3 or later. Enter the token without `Bearer `. Do not share it in an issue. |
| No ad appears | Wait for a longer response and check any native hook-trust prompt. A slow/unavailable ad or an unmatched thinking row leaves the agent's native output visible. Save the report if it still fails. |
| `failed` or `blocked` | Keep the JSON report. These are not passes, even if the agent itself answered. |

## Optional: simulated diagnostic and automated real-model check

| Mode | What it does | When to use it |
| --- | --- | --- |
| `--mode interactive` | Your prompts and real model connection; local mock ads | **Primary beta test** of the actual customer experience |
| `--mode fixture` | Fixed prompt and local simulated responses; no provider credentials | Diagnose display/integration problems without account setup or model charges |
| `--mode authenticated` | Fixed factorial prompt through a real provider; requires a supported key/token | Additional automated check with a known final-answer marker |

In beta.3, omitting `--mode` selects **fixture**, for every agent. For example, `./vibead-beta claude` is equivalent to `./vibead-beta claude --mode fixture`. Exporting real credentials does not change that default; fixture mode ignores them.

Use `./vibead-beta AGENT --mode fixture` for the optional diagnostic, replacing `AGENT` with `claude`, `codex`, `gemini` or `opencode`. Windows uses `.\vibead-beta.exe`. Fixture success does not establish authenticated-provider success.

For the automated real-model check, use `--mode authenticated --model YOUR_MODEL`. It requires `OPENAI_API_KEY` for Codex and OpenCode (OpenAI route), `GEMINI_API_KEY` for Gemini, or `ANTHROPIC_API_KEY` / `ANTHROPIC_AUTH_TOKEN` for Claude. Claude also accepts the gateway URL and model variables; `--model` overrides `ANTHROPIC_MODEL`. Provider charges may apply. You do not need this mode to complete the primary interactive test.

## Platform notes

These builds are not publisher-signed or notarized. macOS uses an ad hoc signature; Windows may show an unrecognized-publisher warning. Hosted tests do not establish physical-desktop approval or enterprise-policy behavior. Do not disable system-wide security controls to run a beta.

A Windows Codex fixture teardown can print an `AttachConsole failed` helper message. The qualified runs passed the display and cleanup checks despite that warning; retain the JSON report and judge the result by its status. [Release notes](https://github.com/gwasan/vibead-cli/releases/tag/v0.1.0-beta.3) list the tested versions and remaining limits.

## Remove or upgrade

Exit the beta, then delete its extracted folder and reports you no longer need. No system service is installed. Upgrade by extracting a complete new archive into a fresh folder; do not mix files from different builds.

This is an isolated display-test companion. Persistent installation, upgrade/restoration and full lifecycle acceptance remain later work. Synthetic ads generate no earnings or credits, and local tests do not establish production advertising or server performance.
