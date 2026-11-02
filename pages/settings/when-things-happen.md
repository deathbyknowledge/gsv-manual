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

## When Ship Changes A Row

Ship can change these settings too. The row then says **Your Ship changed this.**

If Ship turns off **Tell me** or sets itself to **Acts**, your messenger is told, whatever your settings say and even while you're active. Without a linked messenger, the note on the row is the record.
