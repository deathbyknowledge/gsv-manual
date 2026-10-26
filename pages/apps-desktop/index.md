# Web And Desktop

[Back to the manual](../../index.md)

The web app and Ship Desktop are two ways to use the same Ship. They share
messages, work, files, connections, integrations, and permissions.

## Choose The App That Fits

Use **the web app** when you want Ship from any signed-in browser. It has five
views: **Chat** for Ship, reply activity and
contextual responsibilities/routines, **Work** for connections and helpers (with
files opened from a connection), **Memory** for personal
knowledge pages, **People** for conversations and contacts on other Ships,
and **Settings** for preferences, standing responsibilities, permissions, instructions,
messengers, MCP servers, Logs, and (for the administrator) sign-in and people.
Chat's **record** button turns a browser microphone recording into a message using
your Ship's transcription provider: send it straight away, or pause to review the words first.

Use **Ship Desktop** when you want a native window, local live dictation, or a guided way to connect the current computer. The desktop app can
still chat when the computer itself is not connected.

## What Stays In Sync

Deliberately sent messages and saved work state are available to other
signed-in clients. A live activity view is an observation of a particular
piece of work; open that work explicitly when you want its reasoning, tool
calls, retries, or errors.

Draft text and transient interface state may remain local to the app where they
were created. Attach a file or send the message before expecting another app to
see it.

## Find Help

Hover over or focus a top-right navigation control for a short explanation. Press **w** outside a text field to open **Work**.

Open **? Help** in the header, or **Help** in the menu on a phone. It introduces what Ship can help with and offers five getting-started topics:

- **Talking to Ship** expands examples inline.
- **Use Ship on WhatsApp** opens the existing Messenger connections in Settings.
- **Memory** opens your knowledge pages.
- **Permissions** opens Settings → Permissions.
- **Privacy and your data** opens [Ship's privacy policy](https://ship.space/privacy).

**Keyboard shortcuts** replaces the Help panel with **Search Chat**, general shortcuts and shortcuts for the current screen, including platform-appropriate modifier labels. Choose **← Help** to return to getting-started guidance.

**Need more help?** includes **Feedback** when feedback is available. It opens the same Feedback form as the header button and preserves any report draft. The section also links to the Ship manual inside Memory, [email support](mailto:hello@humansandmachin.es), and the [Discord community](https://discord.gg/hy9ExJJFvn).

## Send Feedback

If your operator enables it, choose **feedback** in the header to report a bug or
suggest an improvement. Write what happened and press **Send**. A failed send
keeps your draft. Reports include your Ship, account, and app/server versions.
**Include last 20 Ship messages** is off by default. Check it to attach a snapshot
of recent messages, thinking, tool inputs/results and runtime events. Use
**Review** to inspect it before sending; tool results can contain private content.
Uncheck it to remove it. No files or media are fetched. Long activity is visibly shortened, and retries
keep the same selected snapshot. Logs are not attached automatically.

You can also ask Ship to report an issue. In Ship's home (the `gsv` target) it uses:

```bash
feedback < report.txt
```

Use a report file rather than inline text, `printf`, or a heredoc: shell command
text is recorded in Logs.

Share only the details the person asked to report. `feedback --id UUID < report.txt`
keeps the same report identity when retrying. The command returns a receipt once
the operator's inbox accepts the report; unavailable or failed sends return an
error. A receipt does not mean the issue has been fixed.

## Pages In This Section

- [Use the Web and Desktop surfaces](desktop-surfaces-and-apps.md)
- [Use voice](voice-gestures.md)
- [Read images with `img2txt`](image-reading.md)
