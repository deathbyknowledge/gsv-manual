# Use A Cloud Computer

[Computers And Browser](index.md)

Computer fluency is part of Ship's personal intelligence. Ship and Crew can use
an on-demand Linux computer to work with documents, analyze spreadsheets, make
charts, process media, or run software for the user. The user does not need to
operate a terminal or keep a personal computer running.

Connected user devices and cloud instances use the same target and tool
interfaces. Choose a connected user device when the work needs files, programs,
private networks, or hardware there. Choose a cloud computer when it suits the
work. For website interaction, use a [browser target](browser-targets.md),
connected or [on demand](cloud-browsers.md).

## Choose A Computer

Run discovery on `gsv` before asking the owner to connect a device or declaring
that a required tool is unavailable:

```bash
targets list
instance catalog
```

Reuse a suitable ready computer or start an available `computer` template.
Availability and limits come from the operator. The initial image includes
Python, Node.js, npm, Git, and build tools. Install additional software as the
task requires. Use `/workspace` for working files.

Run GSV management commands on `gsv`; run Python, Node.js, and installed software
on the computer target. A missing program on `gsv` does not mean Ship cannot use
it on a computer.

## Start And Use It

Save a fresh request ID with the work before dispatch. Replace `REQUEST_ID`
with that saved value and run on `gsv`:

```bash
instance start computer --request-id REQUEST_ID --name "Spending analysis" --wait
```

Use the returned `targetId` with ordinary Read, Write, Edit, Shell, and network
tools. For example, select that target in Shell and run:

```bash
cd /workspace && python3 --version
```

Retrying the same request ID and arguments returns the same instance, including
after it stops. If the wait times out or is cancelled, check its outcome rather
than starting another computer:

```bash
instance get --request-id REQUEST_ID
instance list
```

A fresh ID requests a separate computer. The fixed expiry is not extended by
work or retries. Browser profiles and `--new` do not apply to computers.

## Save And Deliver The Result

Keep files the user needs in their home on `gsv`. Preserve scripts or source
needed for later edits there too; a [GSV repository](../files-knowledge/repositories.md)
is useful for reusable projects. Files and installed software on the computer
are temporary: stop, expiry, or loss destroys them.

Copy input and output files using `cp` on `gsv`. Replace `OWNER` with the human
owner's account and `TARGET_ID` with the computer's target:

```bash
cp /home/OWNER/expenses.csv TARGET_ID:/workspace/expenses.csv
cp TARGET_ID:/workspace/spending.xlsx /home/OWNER/spending.xlsx
cp TARGET_ID:/workspace/spending.png /home/OWNER/spending.png
```

Use `[TARGET_ID]:/path` if the ID contains a colon. `cp` copies one file per call;
it does not recursively copy directories. Enumerate the needed files or call
the `fs.copy` syscall with explicit source and destination targets. Transfers
preserve binary bytes, including spreadsheets, PDFs, and images.

Check the result before delivering it. Give the useful answer in the message,
use a visual when it explains the result better, and attach the usable files
when they are the deliverable. Keep working notes in GSV. Stop the computer when
its work is finished and needed files are saved; run on `gsv`:

```bash
instance stop TARGET_ID --wait
```

Use ordinary [Crew delegation](../agents-assistants/conversations-delegation.md#delegating-a-bounded-task)
for substantial work. Share the outcome, input files, constraints, and where to
save the result. Keep the request ID, target, and command sessions with the
[responsibility](../agents-assistants/conversations-delegation.md#responsibilities)
so work can be recovered. Ship checks the outcome and delivers it to the user.

## Long Commands And Cancellation

For a recoverable command, save a fresh UUIDv4 as its `sessionId` before dispatch.
In CodeMode, replace `TARGET_ID` and `SAVED_UUIDV4`:

```javascript
return await shell("python3 analyze.py", {
  target: "TARGET_ID",
  cwd: "/workspace",
  sessionId: "SAVED_UUIDV4",
  start: true,
  timeout: 600000
});
```

This uses `shell.exec` with `start: true`. Set a timeout within the remaining
computer lifetime; new commands otherwise default to two minutes. Poll with
`shell("", { target, sessionId })`, omitting `start`. Do not replay a start or
uncertain stdin to recover a lost response.

Cancelling a poll or disconnecting does not kill a detached command. Use
`await shell.cancel({ target, sessionId })` to stop the session and its process
tree, then poll for its terminal result. Stopping the computer ends all commands.
If the computer is lost, recover explicitly on a new one from saved files;
there is no automatic restore or replay.

## Permissions And Usage

Default permissions allow agent shell, filesystem, and network work on cloud
computers. **Settings → permissions → Cloud computers** changes that policy;
custom policies still apply. Connected user devices have separate approval
rules. Computers belong to their initiating human account and Ship.

Computer concurrency and monthly seconds are separate from browser limits.
Starting reserves the requested lifetime. Usage runs from readiness until stop
or expiry; unused reservation is released after termination is confirmed. Check
the catalog and instance state when admission fails.
