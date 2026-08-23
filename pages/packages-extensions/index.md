# Clients, Adapters & Extensions

[Back to GSV Manual](../../index.md)

GSV exposes one typed frame protocol and stable syscall primitives through several authenticated
transports. The participants are related, but the full “protocol peer” unification is not finished.

## Current Participants

- Web, Desktop, and CLI are human clients over WebSocket.
- `gsvd` is a driver client that implements target-routed syscalls.
- Adapter Workers use service bindings for provider control, inbound events, and outbound delivery.
- The browser extension implements a browser-backed target.
- `packages/gsv` is the public TypeScript protocol/client library.

The old installable package runtime, package agents, catalogs, and app-runner no longer exist. Do not
use historical package commands or describe package installation as a current extension mechanism.

## Shared Foundations

All transports use explicit structured frames, cancellation, and separately owned binary streams.
Canonical Conversations and committed Messages give clients and adapters the same user-visible
message semantics. Service-bound adapters still have a deliberately narrower entry path than human
clients.

## Deferred Peer Unification

The intended next step is to describe a participant by principal, transport, and negotiated
facilities. That would let an adapter invoke an attenuated set of ordinary user syscalls and let a
native client register as a directed endpoint without conflating either with a hardware target.

This is a proposal, not a current compatibility promise. See
[Protocol Roles & Trust](trust-entrypoints-source.md).

## Pages In This Section

- [Protocol Roles & Trust](trust-entrypoints-source.md)
- [Extensions Today & Roadmap](catalogs-visibility.md)

## For Agents

Do not infer syscall authority from transport. A service binding proves participation in the
deployment graph; it does not grant arbitrary user impersonation.
