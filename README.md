# iroh-webrtc-transport

Iroh + WebRTC = Even More Weird Web Stuff

> Whoa, hold on there partner!

1. This is still very much experimental
2. The API surface may still change as the transport model settles

## Iroh version

This BlankMauser branch targets Iroh / iroh-base / noq-udp 1.3 and
n0-watcher 1.0; the chat example uses iroh-gossip 0.101. Custom receives
use `RecvInfo` without a local-address hint. Sends continue to select the
registered WebRTC session by destination, ignoring the optional source hint.
Browser hooks use `Connection` and borrowed `Path` snapshots.

Validation: `cargo test -j4` in `crates/iroh-webrtc-transport`, plus
`cargo check --target wasm32-unknown-unknown --no-default-features --features browser -j4`.
Both Rust browser examples are checked with `cargo check --target wasm32-unknown-unknown -j4`.
These compile checks do not replace browser interoperability testing.

## So what do you get for free?

The goal is that application code should not need to know much about WebRTC ceremony. You ask for an Iroh-style connection, and the crate handles the browser mess behind it.

- Browser Wasm facade that exposes Iroh-style endpoint IDs, dial, accept, and stream APIs
- WebRTC channel bootstrapping with signaling using Iroh's relays
- Native WebRTC implementation so browser clients can connect directly to native clients and vice versa.
- Endpoints, ALPNs, connections, and streams; it's still "just Iroh."

I tried my hardest to have the crate bury all the WebRTC setup and Iroh custom transport glue.
