# Use A Cloud Browser

[Computers And Browser](index.md)

When the operator enables cloud browsers, Ship can start one even while the
user's own devices are offline. It uses the same `tabs` and `page` commands as
the browser extension. It begins with a temporary profile or an explicitly
selected saved profile; it does not inherit the user's personal browser login.

## Start, Use, Stop

On the `gsv` target:

```bash
instance catalog
browser profile list
instance start browser --request-id <fresh-persisted-id> --profile <profile-id> --seconds 900
instance get <instance-id>
```

Omit `--profile` for a temporary browser. Create a saved profile with
`browser profile create Personal --request-id <fresh-persisted-id>`.
One browser at a time may use a saved profile.

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
Another start creates a different target. Cancelling a tool's wait does not
stop an already admitted browser.

## Ask The Person To Sign In

Open the desired website first. On `gsv`, request human control for its tab and
the existing responsibility that owns the work:

```bash
browser handoff request <instance-id> <tab-id> --request-id <fresh-persisted-id> --purpose 'Sign in to the website' --work <responsibility-id>
```

Send the returned action URL to the person and yield. The request also appears
in Ship in the Web app. The person signs into GSV, opens the browser view, enters
the website's credentials there, and chooses **Done — return to Ship**. They can
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

## Profiles And Limits

Saved profiles retain cookies, local storage and IndexedDB between instances.
Inspect the profile's `saveStatus` and `savedAt`; do not promise that unsaved
changes will survive. Websites can revoke sessions or require another login.
Profile deletion removes stored login state and stops the browser using it:

```bash
browser profile get <profile-id>
browser profile delete <profile-id>
```

Fleet offers the same start, profile, open-browser and stop actions. The user
sees the remaining browser allowance and concurrent instance limit. Starting
reserves the requested lifetime. Time counts while the browser is running,
including human sign-in, and unused allowance returns after confirmed stop.

Device-bound sign-in, hardware security keys, local extensions, operating-system
dialogs and websites that reject a cloud browser may require a connected
personal browser. Importing extension sessions is not supported. Linux container
instances are not available in this first browser implementation.
