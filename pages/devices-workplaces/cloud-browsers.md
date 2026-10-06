# Use A Cloud Browser

[Computers And Browser](index.md)

When the operator enables cloud browsers, Ship can start one even while the
user's own devices are offline. It uses the same `tabs` and `page` commands as
the browser extension. Ordinary browsers automatically remember website logins
for the local account in this space. They do not inherit the user's personal
browser login.

## Start, Use, Stop

On the `gsv` target:

```bash
instance catalog
instance start browser --request-id <fresh-persisted-id> --seconds 900
instance get <instance-id>
```

An ordinary start reuses the account's current browser, including one that is
still starting. Use another tab for additional work. Reuse does not extend its
lifetime or reserve more usage. Every start request keeps its own receipt,
including requests that reused an instance.

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

When finished, export useful files and run `instance stop <instance-id>`. You can
also stop by the original ID with `instance stop --request-id <id>`, even when
the start response was lost. Stopped and failed instances remain terminal.
An ordinary start after the current browser stops creates a different target
and restores the saved login state. Cancelling a tool's wait does not
stop an already admitted browser.

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
Use the window's secondary menu to stop it.

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
access without the person's GSV login. Do not request website passwords or
verification codes in chat; the next chat message still belongs to Ship.

Browser automation is paused during this handoff. Human-only open, image, input
and completion operations cannot be invoked by agents. Other work can continue.
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
Profile deletion removes stored login state and stops the browser using it:

```bash
browser profile get <profile-id>
browser profile delete <profile-id>
```

Fleet's **browser** action opens the current browser, starting one if needed.
There is no profile picker or take-control step. Stopped browsers leave the
ordinary Fleet list; `instance list --all` retains their records. Instance
commands report usage and limits. Starting a new instance reserves its requested lifetime. Time counts while the browser is running,
including human sign-in, and unused allowance returns after confirmed stop.

Device-bound sign-in, hardware security keys, local extensions, operating-system
dialogs and websites that reject a cloud browser may require a connected
personal browser. Importing extension sessions is not supported. Linux container
instances are not available in this first browser implementation.
