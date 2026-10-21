# Run Commands And Copy Files Across Connections

[Connections](index.md)

An action runs in Ship's home or on a connection. `gsv` means Ship's home. Connected computers and browser profiles have their own connection IDs.

## Discover The Right Connection

```bash
targets list
targets search "computer name or capability"
targets show <target-id>
```

Check that it is online and implements the needed operation before starting work that depends on it.

## Use A Connection

Connection-aware file, shell, and network operations keep the same meaning wherever they run. Select the intended connection and keep the operation itself unchanged.

Use a connection-qualified path to read or copy a remote file:

```bash
cp laptop:/home/sam/report.pdf ~/reports/report.pdf
cp ~/exports/data.csv laptop:/home/sam/Downloads/data.csv
```

Use brackets when a connection ID itself contains a colon:

```bash
cp [browser:work]:/downloads/invoice.pdf ~/invoices/invoice.pdf
```

Use the selected target option in Shell or CodeMode when executing a command, filesystem request, or network request there.

Windows computer commands use PowerShell. The final statement determines success
(0 or 1); use `exit N` for an explicit code, or `exit $LASTEXITCODE` immediately
after a native program when its exact exit code matters. Keep drive-letter and UNC paths intact,
quote paths containing spaces, and check which service account owns the command.
A mapped drive in your interactive desktop may not exist for the background service;
use a UNC path with permissions for that service account instead.
Root-relative Windows paths stay on the current drive or share: `\docs` from
`//server/share/current` resolves to `//server/share/docs`.

## Copy Or Work In Place

- Work in place when the data, installed software, private network, or hardware belongs to that computer.
- Copy when another saved file should exist at the destination.
- Keep an exact file reference when another step only needs to resolve the same bytes later.

## Disconnects And Cancellation

If a connection drops, the active operation fails, accepted file or network streams are cancelled, and partial files are discarded. A retry remains bound to the selected connection unless the user chooses another.

After reconnection, inspect whether the original operation had an external side effect before retrying it.

## Permissions

Connection selection is followed by authorization of the current identity, capability, path, and operation. Remote work may also require human approval.
