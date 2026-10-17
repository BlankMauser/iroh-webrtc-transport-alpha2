# Changelog

## Unreleased — Iroh 1.3 migration

Iroh is now 1.3.0. Its upstream defaults are inherited, not locally overridden:

- Default relay hostnames are now production `*.relay.n0.iroh.link`, replacing
  `*.iroh-canary.iroh.link`.
- The `presets::N0` endpoint preset adds a Pkarr resolver alongside DNS lookup,
  which can generate additional lookup traffic.
- Default QUIC keep-alive is now 5 seconds (previously disabled).

These apply where callers use the corresponding defaults; explicit relay,
lookup, transport, and QUIC configuration still takes precedence. Minimal or
relay-disabled endpoints do not automatically gain the N0 preset configuration.
