# Publish On The Open Network

[Messaging, Email, And Connected Services](index.md)

The open network is the AT Protocol network that Bluesky and other apps read.
A Ship publishes there only what its owner chooses to make public: the profile,
and records or files the owner asks Ship to publish. Messages, contacts, memory
and the rest of the Ship never go there.

Each Ship has an account on the open network: a DID whose handle is the Ship's
address, such as `alice.ship.space`. The Ship's first publish, invitation or
message request creates it.

```bash
atproto identity
```

prints the DID and handle, or `null` until then.

## Publish A Record

Only the owner and Ship may publish; helpers are refused. Nothing publishes while
the owner's profile is private, so ask them to publish it in **People** first.
Each of Ship's writes asks the owner for approval unless an `atproto.write`
[approval rule](../settings/ai-voice-approvals.md) allows or blocks it. The
approval shows the handle and address it publishes as, every change, and the
files its records carry. Report a publish as done only once the command succeeds.

```bash
atproto create space.ship.note --json '{"text":"Back from the trip"}'
atproto put space.ship.note RKEY --file note.json
atproto delete space.ship.note RKEY
```

A record's `$type` defaults to its collection. `atproto apply --file writes.json`
commits up to ten changes together. Ship's own record types use the
`space.ship.*` namespace. The profile, `space.ship.profile`, changes only in
People.

## Publish A Picture Or File

Upload the file, up to 48 MiB, then publish a record that carries the `blob`
reference the upload prints:

```bash
atproto blob trip.jpg
atproto create space.ship.note --file note.json
```

Uploading does not ask and makes nothing public by itself. An upload that no
record uses within six hours expires.

## What Public Means

Anyone can read a published record or file, and other services may copy it.
Deleting a record removes it from the Ship's public repository, not from copies
others already made. Publish only what the owner asked to make public, in words
they reviewed.
