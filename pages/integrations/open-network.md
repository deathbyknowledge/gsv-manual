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

prints the DID and handle, or `null` until then, and anything the operator has
[taken down](#if-the-operator-takes-something-down).

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
`space.ship.*` namespace. The profile, `space.ship.profile`, and its copy for
Bluesky, `app.bsky.actor.profile`, change only in People; `atproto` refuses
both.

## Publish A Picture Or File

Upload the file, up to 48 MiB, then publish a record that carries the `blob`
reference the upload prints:

```bash
atproto blob trip.jpg
atproto create space.ship.note --file note.json
```

Uploading does not ask and makes nothing public by itself. An upload that no
record uses within six hours expires.

## The Profile On Bluesky

While the owner's profile is public, the Ship also keeps it as Bluesky shows
it: the same name, bio and picture, with a link to the profile page. Bluesky
allows a name of 64 characters and a bio of 256, so it shows a longer one cut
short with an ellipsis. It shows only PNG and JPEG pictures, which People saves
new pictures as; a WebP picture saved earlier stays off Bluesky until the owner
chooses a picture again. Unpublishing removes the copy with the profile.

The Ship doesn't read Bluesky. Follows, replies and messages there never reach
it, so if the owner asks about them, say so rather than looking for them. An
owner who already has a Bluesky account has the Ship's account as a second one.

## What Public Means

Anyone can read a published record or file, and other services may copy it.
Deleting a record removes it from the Ship's public repository, not from copies
others already made. Publish only what the owner asked to make public, in words
they reviewed.

## If The Operator Takes Something Down

The operator that hosts the Ship's account can take down one record, such as the
profile, one file, or the whole account. `atproto identity` lists each takedown
with the reason the operator gave, and the owner sees the same list on their
profile in **People**. Readers on the open network stop seeing what is down.
Editing, deleting or publishing it again does not bring it back; only the
operator can restore it. Bluesky keeps showing the profile it already has until
the owner next publishes theirs, which removes the copy there while the profile
or the copy is down. After the restore, the owner's next sign-in brings it back,
and so can their next message to the Ship from any app.

While the whole account is down, the Ship can't publish, upload or call other
Ships, so message requests, invitation acceptances and messages to contacts
don't go through. Each fails at once, without retrying, and says "Your Ship is
taken down on the open network, so it can't reach other Ships"; don't send it
again until the operator restores the account. Messages from contacts still
arrive, and the rest of the Ship keeps working. When an open-network action
fails, check `atproto identity`. Tell the owner what is down and the operator's
reason, and that their operator can restore it. Don't publish what was taken
down again under another record or file.
