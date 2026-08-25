# Connect With Another GSV

[Messaging, Email, And Connected Services](index.md)

A Contact joins your Ship to a person on another GSV. You can exchange
messages, coordinate requests, and share exact file revisions without putting
either person's conversations, files, work, or permissions under the other's
control.

Contacts work between standalone and managed GSVs. The other person's
installation does not need to use the same host or deployment model.

## Pair With Someone

One person creates a short-lived invitation in the Contacts page. Send the
complete invitation code to the intended person through a channel you trust.
They open their own Contacts page and accept the code. Share it through a
trusted channel so both people know which Ships they are pairing.

From Shell, the same flow is:

```bash
contact invite create --expires 30m
contact invite accept 'gsv-contact-v1:...'
contact list
```

An invitation can be accepted once and expires automatically. Treat an unused
code as a temporary secret: do not post it publicly or place it in a long-lived
document.

Pairing creates one local Contact conversation on each side. It does not reveal
local account ids, Process ids, paths, credentials, or other conversations.

## Send A Message

Open the conversation from the Contacts page, or copy its contact id and send
from Shell:

```bash
message send --to 'contact:...' --message "Can you review this?" --also
```

`message destinations` includes active Contacts as well as messaging endpoints.
The sender first records the message locally. Delivery is complete when the
other GSV has durably recorded it; that does not mean the other person or their
Ship has already acted on it.

An incoming Contact message creates a responsibility for Ship. Use
`r12y show ID` to inspect its exact untrusted text and resource references
before replying or resolving it.

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

contact request list
contact request update 'request:...' --state accepted --revision 1
contact request update 'request:...' --state active --revision 2
contact request update 'request:...' --state completed --revision 3
```

Useful terminal states are `completed`, `rejected`, and `cancelled`. Include
`--all` when listing requests to see terminal records. If an expected revision
is stale, inspect the current record before deciding what should happen next.

The Contacts page exposes the common accept, reject, cancel, start, and complete
actions without requiring Shell.

## Revoke A Contact

Use the Contacts page or:

```bash
contact revoke 'contact:...'
```

Revocation stops new messages, request updates, and file reads through that
relationship. It does not erase messages that each person already received.
The other GSV records the relationship as revoked when it receives the durable
notice.

If a relationship should exist again later, create and accept a new invitation.
The new relationship does not reactivate old file grants or delayed deliveries.

## Inspect Or Recover

```bash
contact identity
contact list --all --json
contact request list --all --json
message destinations --all --json
```

If a delivery is queued, GSV keeps retrying the same logical delivery. A
terminal failure becomes work for Ship to inspect instead of silently creating
duplicates. If pairing fails, verify that the invitation is unexpired and that
the other GSV's origin is reachable over HTTPS.
