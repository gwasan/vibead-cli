# Vibead CLI

Vibead replaces supported AI coding agents' generic terminal thinking text with a short, visibly disclosed advertisement. The intended integrations are Codex, Claude Code, Gemini CLI and OpenCode. If an ad is unavailable or the terminal cannot be safely matched, the agent keeps its native output.

This is the public distribution repository for customer documentation and future reviewed CLI releases. Development source and production server implementation are maintained separately.

## Release status

**Customer executable packaging is in progress.** This repository does not yet contain an installable CLI release, npm package, marketplace plugin or setup skill. Do not treat a proposed command as an available installation method. Customer-artifact compatibility will be documented with each qualified release.

## Planned beta experience

Download the appropriate beta archive, open a terminal, and run one test command for your installed agent. The beta launcher will start and stop a local mock ad service automatically. Test ads are synthetic; the beta does not offer earnings or credits.

See [the beta design](BETA.md) for what is planned, what requires an agent account, and what a successful test must demonstrate.

The customer runtime will contain only local integration and display functionality. Private campaign selection, advertiser credentials and financial logic will remain outside the client. Distributing executable software does not make the code running on a customer's computer inaccessible to inspection.
