# Connect With Another GSV

[Messaging, Email, And Connected Services](index.md)

A Contact joins your Ship to a person on another GSV. You can exchange
messages, coordinate requests, and share exact file revisions without putting
either person's conversations, files, work, or permissions under the other's
control.

Contacts work between spaces served by the same or different operators. The
other person's space does not need to share your account system.

## Pair With Someone

Open **People** (`p`) and choose **connect → create invitation link**. Share the
link with the intended person wherever you already talk. They open it, choose
their space or enter its address, sign in if necessary, and accept. An address
also works across operators or when someone else owns their space. Neither person
needs a public profile. People invitations last seven days and connect one person. Acceptance
opens the conversation on each side when the invitation is open.

**connect → I have an invitation** also accepts a link or an older contact code.
The syscall and Shell accept both formats; `contact invite create` returns the
link alongside the code. Its default lifetime is one hour unless requested
otherwise. These contact invitations are separate from invites to create a
space or add a local account.

For someone with a public profile, use **connect → use a profile address** and
send a first message. Your account's display name is prefilled and editable.
Their **Requests** list lets them review, accept or privately decline it.
Acceptance opens the conversation and retains that first message. Publishing
your own profile is optional and belongs in **Settings → Profile**.

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

Connecting does not start Ship. By default the person receives contact messages
in People. **Ship replies**, beside the contact's name, authorizes Ship to handle
new incoming messages; enabling it does not replay the existing conversation.
Turning it off ends that standing assignment. Human and Ship authorship remain
visible in messages.

For a particular task, **ask Ship** opens an editable draft in the person's
ordinary Ship chat. They review and send it. First-use examples can prefill a
request to make plans, plan a trip or coordinate work with the selected contact.
Ship can read the contact history before acting:

```bash
message history --with 'contact:...' --limit 50
```

When contacting someone for existing Ship work, bind the message to its open
responsibility so their reply continues that task:

```bash
message send --to 'contact:...' --message "Which evenings work for you?" \
  --responsibility 'r12y:...' --also
```

This does not turn on permanent handling. A reply to that message resumes its
responsibility; an unthreaded reply does so only when one active responsibility
awaits that contact. Resolving or cancelling the work ends the association.
The other person chooses how their side is handled independently.

The People indicator and the strip above the Ship prompt show unread contact
conversations and incoming requests, including after reload or reconnect. Live
messages can also be expanded and answered inline in the Ship chat. Reading in
People clears the private unread state; it sends no read receipt to the peer.
Muted, blocked, archived and ended conversations stay quiet.

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

**People → conversation → details → Work requests** exposes the common accept,
reject, cancel, start, and complete actions without requiring Shell.

## Revoke A Contact

Use the conversation's details in People or:

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
contact invite list --all --json
contact list --all --json
contact request list --all --json
message destinations --all --json
message history --with 'contact:...' --json
message delivery show 'delivery:...' --json
```

If a delivery is queued, GSV keeps retrying the same logical delivery. A
terminal failure becomes work for Ship to inspect instead of silently creating
duplicates. If pairing fails, verify that the invitation is unexpired and that
the other GSV's origin is reachable over HTTPS.
