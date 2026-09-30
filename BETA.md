# Test Vibead with your installed agent

Use a qualified archive from [Releases](https://github.com/gwasan/vibead-cli/releases). If no release is listed, executable qualification is still in progress. You need an installed supported agent on your PATH; no private repository access, npm installation, compiler, Docker or separately managed ad server is needed for Vibead.

## Download and extract

Choose the archive matching your computer:

| Computer | Archive platform |
| --- | --- |
| Mac with Apple Silicon | `darwin-arm64.tar.gz` |
| Mac with Intel processor | `darwin-x64.tar.gz` |
| Windows x64 | `win32-x64.zip` |
| Linux x64 | `linux-x64.tar.gz` |

Download its `.sha256` file too. On macOS, compare `shasum -a 256 ARCHIVE` with the checksum; on Linux use `sha256sum ARCHIVE`; on Windows use `Get-FileHash ARCHIVE -Algorithm SHA256`. Extract the complete archive and keep its files together. Open a terminal in the extracted `vibead-beta-PLATFORM-ARCHITECTURE` folder.

These early beta builds are not publisher-signed or notarized. macOS uses an ad hoc signature; Windows may show an unrecognized-publisher warning. Physical-desktop approval and enterprise-policy behavior are not established by the hosted test results. Do not disable system-wide security controls to run a beta.

## Run one agent test

macOS or Linux:

```sh
./vibead-beta claude
./vibead-beta codex
./vibead-beta gemini
./vibead-beta opencode
```

Windows PowerShell:

```powershell
.\vibead-beta.exe claude
.\vibead-beta.exe codex
.\vibead-beta.exe gemini
.\vibead-beta.exe opencode
```

Run only the commands for agents you have installed. Each command opens that real agent in a temporary empty workspace, starts its own synthetic ad service and local model simulator, and submits a fixed test prompt. It checks that a disclosed test ad replaces a supported thinking row, clears at completion and preserves the final answer. It then stops its services and removes the temporary agent configuration.

The default uses simulated model responses, with no provider API key or paid model request. Test ads are synthetic; there are no earnings or credits. Native hook trust and organization policies still apply. Normal agent settings are not modified.

A successful run ends with `Vibead beta: passed` and the location of a JSON report under `vibead-beta-results` in your current directory. `failed` is a failed test, even if the agent itself answered. Retain the failed report if you retry. A slow ad request deliberately leaves the agent's native status unchanged.

## Try your authenticated model afterward

After the fixture passes, use your provider credentials already set in your shell or sign in within the temporary agent session:

```sh
./vibead-beta claude --mode interactive
```

On Windows, use `.\vibead-beta.exe claude --mode interactive`. Replace `claude` with your chosen agent. Submit a prompt that takes several seconds, wait for the answer, then exit the agent normally. The session has a ten-minute limit. Your usual stored login is not copied into the isolated home; a new login may be needed and the temporary login state is deleted afterward. Provider charges may apply. Do not put secrets in command arguments or reports.

Authenticated-provider testing is a separate stage. Fixture success does not establish authenticated success. See the specific release notes for versions and platforms actually tested.

## Report the outcome and remove the beta

Reports contain versions, timings and boolean checks, not prompt text, source code, terminal captures, model responses or credentials. They stay local. Review a report before choosing to share it in an issue, along with your OS, agent version and whether you used fixture or interactive mode. Avoid screenshots containing personal information.

This is an isolated display-test companion, not a persistent installed product. To remove it, exit any active beta session, then delete the extracted folder and any reports you no longer need. There is no system service or persistent activation to uninstall. Upgrade by extracting a newer complete archive into a new folder; do not mix files from different builds.

Full product acceptance still requires persistent installation, upgrade, disable/enable, restoration, physical-terminal and authenticated-model checks. The local mock does not establish hosted latency, production authorization, advertiser delivery, impressions or earnings.
