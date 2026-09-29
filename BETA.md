# Local beta design

**Planned behavior, not a released executable.** Installation instructions will accompany a qualified platform archive. No account secrets should be placed in issue reports or command arguments.

## One command for each agent

The target is a beta launcher that:

1. Detects the selected installed agent and checks compatibility.
2. Creates an isolated test workspace and starts a synthetic ad service on a temporary loopback port.
3. Launches the real agent through the packaged Vibead runtime.
4. Verifies that a disclosed test ad replaces a supported thinking row and disappears when the turn completes, while preserving the native answer.
5. Stops its own services and removes temporary configuration when the test exits or is interrupted.
6. Writes a local report containing versions, timings and pass/fail checks for the tester to review before sharing.

The intended experience requires no source checkout, manual server startup, fixed port, Docker installation or compiler. The local simulator belongs to a separate beta test companion; it is not a fallback ad catalog in the normal customer runtime.

## Two model stages

| Stage | Agent UI | Model response | Ad response | Account requirement |
| --- | --- | --- | --- | --- |
| Local smoke | Real installed agent | Local simulated response | Local mock service | No model-provider credentials for the test |
| Live model | Real installed agent | Authenticated provider | Local mock service | Supported provider credentials or native login; provider charges may apply |

A local ad server removes the need for an ad-service account during the controlled beta. It does not make real model requests free or remove the agent's authentication requirements. Native hook trust and organizational restrictions remain in effect.

Reports must not contain prompts, source code, terminal captures, model responses or credentials. Reports stay local unless the tester chooses to share them. The beta must clearly separate simulated-model results from authenticated results.

## Acceptance before release

The packaged artifacts need native testing for each advertised OS and architecture. Required checks include replacement, clearing, preserved answers, interruption, resizing, stopped-server fallback, cleanup, installation, upgrade behavior, disable/enable and uninstall restoration. A source-based test result alone does not qualify a customer executable.

The mock service validates local display behavior. It does not establish hosted-network latency, production authorization, real advertiser delivery, impressions or earnings. Those require separate hosted-product qualification.
