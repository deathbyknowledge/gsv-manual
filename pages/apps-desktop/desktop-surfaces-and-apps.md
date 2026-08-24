# Use The Web And Desktop Surfaces

[Web And Desktop](index.md)

## Home And Work

Home always opens the personal intelligence. Separate work opens in a visibly
labelled Work session with a Back action, while Home remains available.

Use the Work view when you want to:

- see which tasks are active, waiting, finished, or failed;
- inspect reasoning, tool calls, approvals, and errors;
- continue, abort, reset, or remove a particular task;
- return to Home without stopping the work.

See [Messages, work, and delegation](../agents-assistants/conversations-delegation.md)
for the difference between sent messages and work activity.

## Files, Terminal, And Repositories

- **Files** browses and edits files on an authorized target.
- **Terminal** runs commands on the selected target.
- **Repositories** shows repositories, history, diffs, and changes.
- **Machines** shows connected computers and their state.

Check the selected target before changing a file or running a command. A path
such as `laptop:/projects/report` acts on that connected target; an unqualified
path uses the current target and working directory.

## Attachments

When an app attaches an image, document, audio recording, or other file, GSV
stores the media and puts a reference in the message. Other authorized clients
load the referenced bytes when the attachment is displayed or used.

See [Work with media](../files-knowledge/media.md) for reading, creating, and
transcribing media.

## Desktop Status Menu

Desktop remains available from the system status area when the main window is
closed. Its menu can:

- reopen GSV;
- show or retry Desktop's connection to GSV;
- connect, restart, or diagnose the current computer;
- start or finish voice input;
- show gesture state and open the gesture guide;
- quit Desktop completely.

Closing the main window leaves Desktop available in the status area. **Quit
GSV** exits Desktop completely. The background machine remains connected until
it is disconnected or revoked through Machines or the daemon controls.

## Signing Out

Signing out ends the current app session and clears that session's private
cached data. The GSV account, messages, work, and separately managed machine
credentials remain in place.
