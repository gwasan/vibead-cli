# Beta test with your existing AI agent setup

**Beta.4 keeps the setup you already use:** your home directory, saved login, model/provider configuration, custom configuration directories, project files, settings, plugins and exported environment. You launch through Vibead from your usual project, and it adds local mock advertisements during supported thinking states.

No new account setup, private checkout or separate ad server is required by Vibead. Your agent's own permissions, trust prompts and provider charges still apply.

## Mac quick start: Claude Code, Codex and OpenCode

**Ready to try:** both Apple Silicon and Intel Mac downloads are published. Automated tests passed with real agent executables and simulated model responses. This test with your own account checks your normal provider and desktop experience too.

1. Open Apple menu → **About This Mac**. A **Chip** such as Apple M1/M2/M3/M4 means Apple Silicon; an **Intel Processor** means Intel. Download **both files in the matching row** into Downloads:

| Your Mac | Archive | Checksum file |
| --- | --- | --- |
| Apple Silicon | [Download ARM64](https://github.com/gwasan/vibead-cli/releases/download/v0.1.0-beta.4/vibead-beta-0.1.0-beta.4-darwin-arm64.tar.gz) | [ARM64 checksum](https://github.com/gwasan/vibead-cli/releases/download/v0.1.0-beta.4/vibead-beta-0.1.0-beta.4-darwin-arm64.tar.gz.sha256) |
| Intel | [Download x64](https://github.com/gwasan/vibead-cli/releases/download/v0.1.0-beta.4/vibead-beta-0.1.0-beta.4-darwin-x64.tar.gz) | [x64 checksum](https://github.com/gwasan/vibead-cli/releases/download/v0.1.0-beta.4/vibead-beta-0.1.0-beta.4-darwin-x64.tar.gz.sha256) |

2. In Terminal, run the block for **your Mac only**. It checks the download and extracts it only if the checksum matches. These commands leave your terminal's working directory unchanged.

Apple Silicon:

```sh
(
  cd "$HOME/Downloads" &&
  shasum -a 256 -c vibead-beta-0.1.0-beta.4-darwin-arm64.tar.gz.sha256 &&
  tar -xzf vibead-beta-0.1.0-beta.4-darwin-arm64.tar.gz
)
```

Intel:

```sh
(
  cd "$HOME/Downloads" &&
  shasum -a 256 -c vibead-beta-0.1.0-beta.4-darwin-x64.tar.gz.sha256 &&
  tar -xzf vibead-beta-0.1.0-beta.4-darwin-x64.tar.gz
)
```

Expect a line ending in `OK`. If the check fails or either file is missing, download both files again before proceeding. If your browser already extracted and removed the archive, download it again with automatic extraction disabled. Keep the complete extracted folder together.

3. Open the same terminal and project where your agent already works. Stay in your project; you do not need to work from the download folder. Set the executable path in that terminal. For Apple Silicon:

```sh
VIBEAD_BETA="$HOME/Downloads/vibead-beta-darwin-arm64/vibead-beta"
```

For Intel:

```sh
VIBEAD_BETA="$HOME/Downloads/vibead-beta-darwin-x64/vibead-beta"
```

If you extracted elsewhere, change the path. This variable lasts for the current terminal session; set it again in a new terminal. Test one agent at a time:

| Agent | Start it | Exit after testing |
| --- | --- | --- |
| Claude Code | `"$VIBEAD_BETA" claude` | Enter `/exit` |
| Codex | `"$VIBEAD_BETA" codex` | Press Ctrl+C twice |
| OpenCode | `"$VIBEAD_BETA" opencode` | Enter `/exit` |

**No `--mode interactive` is needed in beta.4.** Your existing provider, model, login, exported environment and current project remain in use. If plain `claude` already works with `ANTHROPIC_BASE_URL`, `ANTHROPIC_MODEL` and `ANTHROPIC_AUTH_TOKEN`, keep those settings and launch Vibead from that same shell. Do not copy or send us your token. Saved Codex and OpenCode setups are reused in the same way.

Review any native trust prompt. In Codex, review the Vibead hooks and approve the ones you intend to run; `/hooks` opens the hook controls. Vibead does not approve customer hooks automatically. Close the hook menu before sending your prompt.

Ask a normal question, or try: “Compare five sorting algorithms and explain their tradeoffs. Do not use tools or change files.” Look for `Beta … [Ad]…` while the agent thinks, then check that the ad disappears and the answer remains readable. Very short turns may show no ad. Your normal model billing applies; the ad is local and synthetic.

Exit normally and review the report printed by Vibead, under `~/.vibead-beta/results`. Share only that report JSON and your observations in a [beta issue](https://github.com/gwasan/vibead-cli/issues). A `failed` or `blocked` report is not a pass even if the agent answered. The report section below explains what is recorded.

Repeat for each installed agent and share one report per agent. Include your Mac chip, macOS version, agent version, whether the ad appeared during thinking, and whether the answer and normal agent behavior stayed intact. To find the reports in Finder:

```sh
open "$HOME/.vibead-beta/results"
```

If you only see `Vibead beta: passed` from an automatic test without your normal session, check that you downloaded **beta.4** and omitted `--mode fixture`. Older releases used the simulated test by default.

If macOS blocks the executable, see [platform notes](#platform-notes). If you force-killed a session, use the [recovery command](#recovery-after-a-crash-or-forced-termination) before trying again or deleting the folder.

Gemini is also supported on qualified Mac builds: use `"$VIBEAD_BETA" gemini`. Other-platform availability is listed in the release; Windows beta.4 remains under qualification.

## 1. Download

Get an archive and its `.sha256` file from [beta.4 Releases](https://github.com/gwasan/vibead-cli/releases/tag/v0.1.0-beta.4):

| Computer | Archive ending |
| --- | --- |
| Mac with Apple Silicon | `darwin-arm64.tar.gz` |
| Mac with Intel processor | `darwin-x64.tar.gz` |
| Windows x64 | Beta.4 download pending qualification |
| Linux x64 | `linux-x64.tar.gz` |

Compare the checksum with the value in the `.sha256` file, replacing `ARCHIVE` with the downloaded filename:

| Terminal | Command |
| --- | --- |
| macOS | `shasum -a 256 ARCHIVE` |
| Linux | `sha256sum ARCHIVE` |
| Windows PowerShell | `Get-FileHash ARCHIVE -Algorithm SHA256` |

Extract the complete archive somewhere convenient. Keep all extracted files together. Your chosen AI agent must already be installed and working in the terminal you will use.

## 2. Open your usual project and launch

Use the same terminal, exported environment and project directory where you normally run your agent. Call the extracted executable by its full path; **do not change into the download folder to do your project work**.

Example for macOS/Linux; replace both paths with yours:

```sh
cd "/path/to/your/project"
"/path/to/vibead-beta" claude
```

Windows PowerShell:

```powershell
Set-Location "C:\path\to\your\project"
& "C:\path\to\vibead-beta.exe" claude
```

Choose the agent name you normally use:

| Agent | Argument after the executable path |
| --- | --- |
| Claude Code | `claude` |
| Codex | `codex` |
| Gemini CLI | `gemini` |
| OpenCode | `opencode` |

**The short command now uses your real setup by default.** Adding `--mode interactive` has the same effect in beta.4. You do not need to copy credentials into Vibead or sign in again just for the beta. Your agent can still request login if its existing credentials have expired or are unavailable.

Complete the agent's normal project-trust prompts. Approve the new Vibead hooks if your agent requests it; for Codex, check `/hooks`. Vibead does not approve hooks, change your permissions or disable organization policies for you.

### Keep your usual arguments

Put native arguments after `--` so they reach your agent:

```sh
"/path/to/vibead-beta" claude -- --model my-model
"/path/to/vibead-beta" codex -- --profile my-profile
"/path/to/vibead-beta" gemini -- --model my-model
"/path/to/vibead-beta" opencode -- --model provider/model
```

No model override is needed if you want the agent's saved default. Shell aliases and functions are not invoked by Vibead. If your normal alias supplies arguments or environment variables, supply those same arguments after `--` and export those variables in the shell before launching.

### Claude Code through your gateway (beta.3 or later)

In beta.4, keep the same gateway configuration that already works with plain `claude`: settings files or exported `ANTHROPIC_BASE_URL`, `ANTHROPIC_MODEL` and `ANTHROPIC_AUTH_TOKEN` remain available. Simply launch the wrapper from the same shell and project. The local mock ad service does not replace your model gateway.

If you are configuring a gateway for the first time, follow [Claude's gateway setup](https://code.claude.com/docs/en/llm-gateway-connect), confirm plain `claude` works, then launch through Vibead. Do not send us your token. The same principle applies to Codex, Gemini and OpenCode: keep their working provider setup; Vibead inherits it.

Beta.3 forwarded those three Claude variables but still used a fresh temporary home. Beta.2 filtered them. Use beta.4 for the full existing-setup path.

## 3. Check the ad during normal use

1. Submit your own prompt, or try: “Compare five sorting algorithms and explain their tradeoffs. Do not use tools or change files.”
2. During thinking, look for the disclosed `Beta … [Ad]…` phrase printed when Vibead started.
3. Check that the ad disappears when the turn completes and the answer remains readable. A very short turn may finish before an ad appears; try a longer prompt.
4. Keep working normally. The interactive session has no beta-imposed time limit.
5. Exit the agent normally when finished; for example, `/exit` in Claude.

This is your actual workspace. Agent file edits, conversation history, settings changes and authentication refreshes behave as normal; they are not discarded by the beta.

## 4. Review and share the report

Vibead prints the ad-test result and a report path, normally under `~/.vibead-beta/results` (`%USERPROFILE%\.vibead-beta\results` on Windows). Add `--report-dir DIRECTORY` before `--` to choose another location.

A `passed` report means the display checks passed for this session. `failed` or `blocked` is not a pass, even if the agent itself answered. Interactive mode does not compare the model's answer against a fixed expected response; your visual check matters. The wrapper preserves the agent's exit code, so judge ad-test success from the JSON status rather than the shell exit code.

Review the JSON and attach it to a [beta issue](https://github.com/gwasan/vibead-cli/issues) with your OS, agent version and what you observed. Reports contain versions, timings and checks, not prompts, terminal captures, model responses, credentials or project contents. Reports stay local until you choose to share them. **Share only report JSON from `results`; integration recovery files contain local settings backups and must not be shared.**

## How your setup is preserved

Vibead retains your working directory and provider environment. It temporarily merges its hooks into the selected agent's hook settings, or adds its OpenCode plugin. Your existing hooks and settings stay present. Claude also receives temporary launch settings for its generic thinking phrase. On normal exit, Vibead removes its integration, restores the original settings bytes when unchanged, and preserves other settings changes made during the session. It does not delete your agent's home or alter your shell configuration/vendor executable.

A second overlapping beta session for the same configuration, an existing Vibead integration, disabled hooks, managed restrictions, or an unsupported invocation can prevent safe attachment. In that case the agent runs normally without ads; the report does not claim success. Examples include Claude custom `--settings`, Codex inline `--config`/`--cd` overrides, and sandboxed Gemini hooks. Existing provider settings loaded normally from your files are retained.

### Recovery after a crash or forced termination

Normal exit handles cleanup automatically. A power loss or force-kill can leave temporary hooks and a local recovery journal. Close other beta sessions for that agent, then run from the same account and configuration environment:

```sh
"/path/to/vibead-beta" claude --cleanup
```

Replace `claude` with your agent. Windows uses `& "C:\path\to\vibead-beta.exe" claude --cleanup`. This command needs no model request. It refuses to clean up a live beta session. If cleanup reports an error, retain the archive and recovery files; report the error without uploading those files. Do not delete recovery state while cleanup is pending.

## Optional isolated checks

| Mode | What it does |
| --- | --- |
| No mode, or `--mode interactive` | **Primary beta:** your existing setup, project and real model; local mock ads |
| `--mode fixture` | Temporary empty home, fixed prompt and local simulated model; no account or model charges |
| `--mode authenticated` | Temporary empty home and fixed factorial prompt using an exported provider key/token |

To run an optional diagnostic, use `"/path/to/vibead-beta" AGENT --mode fixture`, replacing `AGENT` with any of the four agent names. You do not need to pass it before using the primary beta. Fixture success does not establish that your usual provider works.

The separate automated authenticated mode requires `OPENAI_API_KEY` for Codex/OpenCode, `GEMINI_API_KEY` for Gemini, or `ANTHROPIC_API_KEY` / `ANTHROPIC_AUTH_TOKEN` for Claude. It accepts `--model MODEL`; Claude also accepts the gateway URL/model variables. Unlike the primary mode, it does not reuse saved account configuration. Provider charges may apply.

## Platform notes

**OpenCode beta.4 display issue:** some normal thinking layouts are not recognized, including titled reasoning headers and the static spinner used with animations disabled. Ads may be assigned without becoming visible. A correction has passed local native-renderer tests but is not yet in these downloads. If affected, share your report and the status label you saw; do not change your OS, provider or working setup, or keep spending model turns on longer prompts to retry this issue.

These builds are not publisher-signed or notarized. macOS uses an ad hoc signature; Windows may show an unrecognized-publisher warning. Hosted tests do not establish desktop approval or enterprise-policy behavior. Do not disable system-wide security controls to run a beta.

Windows Codex teardown can print an `AttachConsole failed` helper warning even when display/cleanup checks pass. Retain the JSON report and check its status. [Release notes](https://github.com/gwasan/vibead-cli/releases/tag/v0.1.0-beta.4) identify tested versions, platforms and known limits.

## Remove or upgrade

Exit active beta sessions and complete any pending `--cleanup` before deleting the extracted archive. Reports can be deleted separately. Upgrade by extracting the complete newer archive into a fresh folder; do not mix runtime files from different builds. Beta.4 changes the short command from simulated testing to using your real setup.

This remains an explicit wrapper; automatic activation through your normal agent command is separate distribution work. Synthetic ads generate no earnings or credits. Real-provider, physical-desktop and full lifecycle acceptance remain distinct from the simulated-model qualification recorded in release notes.
