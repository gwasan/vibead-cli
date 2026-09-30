# Try Vibead with your AI agent

Vibead replaces supported terminal thinking text with a short, disclosed test advertisement. **The main beta test uses your real model account or gateway.** Vibead starts its own local mock ad service; you do not need to run a server or access a private repository.

## 1. Download

Download [beta.3](https://github.com/gwasan/vibead-cli/releases/tag/v0.1.0-beta.3) for your computer and its accompanying `.sha256` file. [Verify the checksum](BETA.md#1-download-and-extract), extract the complete archive, and open a terminal in the extracted folder. Keep its files together.

| Computer | Download |
| --- | --- |
| Apple Silicon Mac | [macOS ARM64](https://github.com/gwasan/vibead-cli/releases/download/v0.1.0-beta.3/vibead-beta-0.1.0-beta.3-darwin-arm64.tar.gz) |
| Intel Mac | [macOS x64](https://github.com/gwasan/vibead-cli/releases/download/v0.1.0-beta.3/vibead-beta-0.1.0-beta.3-darwin-x64.tar.gz) |
| Windows x64 | [Windows ZIP](https://github.com/gwasan/vibead-cli/releases/download/v0.1.0-beta.3/vibead-beta-0.1.0-beta.3-win32-x64.zip) |
| Linux x64 | [Linux archive](https://github.com/gwasan/vibead-cli/releases/download/v0.1.0-beta.3/vibead-beta-0.1.0-beta.3-linux-x64.tar.gz) |

Your chosen agent must already be installed and available in this terminal. Vibead itself needs no npm installation, Docker or compiler. These beta builds are not publisher-signed or notarized; see the [platform notes](BETA.md#platform-notes).

## 2. Start your agent with a real model

On macOS or Linux, run **one** of these:

```sh
./vibead-beta claude --mode interactive
./vibead-beta codex --mode interactive
./vibead-beta gemini --mode interactive
./vibead-beta opencode --mode interactive
```

On Windows PowerShell, replace `./vibead-beta` with `.\vibead-beta.exe`, keeping the agent name and `--mode interactive`.

Sign in or select your provider inside the agent, or use a [supported API key already exported in your shell](BETA.md#2-connect-your-model-account). Vibead opens a temporary empty workspace; it does not copy your usual saved login or agent settings. Provider charges may apply.

**Using a Claude gateway?** Follow the [URL, model and token setup](BETA.md#claude-code-through-your-gateway-beta3-or-later) before starting. It requires beta.3 or later.

## 3. Check the ad and share your result

1. Complete any agent onboarding or hook-trust prompts. For Codex, check `/hooks` if requested.
2. Ask: “Compare five sorting algorithms and explain their tradeoffs. Do not use tools or change files.”
3. Watch for the `Beta … [Ad]…` message during thinking. It should disappear when the turn finishes, with the answer still readable. Try a longer prompt if the first answer is too fast.
4. Exit the agent normally. Vibead prints `passed`, `failed` or `blocked` and a JSON report path under `vibead-beta-results`.
5. Review the report, then share it in a [beta issue](https://github.com/gwasan/vibead-cli/issues) with your OS, agent version and what you observed. Never share credentials.

You do not need to pass a simulated test first. The [full testing guide](BETA.md) covers authentication, Windows commands, troubleshooting and removal.

## Why include `--mode interactive`?

In beta.3, `./vibead-beta claude` **works, but runs the automated simulated-model test**. The same default applies to all four agents. Use `--mode interactive` for the primary beta test: your prompts, your actual model connection, and your terminal. Ads remain local and synthetic in both modes.

For an optional no-credentials diagnostic, run `./vibead-beta claude --mode fixture`, replacing `claude` with your agent. A simulated pass does not establish that your real model connection works.

## What has been verified?

Beta.3 passed all sixteen packaged-agent simulated tests across Ubuntu 24.04 x64, macOS 15 Apple Silicon, macOS 15 Intel and Windows Server 2025 x64. Four additional Claude gateway checks passed using a local simulator. Tested agents: Codex 0.158.0, Claude Code 2.1.283, Gemini CLI 0.61.0 and OpenCode 1.18.33. These results do not establish success with your provider, model or desktop terminal; that is what the primary beta test helps check.

This beta is an isolated display-test companion. Persistent installation and full lifecycle acceptance remain later work. Test ads generate no earnings or credits. Source and server code remain private; no npm package or marketplace listing has been published.

This online guide is the current procedure. Instructions bundled in an earlier download may still lead with the simulated test; the beta.3 commands above work with the existing download.
