# Connect With Another GSV

[Messaging, Email, And Connected Services](index.md)

A Contact joins your Ship to a person on another GSV. You can exchange
messages, coordinate requests, and share exact file revisions without putting
either person's conversations, files, work, or permissions under the other's
control.

Contacts work between spaces run by the same or different operators.

## People And First Messages

Open **People** with `p`. Inbox holds conversations, Requests holds first messages
from new people, and Contacts is the private address book. Read position, archive,
aliases and mute stay private to your space. New messages bring an archived
conversation back unless muted; mute also suppresses tab attention.

**New conversation** accepts a public profile address. Review the person, choose
the display name they will see, and send a first message. Once accepted, that
message stays in the same conversation and both sides can send more messages and
attachments. Declining does not notify the sender. First-message requests expire
after 30 days.

Public profiles start private. A signed-in person can save and publish theirs in
**Settings → Profile**. Saving edits does not update a published page until they
publish again. Unpublishing removes the page but leaves existing conversations
intact. Ship may resolve a public profile; publishing and first-message decisions
belong to the signed-in person.

## Pair With Someone

One person chooses **new conversation → use a private invitation** in People. Send the
complete invitation code to the intended person through a channel you trust.
They open the same invitation flow in their space and accept the code. Share it through a
trusted channel so both people know which Ships they are pairing.

You can ask Ship to do the same setup in natural language. Ship may create,
accept, cancel, or revoke trust for its owner; delegated work processes cannot
change Contact trust.

From Shell, the same flow is:

```bash
contact invite create --expires 30m
contact invite accept 'gsv-contact-v1:...'
contact invite list
contact invite cancel 'invite:...'
contact list
```

An invitation can be accepted once and expires automatically. Treat an unused
code as a temporary secret: do not post it publicly or place it in a long-lived
document. Invitation listings contain only lifecycle metadata, never the
recoverable invitation code. Use `contact invite list --all` to inspect recently
accepted, expired, or cancelled invitations.

Pairing creates one local Contact conversation on each side. It does not reveal
local account ids, Process ids, paths, credentials, or other conversations.

## Send A Message

Open the conversation from People, or copy its contact id and send
from Shell:

```bash
message send --to 'contact:...' --message "Can you review this?" --also
```

`message destinations` includes active Contacts as well as messaging endpoints.
The sender first records the message locally. Delivery is complete when the
other GSV has durably recorded it; that does not mean the other person or their
Ship has already acted on it.

The send result says `accepted=true` once this GSV durably owns the delivery.
Keep its delivery id and inspect the eventual result when needed:

```bash
message delivery show 'delivery:...'
```

Pairing, accepting a first message and receiving an ordinary message do not start
Ship. The person handles the conversation until they enable **Let Ship handle
this** in Details. That handoff uses one ordinary responsibility and Ship's usual
permissions and approval rules. Disable the same control to take it back. Messages
show whether the person or their Ship wrote them.

When contacting someone for an existing task, bind the outgoing message to that
Ship responsibility instead of enabling permanent conversation handling:

```bash
message send --to 'contact:...' --responsibility 'r12y:...' \
  --message "Does Friday morning work?" --also
```

Human and Ship replies can continue this responsibility. An exact reply reference
selects the task; an unthreaded reply continues only one unambiguous active task
awaiting that contact. Resolved or cancelled work stops receiving continuations.
Delivery acknowledgements and duplicate messages never create more work. The
other person independently decides whether their Ship handles their side.

Use `r12y show ID` and Contact history for the exact message before acting:

```bash
message history --with 'contact:...' --limit 50
message search 'Friday morning' --with 'contact:...'
```

Reusing the same delivery id safely reconciles an uncertain attempt:

```bash
message send --to 'contact:...' \
  --message "Can you review this?" \
  --delivery-id 'stable-id-for-this-message' \
  --also
```

Use a new delivery id for a genuinely new message. GSV rejects changed content
under an id that already names another logical delivery.

## Share A File Or Image

Attach a GSV file in the ordinary way:

```bash
message send --to 'contact:...' \
  --message "Here is the exact build I tested." \
  --attach /home/alice/releases/app.zip \
  --also
```

The conversation stores a reference to the retained revision, not another
eager copy of its bytes. The other GSV streams that exact revision when the
recipient opens or uses it. A later edit to the original file does not rewrite
the earlier message.

Copy from a connected computer to GSV first when the source is not already
available as an immutable GSV reference:

```bash
cp laptop:/Users/alice/Desktop/report.pdf /tmp/report.pdf
message send --to 'contact:...' --message "Report" --attach /tmp/report.pdf --also
```

## Coordinate A Request

A request is useful when both Ships need a shared state rather than only a
message. It has a kind, title, optional structured details, and a revisioned
lifecycle.

```bash
contact request create \
  --contact 'contact:...' \
  --kind review \
  --title "Review the release candidate" \
  --details '{"version":"0.5.0"}'
```

The requester can cancel an unaccepted offer. On the other GSV, the performer
accepts or rejects it, then starts, completes or stops accepted work:

```bash
contact request list
contact request update 'request:...' --state accepted --revision 1
contact request update 'request:...' --state active --revision 2
contact request update 'request:...' --state completed --revision 3
```

Wait for `EXCHANGE` to become `acknowledged` before the next local update.
The work state is recorded locally first; `pending` means the other GSV has not
confirmed it yet. `failed` leaves the exchange unsettled, even when its work
state says `completed`. Older records may say `unconfirmed` when no confirmation
was retained. Check the current record rather than assuming a remote outcome.

Useful terminal states are `completed`, `rejected`, and `cancelled`. Include
`--all` when listing requests to see terminal records. If an expected revision
is stale, inspect the current record before deciding what should happen next.

The conversation's Requests tab exposes the common accept, reject, cancel, start, and complete
actions without requiring Shell.

## Revoke A Contact

Use conversation Details or:

```bash
contact revoke 'contact:...'
```

Revocation stops new messages, request updates, and file reads through that
relationship. It does not erase messages that each person already received.
The other GSV records the relationship as revoked when it receives the durable
notice.

If a relationship should exist again later, create and accept a new invitation.
The new relationship does not reactivate old file grants or delayed deliveries.

**Block** also refuses new requests from that remote identity. It is available in
conversation Details and first-message request controls. **Unblock** allows a new
connection; it does not restore an old one. Muting or removing someone from the
saved address book keeps the conversation and does not cancel Ship's work.
**Blocked people** keeps the list available after old requests are cleaned up.

## Inspect Or Recover

```bash
contact identity
contact invite list --all --json
contact list --all --json
contact request list --all --json
message destinations --all --json
message history --with 'contact:...' --json
message delivery show 'delivery:...' --json
```

If a delivery is queued, GSV keeps retrying the same logical delivery. Failures
of messages sent by Ship become work for Ship to inspect. A signed-in person or
their Ship can resume a recoverable failure through `contact.delivery.retry`,
using the delivery ID and `updatedAtMs` from `contact.delivery.get`. This retries
the exact stored message; it does not create a new message. A permanent refusal,
revoked relationship or delivery older than seven days cannot be retried.

If pairing fails, verify that the invitation is unexpired and that the other
GSV's origin is reachable over public HTTPS.
