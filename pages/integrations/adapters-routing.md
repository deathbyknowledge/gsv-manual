# Connect And Route Messaging

[Messaging, Email, And Connected Services](index.md)

## Connect Versus Link

- **Connect** gives Ship access to the messaging service or bot account.
- **Link** binds an external sender to the Ship owner through a one-time link or a short-lived code.

Keeping these separate prevents an untrusted incoming username or chat ID from choosing a local account.

## Connect For The Owner

When the person asks to connect a messenger, handle the Ship side for them:

1. Run `messenger list` on `gsv` to see which messengers are enabled.
2. Run `messenger setup ADAPTER`. Use the returned information rather than inventing a number or URL.
3. When it returns `pairingLinks: true`, as WhatsApp and Telegram do, send the person its `setupUrl`. That page in Settings makes a one-time link while they are signed in; they send one message from it, and the page names the account that connected. There is no code for you to collect, and none reaches you. If they ask whether it worked, check `messenger list`.
4. Otherwise, share its link or bot name and instructions for getting a code, and ask the person to paste the code back into this conversation. Write it to a temporary file, then run `messenger connect ADAPTER < /tmp/messenger-code.txt`. Read the code from the file so it stays out of logged shell command text, and delete the file afterwards. Report success only after the command returns `paired: true`. If the code expired, get a new one.
5. Ask them to send a new message in the messenger to start chatting there.

`messenger inspect ADAPTER < code.txt` can check the external account without changing its connection. Redemption connects it to Ship's human owner; neither a code nor an argument can select another account or Ship. Redeeming a code for an already-connected account moves it to this Ship. Only redeem a code the person supplies to connect their own account. Messengers that connect from links refuse `inspect` and `connect`.

A messenger connected from a link was connected by the signed-in person, so it also works for password recovery. For a code you redeem, no Settings visit is needed for messaging, but password recovery through that messenger requires a direct confirmation in Settings; a messenger that Ship or a helper connected does not authorize password resets. The Settings flows below remain available, and disconnect is still a signed-in human action. On older releases without `messenger`, use those flows.

## Telegram

Open **Settings → Messengers → Telegram**, or the `setupUrl` from `messenger setup telegram`. **Open Telegram** opens the operator's bot with a one-time code; tapping **Start** sends it. The code works once, for 10 minutes, and only for the Ship that made it. On a computer, the page also shows a QR code to scan with a phone's camera and the code to send by hand. The page then names the Telegram account that connected; **Disconnect** removes a wrong one.

If that Telegram account already talks to another Ship, the bot asks whether to **Move it** to this Ship or **Keep it**. A message to the bot without a connection gets a reminder to connect from Settings. The message used to connect is consumed while connecting. Send another message after connecting to begin the conversation.

## Slack

Install the operator's Slack app using the connect link, then send `link` in a direct message to it. Paste the code back to Ship, or redeem it in **Settings → Messengers → Slack**. Direct messages to the app reach Ship; channels and threads keep explicit routes. Files shared in Slack become Ship files tied to exact revisions, and Ship can share files back into the conversation.

## WhatsApp

When the operator offers WhatsApp Business, open **Settings → Messengers → WhatsApp**, or the `setupUrl` from `messenger setup whatsapp`. **Open WhatsApp** opens a chat with the Ship number with "Connect my Ship" and a one-time code filled in; sending it connects that WhatsApp account. The code works once, for 10 minutes, and only for the Ship that made it. On a computer, the page also shows a QR code to scan with a phone's camera and the code to send by hand. The page then names the profile and masked number, or the username, that connected; **Disconnect** removes a wrong one. A number that already talks to another Ship is asked whether to **Move it** or **Keep it**, and a number without a connection gets a reminder to connect from Settings. Send another message after connecting to reach Ship. The operator owns the Meta credentials; people do not supply their own tokens.

This messenger supports direct messages to that number, including media and approval buttons. Ship’s prose paragraphs arrive as separate messages; headings stay with the following block and lists, quotations, tables and code stay together. It does not expose a person's WhatsApp account or group conversations. Availability depends on the operator's Meta account and regional eligibility.

Free-form replies require a message from the person within the last 24 hours. Outside that window, a configured Meta-approved template carries the message or a shortened preview. The full message stays in the Ship conversation; the person can open Ship or reply in WhatsApp to ask Ship about it. **Show me** is an ordinary user reply, not a command to replay queued messages. There is no messenger backlog. Approval notifications direct the person to Ship. Attachments cannot use the text template; use another authorized destination or wait for a reply. Without a configured template, out-of-window delivery fails explicitly.

## Discord

Add the operator's bot using the connect link, then send `pair` in a direct message to it. Paste the code back to Ship, or inspect and confirm it in **Settings → Messengers → Discord**. Send another message after connecting to reach Ship.

## Ship And Helpers

An ordinary private message from a connected messenger goes to Ship. In a messenger chat:

- `/where` reports the current selection.
- `/ship` returns future messages to Ship immediately.

Ship can offer a direct line to one of its helpers from the active private conversation. The messenger labels that selection as a helper. It affects future input on that chat; it does not replace Ship elsewhere or redirect a reply that was already being generated.

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

This works on every messaging path when the selected messenger supports that media type. Attaching a document from a connected computer needs that computer's daemon to be current; older daemons can attach only images.

## Choices

A message that asks something can offer [choices](../agents-assistants/conversations-delegation.md#what-becomes-a-message), and each surface shows them its own way:

| Surface | Choices appear as |
| --- | --- |
| Ship app | Buttons under Ship's latest message, until anyone writes again. |
| WhatsApp | Up to three of at most 20 characters: reply buttons. Up to ten of at most 24: a list behind **Choose one**. Longer choices, choices beside an attachment or a link button, and messages outside the 24-hour window: a numbered list. |
| Telegram | A reply keyboard in place of the person's keyboard, until Ship's next text message removes it. Beside an attachment or a link button: a numbered list. |
| Discord and Slack | A numbered list under the message. |

A tap arrives as an ordinary message with the choice's text. Under a numbered list the person may answer with the number, so read a reply such as "2" against the choices offered. Choices of a few words fit WhatsApp's buttons. WhatsApp cannot withdraw buttons, so a tap on an earlier message's button can still arrive later, as a reply to the question it answers.

## Delivery And Retries

Ship gives each logical inbound and outbound delivery a stable identity. Each destination receives exactly one correlated send request; Ship owns the durable retry, and the messenger owns provider presentation and idempotency. When provider acceptance is uncertain, the delivery remains ambiguous under the same identity for status checks or a safe retry. Inspect one with `message delivery show <delivery-id>`.

Ship remembers where the person last sent a message, including across follow-ups and background work. Opening, typing in, clicking or scrolling another window does not redirect replies. Activity in the selected web or desktop client keeps it active; if it closes or is inactive for five minutes, replies and new Ship approval notifications use the last authorized connected private messenger. Sending a new message in the app selects that client again. Helpers, groups and explicitly addressed messages keep their own routes.

All signed-in clients share Ship's committed history. Only the selected destination notifies, and a retry keeps the destination chosen for that message. Messenger delivery still obeys the provider's rules, including WhatsApp's reply window.

## Approvals In Messaging

An approval applies only to its exact request token and authorized sender. Bare approval text, stale tokens, and answers from another surface leave the operation unauthorized.
