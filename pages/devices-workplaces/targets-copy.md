# Run Commands And Copy Files Across Targets

[Computers And Browser](index.md)

A target is a place where GSV can perform an action. `gsv` means the installation itself. Connected computers and browser profiles have their own target IDs.

## Discover The Right Target

```bash
targets list
targets search "computer name or capability"
targets show <target-id>
```

Check that it is online and implements the needed operation before starting work that depends on it.

## Use A Target

Target-aware file, shell, and network operations keep the same meaning wherever they run. Select the intended target and keep the operation itself unchanged.

Use a target-qualified path to read or copy a remote file:

```bash
cp laptop:/home/sam/report.pdf ~/reports/report.pdf
cp ~/exports/data.csv laptop:/home/sam/Downloads/data.csv
```

Use brackets when a target ID itself contains a colon:

```bash
cp [browser:work]:/downloads/invoice.pdf ~/invoices/invoice.pdf
```

Use the selected target option in Shell or CodeMode when executing a command, filesystem request, or network request there.

## Copy Or Work In Place

- Work in place when the data, installed software, private network, or hardware belongs to that computer.
- Copy when another saved file should exist at the destination.
- Keep an exact file reference when another step only needs to resolve the same bytes later.

## Disconnects And Cancellation

If a target disconnects, the active operation fails, accepted file or network streams are cancelled, and partial files are discarded. A retry remains bound to the selected target unless the user chooses another.

After reconnection, inspect whether the original operation had an external side effect before retrying it.

## Permissions

Target selection is followed by authorization of the current identity, capability, path, and operation. Remote work may also require human approval.
