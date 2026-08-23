# Targets, Execution & File Transfer

[Machines & Targets](index.md)

## Same Primitive, Different Target

Routable filesystem, shell, and network syscalls keep one meaning across targets. `target: "gsv"`
uses the Gateway implementation; a machine ID forwards the request to `gsvd`. The Kernel performs
authorization and routing before the target executes it.

The target that accepts a request or body owns completion, cancellation, and cleanup. A disconnect,
timeout, or malformed response must terminate both the request route and its binary stream.

## Machine Targets

Use a machine for:

- files that should remain on that computer;
- installed command-line tools;
- private/VPN networks;
- GPUs or other local compute;
- hardware such as cameras and microphones;
- credentials that should not be copied to the Gateway.

`gsvd` runs as an unprivileged user and stays in the foreground under the OS service manager. It owns
shell sessions, subprocesses, network requests, reconnection, and cancellation.

## Browser Targets

The browser extension exposes explicitly supported browser-side primitives. Browser state and
automation remain in that target rather than being implemented inside the Kernel.

## File Transfer And References

`fs.transfer.send` streams bytes from a target and `fs.transfer.receive` streams them into a target.
Structured frames carry size, type, path, revision, and ownership metadata; the body is a
backpressured `ReadableStream<Uint8Array>` across WebSocket, Worker service RPC, and Durable Object
RPC boundaries.

Cross-target copy names both source and destination. A resource reference can instead preserve an
exact immutable revision for later lazy resolution. The two operations serve different purposes:
copy creates another file; a reference avoids a copy until durable retention or consumption requires
one.

## Failure Semantics

If a source goes offline, changes revision, or loses authorization, GSV returns an explicit error.
It does not read a newer file with the same path. Partial readers and disconnected callers cancel
the body exactly once.

## For Agents

Prefer executing near the data. Copy only when a durable duplicate is useful, and prefer a revision-
bound reference when the consumer only needs to resolve the same bytes later.
