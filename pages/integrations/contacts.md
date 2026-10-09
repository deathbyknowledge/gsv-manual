# Connect With Another GSV

[Messaging, Email, And Connected Services](index.md)

A Contact joins your Ship to a person on another GSV. You can exchange
messages, coordinate requests, and share exact file revisions without putting
either person's conversations, files, work, or permissions under the other's
control.

Contacts work between spaces served by the same or different operators. The
other person's space does not need to share your account system.

## Pair With Someone

Open **People** (`p`), choose **connect**, decide who handles new messages, then
choose **create invitation link**. Share the
link with the intended person wherever you already talk. They open it, choose
their space or enter its address, sign in if necessary, choose who handles their
new messages, and accept. An address
also works across operators or when someone else owns their space. Neither person
needs a public profile. People invitations last seven days and connect one person. Acceptance
opens the conversation on each side when the invitation is open.

**connect → I have an invitation** also accepts a link or an older contact code.
The syscall and Shell accept both formats; `contact invite create` returns the
link alongside the code. Its default lifetime is one hour unless requested
otherwise. These contact invitations are separate from invites to create a
space. Each space has one personal human account.

For someone with a public profile, use **connect → use a profile address** and
send a first message. Your account's display name is prefilled and editable.
Their **Requests** list lets them review, accept or privately decline it.
Both people choose how their own Ship handles new messages before sending or
accepting the request; neither option is preselected.
Acceptance opens the conversation and retains that first message. Publishing
your own profile is optional. Click your display name at the bottom of the
**People** sidebar to edit it. Save and publish are separate: later edits stay
private until you publish them. Your public URL is `https://YOUR-SPACE/profile`;
there is no separate alias to choose. Old published profile links continue to work.
Profile drafts remain when you return to a conversation.

You can ask Ship to create or accept a private invitation in natural language. Ship may create,
accept, cancel, or revoke trust for its owner; delegated work processes cannot
change Contact trust. Ask the owner who should handle new messages unless they
already chose: **manual** leaves them for the person, and **ship** lets Ship read
and respond to future incoming messages. Task-specific replies can still reach
Ship with manual handling. Pass that choice explicitly; each person decides for
their own side. The whole invitation flow works in the current Ship conversation,
including WhatsApp and other private messaging surfaces.
Public-profile message requests currently use People.

Share the returned `url` with the owner. Creating it means the invitation is ready,
not that the other person has connected. They can open it or give it to their own
Ship to accept. Inspect `contact invite list` and `contact list` to confirm
acceptance. Cancel an unused invitation before replacing it.

From Shell, the same flow is:

```bash
contact invite create --handling ship --expires 7d
contact invite accept 'gsv-contact-v1:...' --handling manual
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

People asks each person to choose **I’ll handle them** or **Let Ship handle them**
when connecting. Each choice affects only that person's Ship and survives delayed
acceptance. **Automatically handle new messages**, beside the contact's name,
changes it later. Existing contacts keep their settings. Ship-led invitations
record the owner's explicit choice too. Ship can change it when asked: read
`preferences.revision` from `contact list --json`, then run
`contact handling CONTACT_ID manual|ship --revision N`. If the revision changed,
reread the contact before applying the request.

Connecting or enabling automatic handling does not wake Ship or replay the first
message. The next incoming message starts handling. Turning the setting off ends
that standing assignment; replies tied to a task you gave Ship can still resume
it until it is finished. Human and Ship authorship remain visible in messages.

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

The People indicator and the compact line above the Ship prompt show unread
contact conversations and incoming requests, including after reload or reconnect.
Select a person's name to read and reply in a panel above the prompt. New messages
keep the panel closed and preserve your place in the Ship conversation. Closing
a panel keeps its unfinished reply for this session, marked **draft**. Sending
clears the answered activity; messages arriving during the send still wait.
**Open conversation** shows the full history in People.
Previews distinguish **You** and **Your Ship** from the other person's messages.

Reading in People clears the private unread state; it sends no read receipt to
the peer. Muted, blocked, archived and ended conversations stay quiet, while an
unfinished reply remains reachable.

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
