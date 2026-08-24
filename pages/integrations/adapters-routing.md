# Connect And Route Messaging

[Messaging, Email, And Connected Services](index.md)

## Connect Versus Link

- **Connect** gives GSV access to the messaging service or bot account.
- **Link** proves that a particular external sender is the signed-in GSV owner.

Keeping these separate prevents an untrusted incoming username or chat ID from choosing a local account.

## Telegram

The exact setup depends on the installation:

- With managed Telegram, message the platform bot. It returns a short-lived one-time code. Enter that code while signed in to GSV, inspect the Telegram identity shown, and confirm the link.
- With a standalone bot, connect the BotFather token through the Telegram settings first, message that bot, then redeem its link challenge while signed in.

The message used to create the link may be consumed by setup. Send another message after confirmation to begin the conversation.

## WhatsApp

First pair the GSV WhatsApp account as a linked device through the Messengers setup. Then message it from the person's own WhatsApp account and confirm the separate identity-link challenge inside GSV.

Pairing the device and linking the human sender are different operations.

## Discord

Connect a bot with the permissions required by the intended direct messages, servers, channels, and message content. Then link or route the desired surface through GSV. Owner identity is established by the authenticated link challenge.

## Home And Direct Work Sessions

An ordinary linked private message goes to Home. In a messenger chat:

- `/where` reports the current selection.
- `/home` returns future messages to Home immediately.

GSV can offer a direct line to an owned work item from the active private conversation. The messenger labels that selection as a Work Session. It affects future input on that chat; it does not replace Home elsewhere or redirect a reply that was already being generated.

From GSV, inspect or change an authorized route with:

```bash
message route show --to here --json
message route set --process PID_OR_LABEL --to here --json
message route clear --to here --json
```

Groups, channels, and threads keep explicit routes. Choose their GSV destination or label from the destination list.

## Attachments And Voice

Incoming images, voice messages, video, and documents become files tied to exact revisions. Transcription may accompany audio, but the original audio remains available.

Outgoing attachments are resolved only when they are sent:

```bash
message send --to DESTINATION --message "Here it is" --attach /path/to/file --also
```

This works for managed and standalone messaging paths when the selected adapter supports that media type.

## Delivery And Retries

GSV gives each logical inbound and outbound delivery a stable identity. Provider retries reuse that identity. When provider acceptance is uncertain, the delivery remains ambiguous under the same identity for status checks or a safe retry.

For a direct reply, the endpoint that started the interaction wins. Background Home events may use the most recently authorized linked private destination.

## Approvals In Messaging

An approval applies only to its exact request token and authorized sender. Bare approval text, stale tokens, and answers from another surface leave the operation unauthorized.
