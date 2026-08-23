# Accounts & Access

[Back to GSV Manual](../../index.md)

Accounts answer who is acting. Capabilities and owned runtime records answer what that identity may
do. Authentication, authorization, Process identity, and external-message linking are related but
separate boundaries.

## Current Account Roles

- A **human account** logs in, owns Processes, Conversations, files, integrations, and machines.
- A **Personal agent account** holds that human's durable Personal identity and home.
- Other **agent accounts** may have distinct context and capabilities.
- **Driver identities** authenticate machines.
- **Service identities** authenticate deployment components such as adapter Workers.

Onboarding currently creates the first human owner and Personal identity. The underlying Kernel has
users, groups, ownership, and capabilities, but a complete product flow for inviting additional
humans, managing shared Conversations, and self-service password recovery is not finished. Do not
present those as shipped features.

## Authorization

The Kernel enforces access even when a caller or UI already checked it. A capability allows a class
of syscall; ownership, target, route, process, path, and lifecycle checks may still reject a specific
call.

Managed deployments add an outer installation boundary. A public hostname first resolves through
the trusted installation directory; public callers cannot choose the installation ID used to address
Kernel, Process, Conversation, adapter, R2, or ripgit state.

## External Identities

Linking a Telegram, WhatsApp, or Discord actor maps an authenticated provider identity to a local
human. The adapter never gets to supply a trusted local uid. Connecting an adapter account and
linking a person are separate operations.

## Pages In This Section

- [Credentials, Sessions & Sharing Boundaries](credentials-sharing.md)

## For Agents

Before changing access, identify the human owner, run-as account, installation, and exact operation.
Labels, usernames from external providers, and route IDs are not authorization.
