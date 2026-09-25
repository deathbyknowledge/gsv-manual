# Use The Web And Desktop Surfaces

[Web And Desktop](index.md)

## Ship And Work

**Zen** always opens the personal intelligence. Separate work opens in a visibly
labelled Work session with a Back action, while Ship remains available.

Use the **Processes** block in **Fleet** when you want to:

- see which tasks are active, waiting, finished, or failed;
- inspect reasoning, tool calls, approvals, and errors;
- continue, abort, reset, or remove a particular task;
- return to Ship without stopping the work.

See [Messages, work, and delegation](../agents-assistants/conversations-delegation.md)
for the difference between sent messages and work activity.

## Fleet

Fleet is the operational view:

- **Places** shows connected computers and browsers and their state; **connect** pairs a new one.
- **Processes** shows running and finished work with its controls.
- **Contacts** shows people on other GSVs; **add contact** starts a pairing.
- **Responsibilities** shows promises, follow-ups, and delegated work Ship is tracking.
- **Ledger** shows every action taken on the installation, with its purpose and outcome.
- **Files** shows recently touched files across places.

Check the selected target before changing a file or running a command. A path
such as `laptop:/projects/report` acts on that connected target; an unqualified
path uses the current target and working directory.

## Browser Extension

**Your GSV** is the browser extension that makes a browser a place. In Fleet,
choose **connect** beside Places and pick **Browser**, then load the extension
and paste the invitation into it. Once it says **Ready**, the browser appears
under Places and as a target.

## Attachments

When an app attaches an image, document, audio recording, or other file, GSV
stores the media and puts a reference in the message. Other authorized clients
load the referenced bytes when the attachment is displayed or used.

See [Work with media](../files-knowledge/media.md) for reading, creating, and
transcribing media.

## The Desktop App

Desktop is the same Instrument app in a native window, with local voice and
hands-free input and a built-in way to connect the computer it runs on. On first
launch it asks for a space: type a handle (it fills in the space domain) or paste
a custom address. Owner verification opens in the system browser.

The space name at the top of the window is a menu. It shows the space address
and offers **this computer** (connect or inspect this computer), **disconnect**
(sign out of the space and return to the space picker), and **quit**. When a
locked account needs recovery, **recover account** appears there too.

There is no background tray application. Closing the window is the same as
**quit**: unsent work is guarded, credentials are flushed, and the app exits. The
computer's background machine service, `gsvd`, is independent and keeps the
computer connected after Desktop closes.

## Connect This Computer

After sign-in, Desktop offers **Connect this computer** so your Ship can use
this computer's files and commands even when the app is closed. Give it a
display name and choose **connect**; Desktop creates the same device invitation
Fleet would, pairs the computer, and installs the background service. Choose
**Not now** to skip it for this session; **this computer** in the space menu
opens the same dialog later and shows the connection's status.

An existing connection for the same space and account resumes automatically. A
connection to another space or account, and a separate CLI login, are left
alone. If the space forgets the computer, Desktop offers to connect it again
with the same display name and workspace.

## Signing Out

**disconnect** ends the current app session and clears that session's private
cached data. The GSV account, messages, work, and separately managed machine
credentials remain in place; the connected computer stays connected until it is
forgotten in Fleet.
