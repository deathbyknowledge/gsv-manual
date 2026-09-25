# Computers And Browser

[Back to the manual](../../index.md)

Connecting a computer lets GSV work with that computer's files, commands, private networks, installed software, and hardware without moving all of it into GSV.

## Connect A Computer

The Desktop app can guide first-time setup:

1. Sign in to the space in Desktop.
2. In the **Connect this computer** prompt, give the computer a display name and choose **connect**. (**Not now** skips it; **this computer** in the space menu opens it later.)
3. Wait for **Connected**; Desktop pairs the computer and installs the background machine service.
4. Verify that the computer appears online under **Places** in Fleet.

Without Desktop, choose **connect** beside Places in the Web app, name the computer, and run the `gsv pair` command it shows on that computer after installing GSV.

The background service keeps the machine connected when the Desktop window closes. Desktop sign-out and machine revocation remain separate actions. The service updates itself when the installation moves ahead; new installs go to `~/.gsv/bin` and need no administrator rights.

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
