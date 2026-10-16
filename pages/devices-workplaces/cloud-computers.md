# Use A Cloud Computer

[Computers And Browser](index.md)

A cloud computer is a temporary Linux target for builds, scripts, compilation,
and other work while the owner's devices are offline. It uses ordinary Read,
Write, Edit, Shell, and network operations. It is a place where Ship or Crew
works, not a separate agent.

The operator must enable the `computer` template. Check `instance catalog` on
`gsv` before saying a computer needs to be connected. The initial image includes
Node.js, npm, Python, Git, and build tools. Use `/workspace` for working files;
check or install additional project toolchains there as needed.

## Keep Source Before Starting

Use an existing GSV repository for editable source and build instructions.
Inspect `rgit list` and `rgit info OWNER/REPO`, then read and edit its files under
`/src/repos/OWNER/REPO`. Writable repository file operations create commits
automatically; `rgit log OWNER/REPO --limit 1` shows the latest full commit hash.
Preserve other work in that repository.

Files in the computer are temporary. Save source changes back to the repository
and copy needed output to `gsv` before stopping. Stopping, expiry, or loss of the
computer destroys files and running commands. There is no saved disk or automatic
restore. For a website, `sites init` creates persistent source and `sites publish`
handles the build and output transfers. See [Build and publish a site](../files-knowledge/publish-site.md).

## Start, Use, Stop

Persist a fresh request ID in the work record before dispatch. Run on `gsv`,
replacing `REQUEST_ID` with that saved value:

```bash
instance catalog
instance start computer --request-id REQUEST_ID --name "Website build" --seconds 1800 --wait
```

Read the returned instance and use its `targetId` for ordinary tools. Select that
target in Shell to run, for example:

```bash
cd /workspace && node --version
```

Do not run the lifecycle commands inside the Linux shell; they belong to `gsv`:

```bash
instance get --request-id REQUEST_ID
instance list
targets show TARGET_ID
instance stop TARGET_ID --wait
```

Repeating the start with the same request ID and arguments returns the same
instance, even after it stops. A fresh ID requests a separate computer. A timeout
or cancellation of `--wait` only ends the wait; recover with `instance get
--request-id REQUEST_ID` instead of creating another computer. Browser profile
options and `--new` do not apply. The computer's fixed expiry is not extended by
work or retries.

## Copy Files Across Targets

Run cross-target copies on `gsv`. Replace `TARGET_ID` and the repository path:

```bash
cp /src/repos/OWNER/REPO/package.json TARGET_ID:/workspace/app/package.json
cp TARGET_ID:/workspace/app/dist/index.html /tmp/site-build/index.html
```

Use `[TARGET_ID]:/path` if the ID contains a colon. The GSV `cp` command copies
one file per call; it does not support recursive directory copies. Enumerate the
needed files and copy each while preserving relative paths, or use the existing
`fs.copy` syscall with explicit source and destination targets. These transfers
handle binary bytes; do not turn WASM, images, or archives into chat text.

## Long Commands And Cancellation

For a command that must be recoverable after a lost response, save a fresh UUID
as its `sessionId` before starting. The `shell.exec` syscall accepts:

```json
{
  "target": "TARGET_ID",
  "input": "npm ci && npm run build",
  "cwd": "/workspace/app",
  "sessionId": "SAVED_FRESH_UUID",
  "start": true,
  "timeout": 900000
}
```

The equivalent CodeMode call is `shell(command, options)`, with `target`, `cwd`,
`sessionId`, `start`, and `timeout` in the options. Set a timeout that fits the
remaining computer lifetime; the ordinary new-command default is two minutes.
Poll with `shell("", { target: targetId, sessionId })` in CodeMode, or `shell.exec`
with the same target and session ID, `input: ""`, and no `start`. Do not replay a
start or uncertain stdin to recover a response.

Cancelling a poll or losing the connection does not kill a detached command.
Use `await shell.cancel({ target: targetId, sessionId })` in CodeMode to stop the
session and its process tree. It invokes the ordinary `shell.cancel` syscall;
polling can then retrieve the terminal result.
Stopping the computer ends every command on it. If the computer itself is lost,
recover explicitly on a new one from saved source; the runtime does not rerun
work automatically.

## Delegate The Work Normally

Use ordinary Crew delegation when a separate worker is useful. Read the Crew
account named in Ship's `~/context.d/10-delegation.md`; replace `CREW_ACCOUNT`
with it:

```bash
proc delegate --as CREW_ACCOUNT --label "Build the site" --check-after 10m "Build the requested site from the agreed GSV repository. Use a temporary cloud computer if needed, publish with sites, and return the share URL, source repository, checks and computer status."
```

Give Crew the chosen repository and task requirements. Assign one worker to
write a shared checkout and retain the start request ID, target ID, and command
session IDs with the task. Delegated work follows the owner's capabilities and
approval policy. Ship remains responsible for assessing the result, completing
the requested delivery, and stopping a computer whose work is finished. Use
the existing [responsibility workflow](../agents-assistants/conversations-delegation.md#responsibilities)
for unfinished commitments.

## Permissions And Usage

Default permissions allow agent shell, filesystem, and network work on cloud
computers. **Settings → permissions → Cloud computers** changes that policy;
custom policies still apply. Personal computers have separate approval rules.
Computers belong to their initiating human account and space.

Computer concurrency and monthly seconds are separate from browser limits.
Starting reserves the requested lifetime. Usage runs from readiness until stop
or expiry; unused reservation is released after termination is confirmed. Check
the catalog and instance state when admission fails. Keep a computer running
while authorized work needs it, and stop it after the required files are saved.
