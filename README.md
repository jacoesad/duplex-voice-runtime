# Duplex Voice Runtime

A real-time, full-duplex voice agent runtime written in Rust.

The project starts with a typed session and dialog core, then adds a minimal
tool/retrieval loop, streaming media, barge-in, telephony, and production
infrastructure.

See [docs/spec.md](docs/spec.md) for the architecture and staged delivery plan.

## Status

This project is in its initial scaffolding phase. It does not provide a usable
voice agent yet. Dependencies and module boundaries are introduced only when
their implementation phase starts.

## Design goals

- Keep session, cancellation, interruption, and delivery correctness in Rust.
- Use one state-owning actor per call.
- Keep prompt, history, tools, and retrieval behind an explicit dialog boundary.
- Reject stale model and audio output with generation identities.
- Apply bounded queues and explicit backpressure throughout the pipeline.
- Support native runtimes and remote providers behind narrow Rust adapters.

## Planned architecture

```text
PSTN / SIP / WebRTC
        |
  media transport
        |
     SessionActor <----> DialogEngine ----> ModelGateway
       /   |   \             |
     ASR  TTS  ToolExecutor  +----> Retrieval
       \   /
      playback
         |
 state and telemetry
```

The implementation proceeds through independently testable milestones:

1. Domain identities, orthogonal states, and deterministic event replay.
2. Text-only dialog engine with prompt and history snapshots.
3. One idempotent tool loop and one fake retrieval path.
4. Offline WAV speech loop.
5. Real-time streaming media and intelligence.
6. Full-duplex barge-in with round and delivery semantics.
7. Persistence, configuration snapshots, and event records.
8. SIP telephony.
9. Reliability, performance, and multi-instance deployment.
10. Optional outbound-calling product capabilities.

## Development

Install the stable Rust toolchain, then run:

```bash
cargo fmt --check
cargo test
cargo clippy --all-targets --all-features -- -D warnings
```

Development happens on short-lived branches and is merged through pull
requests. See [CONTRIBUTING.md](CONTRIBUTING.md) for the workflow.

## Security

Please report vulnerabilities privately as described in
[SECURITY.md](SECURITY.md).

## License

Licensed under either of:

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE))
- MIT License ([LICENSE-MIT](LICENSE-MIT))

at your option.

Third-party libraries, native runtimes, and model weights may use different
licenses. Users are responsible for reviewing those licenses before
distribution or commercial use.
