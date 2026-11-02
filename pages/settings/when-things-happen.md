# When Things Happen

[Settings And Recovery](index.md)

**Settings → When things happen** is one list of the things that can happen on your Ship. Each row has two choices, and a change saves at once.

- **Tell me** sends a short message to your messenger chat with Ship.
- **Ship** is what your Ship does about it: **Off**, **Sees it** or **Acts**. **Sees it** adds the event to Ship's history, without starting any work. **Acts** starts Ship working on it.

A row warns you when nobody will hear about that event.

## What Happens Unless You Change It

| What happens | Tell me | Ship |
| --- | --- | --- |
| Someone asks to message you | On | Sees it |
| A contact messages you | On | Sees it |
| Someone accepts your invitation | On | Sees it |
| Mail arrives | Off | Acts |
| A new computer connects | Off | Acts |
| A messenger connects | Off | Acts |
| A messenger needs signing in again | Off | Acts |

The first three rows offer only **Off** and **Sees it**. Another person's words never start Ship working by a setting. To have Ship handle a contact, turn that on for the contact in [People](../integrations/contacts.md).

**Acts** on the last four rows is the same setting as that event's standing responsibility, so turning it off from the shell shows here too. **Review conversations for memory** is a separate switch below the list. Replying to you, delegated work and your routines are always on.

## What You Receive

Messages use your language setting and carry a short line, for example:

- `💬 Ada: are we still on for tomorrow?`
- `📬 Message request from Ada. Read it and decide in People.`
- `📧 You have 3 new emails.`
- `💻 A new computer connected to your Ship: Studio.`
- `⚠️ WhatsApp needs signing in again.`

An email's sender and words stay out of your messenger, so read them in Ship. Repeated messages from one contact, and repeated emails, collapse into a count. Outside WhatsApp's 24-hour window, the line arrives inside the [message template](../integrations/adapters-routing.md).

You get these only when you have a messenger linked and aren't active in a browser or on Desktop. A contact's event you weren't told about because you were active or couldn't be reached stays out of Ship too. It reaches Ship unsent only if you turned **Tell me** off for that row and left Ship on **Sees it**.

## Your Own Sources

A source is somewhere your own events come from: a script, a routine, another service. Each one gets its own row in this list. Add them in **Work**, under **Your sources**, or ask Ship to. Open one there to pause it, change its secret, delete it or read what arrived. A new source tells you and leaves Ship **Off**.

- **From a routine or script on your Ship:** `event source add backups`, then `event emit backups --title "Nightly backup failed"`.
- **From any computer:** add a source called `backups`, then run `gsv event emit backups --title "Nightly backup failed"`. It doesn't need a public address.
- **From another service:** choose how it signs its webhooks when adding the source: GitHub, Stripe, Shopify and Linear are listed by name, **Signed webhook (Standard Webhooks)** covers services such as Svix and Resend, and **Other signed webhook (HMAC)** takes the header and encoding from the service's documentation. You get an address and, unless the service issues its own, a signing secret, shown once. **New secret** replaces it, and the old one keeps working for 24 hours. When the service issues the secret, as Stripe, Shopify and Linear do, the source shows **needs its secret** and refuses deliveries until you paste it into **Signing secret the sender gave you**.
- **From a sender that can't sign:** choose a secret address. Anyone holding that address can send events, and request logs on the way may record it, so Ship can't be set to **Acts** on these.

Give an event a stable `--id` and repeats are ignored, so a script can re-read the same items without remembering them. `event list` shows what arrived. `event source add NAME --expect-every 1d` tells you once if a source goes quiet for that long.

Messages look like this. While you're active in a browser or on Desktop, or if you have no messenger linked, an event appears as a card in your Ship conversation instead. A source going quiet still goes to your messenger, so you don't miss it:

- `🔔 Backups: Nightly backup failed`
- `🔔 Backups: 3 new. Latest: Nightly backup failed`
- `🔕 Backups has gone quiet: nothing arrived when it should have.`

Whatever an event says is untrusted, wherever it came from. An event from a running process never starts Ship working. Ship needs your approval to set one of your sources to **Acts**.

## When Ship Changes A Row

Ship can change these settings too. The row then says **Your Ship changed this.**

If Ship turns off **Tell me** or sets itself to **Acts**, your messenger is told, whatever your settings say and even while you're active. Without a linked messenger, the note on the row is the record.
