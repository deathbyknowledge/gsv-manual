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

Ship can also guide the connection. Ask what to call the computer and whether it
runs macOS, Linux or Windows, then run on `gsv`:

```bash
targets pair --name "My laptop" --platform mac
```

The JSON result contains the install and `gsv pair CODE` commands for this space
and release. Share each command with the owner in its own fenced code block so it
can be copied directly; skip installation if GSV is already installed.
The invitation lasts ten minutes and enrolls under the human owner's account.
When the user says it finished, check `targets show my-laptop` before claiming it is connected.

Check `targets list` before creating another place. To reconnect an existing one,
use `--id TARGET_ID --replace`. `targets pair list` shows invitation status;
`targets pair cancel INVITATION_ID` cancels an unused invitation if its code was
lost or the user no longer wants it. Cancellation never disconnects an already-paired device.

The background service keeps the machine connected when the Desktop window closes. Desktop sign-out and machine revocation remain separate actions. The service updates itself when the installation moves ahead; new installs go to `~/.gsv/bin` and need no administrator rights.

The CLI can inspect and control the same service. Run `gsv daemon --help` for the commands supported by the installed version.

## Connect A Browser

Pair the **Your GSV** extension to make a browser profile a target. GSV then reaches any site that profile is signed into, with no separate integration. See [Use a browser target](browser-targets.md).

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

## What Belongs In A Browser

Prefer a paired browser for:

- sites the user is signed into;
- web apps with no API or export;
- pages to watch for a change;
- browser-local state such as tabs, history, bookmarks, and downloads.

## Pages In This Section

- [Run commands and copy files across targets](targets-copy.md)
- [Use a browser target](browser-targets.md)
