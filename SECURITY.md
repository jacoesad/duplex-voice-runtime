# Security Policy

## Supported versions

Until the first stable release, security fixes are applied to the latest commit
on `main`.

## Reporting a vulnerability

Do not report security vulnerabilities through a public issue.

Use GitHub private vulnerability reporting for this repository. Include:

- A description of the vulnerability and its impact.
- A minimal reproduction or affected message sequence.
- The affected revision and runtime environment.
- Any suggested mitigation.

Reports should avoid real credentials, private call recordings, personal data,
and proprietary model artifacts.

## Security-sensitive areas

The following areas require particular care:

- SIP, RTP, WebSocket, and media-frame parsing.
- Authentication and management endpoints.
- Unbounded queues or attacker-controlled allocation.
- Session identity, stale-generation rejection, and delivery idempotency.
- Native FFI, codec, and inference runtime boundaries.
- Prompt, tool, and model-provider inputs and outputs.
- Logs, traces, recordings, and conversation history.

Dependency vulnerabilities do not automatically prove exploitability, but they
must be assessed against the enabled features and deployment boundary.
