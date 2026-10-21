# Connect And Route Messaging

[Messaging, Email, And Connected Services](index.md)

## Connect Versus Link

- **Connect** gives Ship access to the messaging service or bot account.
- **Link** binds an external sender to the Ship owner through a short-lived code.

Keeping these separate prevents an untrusted incoming username or chat ID from choosing a local account.

## Connect For The Owner

When the person asks to connect a messenger, handle the Ship side for them:

1. Run `messenger list` on `gsv` to see which messengers are enabled.
2. Run `messenger setup ADAPTER` and share its link or bot name and instructions for getting a code. Use the returned information rather than inventing a number or URL.
3. Ask the person to paste their code back into this conversation. Write it to a temporary file, then run `messenger connect ADAPTER < /tmp/messenger-code.txt`. Read the code from the file so it stays out of logged shell command text, and delete the file afterwards.
4. Report success only after the command returns `paired: true`. Ask them to send a new message in the messenger to start chatting there. If the code expired, get a new one.

`messenger inspect ADAPTER < code.txt` can check the external identity without changing its link. Redemption links the process's human owner; neither a code nor an argument can select another account or Ship. Redeeming a code for an already-linked identity moves it to this Ship. Only redeem a code the person supplies to connect their own account.

No Settings visit is needed for messaging. Password recovery through that messenger requires a direct confirmation in Settings; a process-created link does not authorize password resets. The manual Settings flows below remain available, and disconnect is still a signed-in human action. On older gateways without `messenger`, use those flows.

## Telegram

Message the operator's bot with `/link` to receive a short-lived code. Paste it back to Ship, or enter it in **Settings → Messengers → Telegram**, inspect the identity, and confirm.

The message used to create the link may be consumed by setup. Send another message after confirmation to begin the conversation.

## Slack

Install the operator's Slack app using the setup link, then send `link` in a direct message to it. Paste the code back to Ship, or redeem it in **Settings → Messengers → Slack**. Direct messages to the app reach Ship; channels and threads keep explicit routes. Files shared in Slack become Ship files tied to exact revisions, and Ship can share files back into the conversation.

## WhatsApp

When the operator offers WhatsApp Business, open the setup link and send `/link` to get instructions followed by a code-only message you can copy. The code expires in 10 minutes. Paste it back to Ship, or enter it in **Settings → Messengers → WhatsApp**, inspect the name and masked number, and confirm while signed in. Send another message after linking to reach Ship. The operator owns the Meta credentials; people do not supply their own tokens.

This connection supports direct messages to that number, including media and approval buttons. Ship’s prose paragraphs arrive as separate messages; headings stay with the following block and lists, quotations, tables and code stay together. It does not expose a person's WhatsApp account or group conversations. Availability depends on the operator's Meta account and regional eligibility. WhatsApp is not offered to numbers in Brazil (+55) or Indonesia (+62): Meta restricts business numbers outside those countries from messaging people there, so the pairing code cannot be delivered. When the person may be in one of those countries, say so before they try, and offer Telegram, Discord, Slack, email, or the Ship app instead.

Free-form replies require a message from the person within the last 24 hours. Outside that window, a configured Meta-approved template carries the message or a shortened preview. The full message stays in the Ship conversation; the person can open Ship or reply in WhatsApp to ask Ship about it. **Show me** is an ordinary user reply, not a command to replay queued messages. There is no adapter backlog. Approval notifications direct the person to Ship. Attachments cannot use the text template; use another authorized destination or wait for a reply. Without a configured template, out-of-window delivery fails explicitly.

## Discord

Add the operator's bot using the setup link, then send `pair` in a direct message to it. Paste the code back to Ship, or inspect and confirm it in **Settings → Messengers → Discord**. Send another message after linking to reach Ship.

## Ship And Direct Work Sessions

An ordinary linked private message goes to Ship. In a messenger chat:

- `/where` reports the current selection.
- `/ship` returns future messages to Ship immediately.

Ship can offer a direct line to an owned work item from the active private conversation. The messenger labels that selection as a Work Session. It affects future input on that chat; it does not replace Ship elsewhere or redirect a reply that was already being generated.

From Ship, inspect or change an authorized route with:

```bash
message route show --to here --json
message route set --process PID_OR_LABEL --to here --json
message route clear --to here --json
```

Groups, channels, and threads keep explicit routes. Choose their Ship destination or label from the destination list.

## Attachments And Voice

Incoming images, voice messages, video, and documents become files tied to exact revisions. Transcription may accompany audio, but the original audio remains available.

Outgoing attachments are resolved only when they are sent. The Send tool attaches files staged for the reply; from Shell:

```bash
message send --to DESTINATION --message "Here it is" --attach /path/to/file --also
```

This works on every messaging path when the selected adapter supports that media type. Attaching a document from a connected computer needs that computer's daemon to be current; older daemons can attach only images.

## Delivery And Retries

Ship gives each logical inbound and outbound delivery a stable identity. Each destination receives exactly one correlated send request; Ship owns the durable retry, and the adapter owns provider presentation and idempotency. When provider acceptance is uncertain, the delivery remains ambiguous under the same identity for status checks or a safe retry. Inspect one with `message delivery show <delivery-id>`.

Ship remembers where the person last sent a message, including across follow-ups and background work. Opening, typing in, clicking or scrolling another window does not redirect replies. Activity in the selected web or desktop client keeps it active; if it closes or is inactive for five minutes, replies and new Ship approval notifications use the last authorized linked private messenger. Sending a new message in the app selects that client again. Work Sessions, groups and explicitly addressed messages keep their own routes.

All signed-in clients share Ship's committed history. Only the selected destination notifies, and a retry keeps the destination chosen for that message. Messenger delivery still obeys the provider's rules, including WhatsApp's reply window.

## Approvals In Messaging

An approval applies only to its exact request token and authorized sender. Bare approval text, stale tokens, and answers from another surface leave the operation unauthorized.
