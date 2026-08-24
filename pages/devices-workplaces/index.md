# Computers And Browser

[Back to the manual](../../index.md)

Connecting a computer lets GSV work with that computer's files, commands, private networks, installed software, and hardware without moving all of it into GSV.

## Connect A Computer

The Desktop app can guide first-time setup:

1. Sign in to the GSV installation.
2. Choose a name for the computer.
3. Confirm machine enrollment.
4. Let Desktop install and start the background machine service.
5. Verify that the computer appears online under Machines.

The background service keeps the machine connected when the Desktop window closes. Desktop sign-out and machine revocation remain separate actions.

The CLI can inspect and control the same service. Run `gsv daemon --help` for the commands supported by the installed version.

## Find Where Work Can Run

```bash
targets list
targets search "laptop"
targets show <target-id>
```

The target ID is the stable name used in commands. A friendly label helps people recognize it.

## What Belongs On A Computer

Prefer a connected computer for:

- files that should remain there;
- locally installed programs;
- VPN or private-network access;
- local credentials that should not be copied elsewhere;
- GPUs, cameras, microphones, and other hardware;
- platform-specific automation.

## Pages In This Section

- [Run commands and copy files across targets](targets-copy.md)
- [Use a browser target](browser-targets.md)
