# Protocol Roles & Trust

[Clients, Adapters & Extensions](index.md)

## Human Clients

Web, Desktop, and CLI authenticate as a human and call the ordinary Kernel syscall surface. They may
send Conversation input, receive directed Message streams, synchronize committed Messages, and
explicitly observe Processes. A client connection is not a machine target unless a separate driver
identity implements that role.

## Machine Drivers

`gsvd` connects with a driver-bound credential. It may implement selected filesystem, shell, and
network primitives for its machine ID. It cannot turn that transport into an arbitrary human login.

## Adapter Services

An adapter Worker authenticates provider traffic and calls the restricted service-binding entrypoint.
The Kernel derives the linked local human. Adapter service authority and delegated external-user
authority are intentionally different contexts.

Today, text commands such as process inspection are partly adapter-specific frontends. The planned
peer work would route permitted commands through the same syscall dispatcher with effective
capabilities equal to the intersection of user authority, adapter policy, and connection policy.

## Binary Bodies

Frame metadata is structured and bounded. Large or binary content is a `ReadableStream<Uint8Array>`
body:

- WebSocket clients use the protocol's binary-body channel.
- Worker and Durable Object RPC forward the `ReadableStream` directly.
- Providers and R2 are streamed at their owning boundary.

Intermediate code preserves backpressure and cancellation. It does not send one RPC per token/chunk,
base64-encode bodies, or collect the whole stream before forwarding. The receiver that accepts a body
owns consuming, forwarding, or cancelling it exactly once.

## Browser Extension

The extension is a browser target, not an installable Gateway package. It exposes intentionally
supported browser operations and remains subject to target routing and browser permission.

## For Agents

When adding an operation, fix the stable syscall/protocol boundary and then implement transport
adapters. Do not add separate semantics solely because one caller happens to use WebSocket and
another a service binding.
