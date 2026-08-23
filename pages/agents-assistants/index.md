# Personal Intelligence & Work

[Back to GSV Manual](../../index.md)

Personal is the durable relationship the user talks to. Processes are the durable execution units
that perform and expose work.

## Personal Intelligence

Personal has an account identity, home directory, context, capabilities, and one canonical Home
Conversation. The Kernel maintains one current Personal Process slot per owner. Resetting that
Process clears its raw history while preserving the slot; killing it leaves the slot empty until the
next Personal interaction creates a fresh Process.

The stable thing is the role and address—not an immortal PID or one ever-growing transcript.

## Work Processes

Every other interactive Process is Work. It may run as the Personal account or another owned agent
account, but that does not make it Personal. Work can be created directly, delegated by another
Process, scheduled, observed, reset, or killed.

The Work UI never silently changes Home. Opening one Process creates a visibly labeled Work Session;
Back returns to Personal.

## Conversations

Home, Work, and adapter groups are canonical Conversations. Conversation messages live independently
from Process histories and name the Process/run that handled an interaction when relevant. See
[Conversations & Delegation](conversations-delegation.md).

## Context And Safety

Accounts supply identity and standing context. Capabilities and tool-approval policy decide what a
Process may attempt and what needs human confirmation. See
[Identity, Context, Resources & Approvals](identity-context-approvals.md).

## For Agents

Use delegation for bounded parallel work, not as a substitute for answering. Child output is not
automatically user-visible. Personal should synthesize useful results and explicitly choose Message
or Silence.
