# Vibead CLI beta

Vibead replaces supported AI coding agents' generic terminal thinking text with a short, visibly disclosed advertisement. If an ad is unavailable or a row cannot be safely matched, the agent keeps its native output.

## Current status — September 30, 2026

**Native beta executables are implemented and undergoing release qualification. No public download is available yet.** This repository contains customer documentation; development source and server code remain private. No npm package or marketplace listing has been published.

The compiled replacement core is checked against the original renderer for identical terminal output, Unicode handling, styling, clearing and resizing. The beta launcher manages its own temporary mock ad service and model simulator, so testers will not need private-repository access or manual server setup.

Current packaged-agent qualification:

| Hosted platform | Codex, Claude Code, Gemini CLI and OpenCode |
| --- | --- |
| Ubuntu 24.04 x64 | All four passed with simulated model responses |
| macOS 15, Apple Silicon | All four passed with simulated model responses |
| macOS 15, Intel | All four passed with simulated model responses |
| Windows Server 2025 x64 | All four passed with simulated model responses |

These are candidate-build results. The exact published archives must pass qualification before download links appear. Authenticated-provider and physical-desktop acceptance remain separate stages. The tested agent versions are Codex 0.158.0, Claude Code 2.1.283, Gemini CLI 0.61.0 and OpenCode 1.18.33.

## How beta testing will work

Once a qualified archive is available in [Releases](https://github.com/gwasan/vibead-cli/releases), download the version for your computer, verify its accompanying SHA-256 checksum, and extract the complete folder. You need your chosen agent installed on your PATH. Vibead will not require npm, Docker, a compiler or a source checkout.

Open a terminal in the extracted folder. On macOS/Linux:

```sh
./vibead-beta claude
```

On Windows PowerShell:

```powershell
.\vibead-beta.exe claude
```

Replace `claude` with `codex`, `gemini` or `opencode`. The default test uses the real agent UI with simulated local model responses and synthetic local ads. It checks replacement, clearing, preserved answers and cleanup, then saves a local pass/fail report. No provider key or paid model request is needed for this stage.

After the fixture passes, `--mode interactive` lets you test an authenticated model in an isolated session. A new vendor login or API key may be needed, and provider charges may apply. Automated authenticated-model qualification remains paused pending provider credentials.

[Read the beta testing guide](BETA.md) for platform selection, commands, reports and removal. The instructions apply to a qualified archive; they are not an available installer until a release appears.

## Beta scope

This is an isolated display-test companion, not a persistent installation. It offers no earnings or credits. Persistent installation, upgrade, disable/enable and full lifecycle acceptance remain later release work.

The initial builds are not publisher-signed/notarized; operating-system approval may be required. Keep all extracted files together. To remove the beta, exit it and delete its folder and any local reports you no longer need.
