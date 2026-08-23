# Credentials, Sessions & Sharing Boundaries

[Accounts & Access](index.md)

## Credential Types

- A human password or session authenticates an interactive user.
- A user token supports non-interactive client access with that user's bounded authority.
- A machine credential is driver-bound and stored in local host configuration.
- Adapter provider credentials belong to their adapter boundary.
- Managed platform credentials belong to the managed service Worker and are never copied into an
  installation's ordinary configuration.

Raw secrets may be displayed only at their deliberate creation or provider boundary. Never log them,
put them in prompts, paste them into Messages, or store them in ordinary knowledge files.

## Sessions And Client Caches

Web and Desktop sessions are separate from machine and adapter connections. Signing out removes the
user session but does not silently revoke a machine. UI query caches are session-scoped and replaced
on lock, logout, or account change so one user's fresh data cannot appear in another session.

## Linking External Actors

An adapter first proves the provider event and normalizes its actor. The Kernel then resolves an owned
identity link. A link code is short-lived and one-time; confirmation occurs inside an authenticated
GSV session so the code itself cannot select a local user or installation.

Managed Telegram uses the platform bot and this pairing flow. Standalone Telegram uses a user-owned
bot credential. WhatsApp pairing connects the adapter account first, then a separate direct-message
challenge links the human sender.

## Sharing

Current product behavior is primarily one owner per installation. Do not simulate multi-user sharing
by handing out the owner's password, copying a bearer token, or mapping unrelated external actors to
the owner. Proper N-human/M-Process Conversations require explicit membership, sender identity, and
per-message authorization and remain future product work.

## Recovery

Prefer normal logout/revocation, adapter disconnect, machine revoke, and setup flows. A complete
self-service forgotten-password reset is not currently shipped. Operators should follow a documented
installation recovery procedure rather than editing password records ad hoc.

## For Agents

Report whether a credential was configured or revoked, never its value. If a workflow requires a
secret in an unsafe channel, stop and direct the user to the owning settings or provider surface.
