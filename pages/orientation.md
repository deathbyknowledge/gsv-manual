# Orientation

[Back to GSV Manual](../index.md)

The intended experience is one intelligence with visible work—not a chat application full of
interchangeable agents.

## Personal Home

Each human owner has a Personal intelligence identity and one current Personal Process. The Process
is replaceable; the identity, home files, standing context, and Home Conversation are durable.

Private Web, Desktop, CLI, Telegram, WhatsApp, and Discord interactions normally enter the same
Home Conversation. A linked messenger does not create another assistant. Background events such as
managed email also reach the Personal Process, which decides whether to send a Message or remain
silent.

## Visible Work

Personal may create or delegate to other Processes. Those are pieces of work, not additional
personal intelligences.

- **Home** is where you talk to Personal.
- **Work** lists Processes and lets you inspect, reset, kill, or explicitly open one.
- A **Work Session** is a direct line into one Process. The UI labels it clearly and provides a way
  back to Home.
- Child results return to their caller as Process events. Personal decides what deserves a
  user-visible Message.

Killing a Work Process removes its live execution state but does not erase canonical Conversation
messages. Process archives remain available according to lifecycle and retention policy.

## Messages And Process Activity

GSV deliberately keeps two projections:

- **Messages** are the canonical, user-visible Conversation stream. A model must explicitly choose
  `Message` or `Silence`; ordinary model text is not automatically delivered.
- **Process activity** is the inspectable execution trace, including model reasoning when the chosen
  provider supplies it, drafts, tool calls, results, errors, and retries.

Only the endpoint that started a run receives transient Message deltas. Other signed-in clients
synchronize the committed Message. Inspecting a Process explicitly subscribes that client to its raw
activity; it does not turn all Process output into a user Message.

## Where Work Runs

Every routable filesystem, shell, or network call names a target:

- `gsv` runs inside the Gateway environment.
- A machine ID runs on a connected `gsvd` daemon.
- Browser-backed operations run through the browser extension target.

The Kernel authorizes and routes the call. The target owns execution, cancellation, and any binary
body it accepts. A target name identifies a destination; it is not a credential.

## Managed And Standalone

- **Standalone** deploys into the user's Cloudflare account. The user supplies provider and adapter
  credentials. Managed email is unavailable.
- **Managed** hosts multiple isolated installations. The installation ID is the outer security and
  storage boundary. Platform inference, managed email, and the shared managed Telegram bot may be
  available according to deployment configuration and limits.

Both modes use the same Kernel, Process, Conversation, syscall, and client concepts. Managed
services do not weaken installation isolation or let public callers choose an installation ID.

## Current Limits

- Onboarding creates the first owner. General multi-human invitation, membership, and password
  recovery are not yet a complete product flow.
- WebSocket clients and service-bound adapters share core message semantics but are not yet one
  fully negotiated protocol-peer implementation.
- Managed entitlements and billing controls are planned; limits currently live in the services that
  enforce them.
- Public Desktop distribution still needs the platform-specific signing and release work described
  in [Web & Desktop](apps-desktop/index.md).

## For Agents

Determine whether the user wants a canonical Message, raw Process inspection, a new Work Process, or
execution on another target. Do not create a new agent identity when a Process is enough, and do not
mistake a Work Session for Personal Home.
