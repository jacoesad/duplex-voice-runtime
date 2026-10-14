# Contributing

Thank you for contributing to Duplex Voice Runtime.

## Development workflow

1. Create a short-lived branch from `main`.
2. Keep each pull request focused on one behavior or infrastructure change.
3. Add tests for new behavior and regressions.
4. Update `docs/spec.md` when a change affects architecture or contracts.
5. Run the required checks before opening a pull request.

Recommended branch prefixes:

- `feat/`
- `fix/`
- `docs/`
- `test/`
- `refactor/`
- `chore/`

## Required checks

```bash
cargo fmt --check
cargo test
cargo clippy --all-targets --all-features -- -D warnings
```

Do not commit build artifacts, credentials, recordings containing private data,
or proprietary model weights.

## Design expectations

- Conversation state has one explicit owner.
- Async queues are bounded.
- External operations have timeout and cancellation behavior.
- Provider results carry enough identity to reject stale work.
- Native runtime boundaries are isolated behind safe Rust adapters.
- Logs and errors do not expose credentials or raw sensitive payloads.

## Pull requests

Pull requests should explain:

- The behavior being added or changed.
- The invariants affected.
- The tests that demonstrate the behavior.
- Any native runtime, model, or deployment dependency introduced.
- The licensing implications of new dependencies or model weights.

## Licensing

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in this project is licensed under both the Apache License,
Version 2.0 and the MIT License, at the user's option, without additional terms
or conditions.
