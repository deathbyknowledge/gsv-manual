# Use The Web And Desktop Surfaces

[Web And Desktop](index.md)

The web app keeps its header, background and drafts while changing views.
On phones, use **menu** in the header to choose a view.
Browser **Back** and **Forward** retrace those destinations, including People lists,
conversations, requests and your profile, without reloading the page. Drafts are
retained while navigating within the open app. Reloading a People destination
restores the selected list, conversation, request or profile.

## Ship And Work

**Chat** always opens Ship. Separate work opens as a visibly labelled helper
with a Back action, while Ship remains available.

Use the **Ship and helpers** section in **Work** when you want to:

- see which helpers are active, waiting, finished, or failed;
- inspect reasoning, tool calls, approvals, and errors;
- continue, abort, reset, or remove a particular helper;
- return to Ship without stopping the work.

See [Messages, work, and delegation](../agents-assistants/conversations-delegation.md)
for the difference between sent messages and work activity.

While Chat shows **Reconnecting…**, you can keep writing and editing the draft.
Sending waits for the connection to return; reconnecting does not send the draft
automatically.

Code blocks in Ship replies and Memory have a **copy** action. Long lines scroll
within the block; copy keeps indentation and line breaks without adding a final newline.
Scrolling Chat selects the message nearest the middle of the visible conversation;
at either end it selects the first or latest message. On phones, the down arrow
on the right returns to the latest message. Closed completed action summaries are
hidden on phones once Ship replies. Actions remain in **Settings → Logs**;
active work, failures, approvals and already-open summaries stay visible.
Direct `$` commands show a compact connection heading on phones; expand it to read the
full command, its output and terminal controls.
Messages longer than eighteen rendered line-heights fold to twelve behind
**read more**; **show less** folds them again. Shorter messages and replies you
watched arrive stay open.
Installed PWAs fill the screen behind the home indicator, with safe-area padding
inside the page to keep the controls reachable.
When the activity line is visible above the prompt, a lavender edge marks the
bottom of the transcript only while text is being clipped there. It clears between
lines and messages and at the end of the conversation.

## Work

Work is the view for connections and helpers:

- **Connections** shows connected computers and browsers and their state; **connect** adds a new one.
- **Ship and helpers** shows running and finished work with its controls.
- Open a connection and choose **browse files** for its folders, file previews and reader/editor.

On phones, connections and helpers use compact rows; their inspectors keep the additional details. Helper responsibility counts open the matching list in Chat.

Open **Settings → Logs** for every action, its purpose and outcome.

Chat's composer starts on **Ship's home** (`gsv`). Choose another connection
explicitly to address a message or command to it. That choice stays when
switching views.

Check the selected connection before changing a file or running a command. A path
such as `laptop:/projects/report` acts on that connection; an unqualified
path uses the current connection and working directory.

## Context In Chat

The activity line above Chat's prompt combines ongoing plans and People messages.
Tap **N ongoing** (or **plans** when none are active) for responsibilities and
routines. The panel stays over the conversation, with **ongoing**, **routines**
and **history** at one level. Responsibility rows show a short status, assignee and
next check. Open one to read its full waiting explanation, inspect details,
cancel it, or **ask Ship** about that exact responsibility. Child steps stay grouped
beneath their parent. Routines show cadence and next-run, paused or failed state,
with pause/enable controls and editing for supported routine types. Event-driven policies live in
**Settings → Standing responsibilities**.

The composer’s **+** menu separates **add context** from **ask Ship** and offers:

- **attach a file** from this device;
- **find a person** by handle or saved name, then mention them or open contact controls;
- **reference a file** on a connection;
- **create a routine**, **connect a computer**, or **start a browser** as requests to Ship.

A handle such as `esteve` or `@esteve` opens that person’s profile on `gsv.space`.
Use a full address for a Ship hosted elsewhere. Saved people use the full available
list height in the contextual panel.

In the file picker, **../** above a connection’s entries moves toward its
filesystem root and stops there. Tapping a file name immediately adds its
connection and path to your Chat draft. Work’s file browser still opens a preview
with **talk about it**.
Files can change after being referenced.

Selecting a request adds ordinary editable text and preserves existing text
and attachments. Review, change or remove it before sending. Selection alone
sends nothing and grants no permissions. Sent requests use the normal message
rendering and history. Routine and responsibility references include exact record
IDs; person references include the profile URL.

**Ask Ship** in People and Memory uses the same composer.
A person mention does not contact them automatically.

Pasting more than 400 characters or eight lines creates a **pasted text** chip.
Tap it to inspect the full text or use its remove button. Sending joins your typed
words with the pasted blocks in order, preserving the pasted whitespace. Command
pastes starting with `$` or `!` stay in the prompt.

Chat failures show a short explanation and a next step. Open **details** for the
original error when diagnosing a problem.

On phones, opening the keyboard shrinks the content area between the header and
composer. Lists and message history scroll within the available space; the page
itself stays fixed. The star field retains its full-screen background.

## People

Open **People** (`p`) to connect with someone on another Ship. **connect**
creates an invitation link; **I have an invitation** accepts a link or code.
Handles are another way to send a first message. Incoming
requests wait for an explicit acceptance, which opens the conversation.
Inviting and accepting ask each person to choose who handles new messages on
their own side, with neither option preselected.

People uses the same growing prompt as Chat. Its **+** opens the attachment file
picker, and **send** appears beside the prompt when there is something to send.
The profile editor keeps its title and back arrow fixed while its form scrolls;
the lavender edge appears only where that scrolling cuts through text.

You can message people yourself or choose **ask Ship** to open an editable request
in your ordinary Ship chat. The first-use examples help you start with a concrete
task, such as making plans together. **Automatically handle new messages** in
conversation **details** changes your choice later. On phones, **more** holds
**ask Ship**, **search** and **details**, and the back arrow returns to the
full-height conversation list. Replies associated with assigned tasks can still reach Ship
when it is off; connecting or enabling it does not replay existing messages.

A dot beside People marks unread activity. Chat also shows unread conversations
and incoming requests beside ongoing plans in one compact line above the prompt, including after
reload. Select a person to read and reply without leaving Chat. Closing the panel
keeps an unfinished draft, and new messages do not move your reading position. See
[Connect with another Ship](../integrations/contacts.md) for messages, private
controls, and task-specific coordination.

## Browser Extension

**Your Ship** is the browser extension that makes a browser a connection.

The Your Ship extension requires a Chromium-based browser, such as Google Chrome
or Microsoft Edge. Firefox and Safari are not supported.

In Work,
choose **connect** beside Connections and pick **Browser**, then load the extension
and paste the invitation into it. Once it says **Ready**, the browser appears
under Connections.

## Attachments

When an app attaches an image, document, audio recording, or other file, Ship
stores the media and puts a reference in the message. Other authorized clients
load the referenced bytes when the attachment is displayed or used.

See [Work with media](../files-knowledge/media.md) for reading, creating, and
transcribing media.

## The Desktop App

The install script opens Desktop automatically when run in a local graphical
terminal. Set `GSV_NO_LAUNCH=1` to skip opening it; headless, SSH, CI and
redirected sessions keep the installation without launching a window. You can
open it later with `gsv desktop`.

The installer puts the `gsv` command on `PATH` for future shells. On Linux and
macOS, the `curl ... | bash` installation cannot change the parent terminal's
environment; to use the CLI there immediately after a default installation, run
`export PATH="$HOME/.gsv/bin:$PATH"`. Desktop opens without that extra step.

Ship Desktop is the same web app in a native window, with local voice and
a built-in way to connect the computer it runs on. On first launch, choose:

- **Create your Ship**: choose a handle, verify your email, and set a password.
  No invite code is needed.
- **Open Ship**: sign in with your email to choose your Ship, or enter its handle
  or custom address directly. Then sign in with your Ship's password.

Your Ship's name at the top of the window is a menu. It shows its handle
and offers **this computer** (connect or inspect this computer), **disconnect**
(sign out and return to the Ship picker), and **quit**. When a
locked account needs recovery, **recover account** appears there too.

Closing the window is the same as **quit**: unsent work is guarded, credentials
are flushed, and the app exits. The computer's background service,
`gsvd`, is independent and keeps the
computer connected after the desktop app closes.

## Connect This Computer

After sign-in, the desktop app offers **Connect this computer** so your Ship can
use this computer's files and commands even when the app is closed. Give it a
display name and choose **connect**; the desktop app creates the same connection
invitation Work would, connects the computer, and installs the background
service. Choose **Not now** to skip it for this session; **this computer** in the
Ship menu opens the same dialog later and shows the connection's status.

A connection for the same Ship and account resumes automatically. A
connection to another Ship or account, and a separate CLI login, are left
alone. If the Ship forgets the computer, the desktop app offers to connect it again
with the same display name and workspace.

## Signing Out

**disconnect** ends the current app session and clears that session's private
cached data. The Ship account, messages, work, and separately managed computer
credentials remain in place; the connected computer stays connected until it is
forgotten in Work.
