# Web And Desktop

[Back to the manual](../../index.md)

The Web and Desktop apps are two ways to use the same GSV. They share messages,
work, files, machines, integrations, and permissions.

## Choose The App That Fits

Use **Web** when you want GSV from any signed-in browser. The Web app is
called **Instrument** and has four views: **Zen** for Ship and the activity
behind each reply, **Fleet** for places, processes, contacts,
responsibilities, the ledger, and recent files, **Memory** for personal
knowledge pages, and **Settings** for preferences, permissions, instructions,
messengers, MCP, and (for root) sign-in and people.

Use **Desktop** when you want a native window, local voice and hands-free
control, or a guided way to connect the current computer as a place. Desktop can
still chat when the computer itself is not connected.

## What Stays In Sync

Deliberately sent messages and saved work state are available to other
signed-in clients. A live activity view is an observation of a particular
piece of work; open that work explicitly when you want its reasoning, tool
calls, retries, or errors.

Draft text and transient interface state may remain local to the app where they
were created. Attach a file or send the message before expecting another app to
see it.

## Send Feedback

If your operator enables it, choose **feedback** in the header to report a bug or
suggest an improvement. Write what happened and press **Send**. A failed send
keeps your draft. Reports include your space, account, and app/server versions;
your conversation and logs are not attached.

You can also ask Ship to report an issue. On the `gsv` target it uses:

```bash
feedback 'The attachment download did not open.'
feedback < report.txt
```

Share only the details the person asked to report. `feedback --id UUID ...`
keeps the same report identity when retrying. The command returns a receipt once
the operator's inbox accepts the report; unavailable or failed sends return an
error. A receipt does not mean the issue has been fixed.

## Pages In This Section

- [Use the Web and Desktop surfaces](desktop-surfaces-and-apps.md)
- [Use voice and gestures](voice-gestures.md)
- [Read images with `img2txt`](image-reading.md)
