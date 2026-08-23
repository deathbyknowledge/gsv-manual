# Operating Model

[System Internals](index.md)

## Control Plane

The Gateway is intentionally lightweight. The Kernel owns identity, authorization, configuration,
Conversation directories, process registry, adapter routes, schedules, and inference coordination.
Heavy native work stays on machines/providers/specialized Workers.

Managed HTTP first resolves an accepted hostname through Accounts. The immutable installation ID
addresses the Kernel and scopes Process, Conversation, R2, ripgit, and adapter state. Standalone uses
the explicit `singleton` projection to preserve supported upgrades.

## Durable State

- Kernel SQLite stores users, capabilities, config, processes, routes, schedules, receipts, mail
  intents, and Conversation directory state.
- Process SQLite stores execution messages, current/queued runs, tool dispatches, approvals, and
  lifecycle metadata.
- Each Conversation Durable Object stores hot canonical Messages and an index of archived segments.
- Installation-scoped R2 stores large/immutable resources and archive objects.
- ripgit backs account home repositories and filesystem history.

Process deletion never means Conversation deletion. Immutable resource retention lets canonical
Messages survive live Process cleanup without duplicating bytes into Conversation storage.

## Raw Durable Objects

Kernel and Process behavior is composed directly around Cloudflare Durable Objects. GSV owns its
WebSocket handling, scheduling, MCP client integration, cancellation, and SQLite state machines; it
does not rely on PartyServer/Agents inheritance for those semantics.

Scheduled ticks intentionally break long agent work into new Durable Object events. This resets
subrequest budgets and leaves abort/reset/kill available between model/tool cycles.

## Streaming Data Plane

The frame is the control plane; the body stream is the data plane. Provider output, file transfer,
adapter media, R2 content, and other binary bodies cross Worker and Durable Object RPC as real
byte-oriented `ReadableStream` values.

No intermediary makes a recursive per-token service call. Backpressure flows from the consumer to
the producer. Cancellation propagates to the component that owns the active read/request, and a body
has exactly one terminal outcome: consumed, forwarded, or cancelled.

Some runtime byte streams can detach enqueued buffers. Code that forwards pooled or reusable input
must enqueue an owned copy at that boundary; it must not corrupt sibling chunks or a Node buffer
slab.

## Agent Loop

A Process tick loads AI config, context, capabilities, target descriptions, and offered tools;
assembles provider history; calls inference; stores raw reasoning/text/tool blocks; dispatches tools;
and requires explicit Message or Silence completion.

Direct input may supersede the active run. Runtime/scheduler events queue. Persistent run and
dispatch identities fence late output after cancellation, reset, replacement, or eviction.

## For Agents

Fix shared behavior at the owning syscall/protocol/runtime boundary. Avoid client-specific patches,
adapter-specific Kernel logic, and defensive revalidation of values already parsed into trusted
internal types.
