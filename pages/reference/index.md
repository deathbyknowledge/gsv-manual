# Find Any Command Or Capability

[Back to the manual](../../index.md)

GSV has two complementary sources of help:

- This manual explains complete product workflows, choices, and recovery.
- The live `man` catalog describes commands and capabilities available in the current GSV.

## Search By Outcome

Describe the goal in plain language:

```bash
man --search -- "copy a photo from my laptop"
man --search -- "send a reminder tomorrow"
man --search -- "use my issue tracker"
```

Search results can include:

- native commands;
- connected computers and browser targets;
- installed skills;
- ready MCP integrations.

Open exact command help with:

```bash
man <command>
<command> --help
```

## Search This Manual

```bash
wiki info gsv-manual
wiki search "query" --prefix gsv-manual
wiki read gsv-manual/pages/reference/command-map.md
```

Use the manual when the task involves several steps, a choice between mechanisms, or recovery from failure. Use `man` for current syntax and availability.

## Other Discovery Commands

```bash
targets list                 # connected places where work can run
skills search "query"       # reusable procedures
mcp list                     # connected external services
mcp search "query"          # tools across those services
oauth list                   # connected provider accounts
wiki list                    # available knowledge collections
proc list                    # visible work
message destinations --all  # places messages may be sent
```

## Pages In This Section

- [Command map](command-map.md)
- [Shell, CodeMode, network, and one-shot AI](shell-codemode-network.md)
- [Troubleshooting](troubleshooting.md)
