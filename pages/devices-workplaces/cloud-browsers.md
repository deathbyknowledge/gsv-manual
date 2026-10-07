# Use A Cloud Browser

[Computers And Browser](index.md)

When the operator enables cloud browsers, Ship can start one even while the
user's own devices are offline. It uses the same `tabs` and `page` commands as
the browser extension. Ordinary browsers automatically remember website logins
for the local account in this space. They do not inherit the user's personal
browser login.

Each account has one automatic saved-login identity. Profiles created through
advanced commands stay separate. Forgetting the automatic state makes the next
ordinary start fresh, even when other saved profiles still exist.

## Start, Use, Stop

On the `gsv` target:

```bash
instance catalog
instance start browser --request-id <fresh-persisted-id> --seconds 900 --wait
instance get <browser-id>
```

An ordinary start reuses the account's current browser, including one that is
still starting. Use another tab for additional work. Reuse does not extend its
lifetime or reserve more usage. Every start request keeps its own receipt,
including requests that reused an instance.
If a start is rejected because the browser is preparing to stop, wait for the
stop to settle and retry the same request ID; that attempt has not been admitted.
It can reuse the browser if saving failed, or create a new one after termination.
The start result says `disposition: created` or `reused`. `--wait` returns when
ready, with a default timeout of 60000 ms (`--timeout MS`, maximum 120000).
A timeout stops waiting without stopping the browser; inspect the same saved
request ID to recover. Instance commands accept the displayed eight-character
target ID or full instance ID. An unknown instance ID is an error, including
for stop.

Request a separate temporary browser only when isolation is needed:

```bash
instance start browser --new --name 'Separate research' --request-id <fresh-persisted-id>
```

That browser has its own name and short target ID. It does not share saved
logins or replace the ordinary browser. The default saved login state is used
by only one running browser at a time.

Persist the start request ID before dispatch. If the response is lost, query
`instance get --request-id <id>` or repeat the exact same start and arguments.
Do not invent another request ID to recover an uncertain start.

Wait until the instance is `ready`, then use its returned target ID for ordinary
Read, Write, Shell and CodeMode operations. Run `tabs list`, `tabs open --active
<url>` and `page snapshot` on that browser target. Consult `skills show
browser-target` for the shared page commands. The target has temporary files and
a browser command shell; it is not a Linux machine.

Large `tabs list` results include `nextOffset`; continue with
`tabs list --offset <nextOffset>`. The cloud browser's `/proc/tabs.json` exposes
the first bounded page and the same pagination metadata.

Temporary storage is limited to 16 MiB per encoded file entry and 64 MiB in
total, including encoding and metadata. Oversized transfers are rejected
before reading their bodies. A failed save leaves existing files unchanged
and does not publish a new file. These temporary-file limits are separate
from the saved website-state allowance below.

When finished, export useful files and close tabs you opened. Do not stop a
shared browser just because one task ended. Stop an isolated browser you
created with `instance stop <browser-id> --wait` when finished. You can
also stop by the original ID with `instance stop --request-id <id>`, even when
the start response was lost. Stopped and failed instances remain terminal.
An ordinary start after the current browser stops creates a different target
and restores the saved login state. Cancelling a tool's wait does not
stop an already admitted browser.

Ordinary stop first commits saved state. If one site cannot be exported, the
result is `persistence.saveStatus: "partial"`: other sites are saved, the failed
site retains its previous saved storage and associated cookies, and normal stop
still succeeds. Inspect `persistence.issues` for affected origins and reasons.
Very wide or deeply nested storage can also produce a partial save: the browser
bounds temporary serialization work as well as saved bytes. Earlier state for
that site is retained when available, and other sites continue saving.
If the whole save fails, the browser remains running within its original
lifetime. Inspect `instance get <browser-id>` for the cause and diagnostic,
then retry with `browser profile save <browser-id>` when appropriate.
`instance stop <browser-id> --wait` returns after termination and release of the
saved-state lease. Use `--force` only for an intentional stop without preserving
unsaved changes. Expiry and forced stops can lose changes since the last save.
Never use `--force` to test persistence or fix unsupported storage. For a restart
test, use `instance stop <browser-id> --wait` and check whether the tested site
appears in `persistence.issues` before starting again. Waiting or closing tabs
does not fix an `unsupported` storage exception.

## Watch And Interact Together

Clicking a cloud browser below Zen's prompt, in a work receipt, or in Fleet opens
its live view directly. Zen remains behind the browser window, which has tabs,
an address strip, and the page filling its width. The view follows
Ship's active tab and shows its cursor and clicks. Watching does not pause
Ship. The person can click, scroll, paste and type in the same browser without
entering a separate control mode. Clicking pins the view to that tab; **Follow
Ship** resumes following. Human input gets brief priority and each browser action
finishes intact before another actor's input runs. Closing the viewer leaves
both the browser and Ship running.
The window uses Instrument's text controls: **expand** enlarges the view,
**close** leaves the browser running, and **more → stop browser** stops it.
The view streams page changes, drops superseded images on slow connections,
and reconnects after an interruption. A hidden view pauses capture; reopening
resumes the same browser. Viewing does not require repeated screenshot commands.

A slow page or interrupted live frame does not by itself stop the browser.
Health checks run independently of page JavaScript. A temporary provider
failure gets a bounded recovery window within the original lifetime; a missing
session or persistent failure stops the instance. Recovery does not repeat
agent actions. Inspect the page before deciding how to continue.

## Ask The Person To Sign In

Open the desired website first. On `gsv`, request human control for its tab and
the existing responsibility that owns the work:

```bash
browser handoff request <instance-id> <tab-id> --request-id <fresh-persisted-id> --purpose 'Sign in to the website' --work <responsibility-id>
```

Send the returned action URL to the person and yield. The request also appears
in Ship in the Web app. The person signs into GSV, opens the browser view, enters
the website's credentials there, and chooses **continue**. They can
switch tabs when a login provider opens a popup. The link does not grant browser
access without the person's GSV login. Each link stays tied to its original
request; an ended request cannot open or complete a later one. Send the current
request's action URL when another handoff is needed. Do not request website passwords or
verification codes in chat; the next chat message still belongs to Ship.

Cloud browsers report passkeys and hardware security keys as unavailable so an
invisible native prompt cannot block password sign-in. Use the site's password
or another sign-in method it offers. If the site requires a passkey, use a
connected personal browser; do not ask for the credential in chat.

Browser automation is paused during this handoff. Human-only open, image, input
and completion operations cannot be invoked by agents. Other work can continue.
**continue** completes only after saving succeeds. If saving fails, human control
and the waiting task remain open; the person can retry or cancel. Cancellation
remains available during a save and cannot be undone by its late completion.
Completion or cancellation reopens the matching waiting responsibility; its
deadline provides a recovery check if completion is interrupted. Inspect with:

```bash
browser handoff get <instance-id> <request-id>
```

After return, inspect the actual page before continuing. A cancelled or expired
request does not mean sign-in succeeded. Requests expire after fifteen minutes
or the browser's lifetime, whichever is earlier. A lost browser response does
not justify replaying a purchase, submission or another consequential action.

## Remembered Logins And Limits

Saved login state retains cookies, local storage and IndexedDB between ordinary
instances. No profile creation or selection is needed in the user flow. Advanced
`browser profile` commands expose `saveStatus` and `savedAt`; do not promise that unsaved
changes will survive. Websites can revoke sessions or require another login.
Saves run periodically, after human input settles, on handoff completion and
before an ordinary stop. Closing tabs does not remove their site data from the
next snapshot. Restore completes before readiness; a failed restore never
silently opens an empty browser. The viewer offers **retry save** and **stop
without saving** after a whole-save failure. Failed or oversized saves preserve
the previous successful snapshot. Partial saves show **saved with exceptions**;
the failed sites may require another login after restarting.

Saved state is discoverable in the native filesystem:

```text
/var/lib/gsv/browser/<human-account>/
  README.txt
  status.json
  sites.json
  state.enc
```

Read `status.json` for save times, errors, duration and sizes. `sites.json` breaks
down cookie domains, local storage and IndexedDB usage without login values.
Byte and record totals include all measured storage. If export exceeds the
allowance, collection stops early: `usage.complete` is false and the reported
required bytes are a lower bound. The previous snapshot remains intact.
Detailed database lists and names are bounded; `databaseUsageTruncated` marks
shortened or omitted details.
`cookieDomainsTruncated` marks omitted domain details. These flags describe the
metadata, independently of whether the website's state was saved successfully.
The complete usage breakdown is limited to 64 KiB. `sitesTruncated` means only
some site details fit; the largest contributors are kept and `siteCount` retains
the total measured count. This never truncates the saved website state.
`browser profile list [--offset N]` returns up to 32 summaries and `nextOffset`
when more remain. Use `browser profile get ID` for one profile's usage and issues.
Both expose `issues` for partial saves. Snapshot `savedAt` applies to the latest
commit; each issue's optional `retainedAt` identifies that site's older saved
data. No `retainedAt` means no earlier site snapshot was available. Parent-domain
cookies shared with the failed site's subdomains are retained too.
The raw serialized allowance defaults locally to 16 MiB; operators can set a
different limit up to 32 MiB. The snapshot is compressed and encrypted. Unchanged
state does not upload a new revision. `state.enc` is opaque and its key stays in
the instance service; copying it alone is not a portable backup.

Metadata and snapshot bytes are read-only. Deleting `state.enc`, or recursively
removing the account directory, invokes the same forget operation as profile
deletion: stop the browser using it, fence pending saves, erase snapshots and the
key. Cleanup may finish after the directory disappears. The next ordinary start
has fresh state. This mount requires the same owner and browser permissions as
the API; it does not bypass them.
Profile deletion removes stored login state and stops the browser using it:

```bash
browser profile get <profile-id>
browser profile delete <profile-id>
```

Fleet's **browser** action opens the current browser, starting one if needed.
There is no profile picker or take-control step. Stopped browsers leave the
ordinary Fleet list. `instance list --all` includes your 64 most recently created
terminal browsers alongside active ones, without per-site save issues. Use
`instance get ID` for recent details. Older instances retain their identity,
status and start-request receipts for exact lookup and safe retries; runtime
and detailed save diagnostics are discarded. Saved logins and usage accounting
have independent lifetimes. Instance commands report usage and limits.
Starting a new instance reserves its requested lifetime. Time counts while the browser is running,
including human sign-in, and unused allowance returns after confirmed stop.
An uncertain launch is never repeated automatically. If no provider session ID
was received, cleanup releases the concurrency slot three minutes after the
acquisition attempt, independently of the requested browser lifetime.
A browser that never became ready consumes no browser-time allowance. Its full
reservation returns when cleanup completes.
Runtime crossing a UTC month boundary is split between the monthly allowances,
while total rounded runtime stays capped by the reserved lifetime. Active
reservations remain held through rollover until confirmed termination.

Device-bound sign-in, hardware security keys, local extensions, operating-system
dialogs and websites that reject a cloud browser may require a connected
personal browser. Importing extension sessions is not supported. Linux container
instances are not available in this first browser implementation.
The saved state is not an entire Chrome user-data directory: session storage,
service-worker caches and filesystem-backed storage are excluded. Binary
buffers/views, dates, maps, sets, bigints and cycles in IndexedDB are preserved.
Unsupported types, including CryptoKey and Blob records, are reported as site
exceptions; supported sites still save. The save command returns a warning for
partial saves and a nonzero exit status for whole-save failures.
Do not promise that any particular site's login survives until it has been
tested through an actual stop and restart.
