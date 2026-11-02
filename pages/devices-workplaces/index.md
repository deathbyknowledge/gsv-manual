# Connections

[Back to the manual](../../index.md)

Connecting a computer lets Ship work with that computer's files, commands, private networks, installed software, and hardware without moving all of it into Ship.

Ship and its helpers can also use an on-demand [cloud computer](cloud-computers.md)
for documents, spreadsheets, charts, media, or other software. Connected computers
and cloud computers share the same connection and tool interfaces; choose the
connection with the resources and access the work needs. Save useful files to GSV
before a temporary computer stops.

## Connect A Computer

Ship Desktop can guide connecting a computer for the first time:

1. Sign in to your Ship in the desktop app.
2. In the **Connect this computer** prompt, give the computer a display name and choose **connect**. (**Not now** skips it; **this computer** in the Ship menu opens it later.)
3. Wait for **Connected**; the desktop app connects the computer and installs its background service.
4. Verify that the computer appears online under **Connections** in Work.

Without the desktop app, choose **connect** beside Connections in the web app, name the computer, and run the `gsv pair` command it shows on that computer after installing Ship.

Ship can also guide the connection. **Chat → + → connect a computer** stages that
request without sending it. Ask what to call the computer and whether it
runs macOS, Linux or Windows, then run on `gsv`:

```bash
targets pair --name "My laptop" --platform mac
```

The JSON result contains the install and `gsv pair CODE` commands for this Ship
and release. Share each command with the owner in its own fenced code block so it
can be copied directly; skip installation if Ship is already installed.
The invitation lasts ten minutes and enrolls under the human owner's account.
When the user says it finished, check `targets show my-laptop` before claiming it is connected.

Check `targets list` before creating another connection. To reconnect an existing
one, use `--id TARGET_ID --replace`. `targets pair list` shows invitation status;
`targets pair cancel INVITATION_ID` cancels an unused invitation if its code was
lost or the user no longer wants it. Cancellation never disconnects an already-connected computer.

The background service keeps the computer connected when the desktop app window closes. Signing out of the desktop app and revoking the computer remain separate actions. On Linux and macOS the service updates itself when the operator releases an update; new installs go to `~/.gsv/bin` and need no administrator rights.

The CLI can inspect and control the same service. Run `gsv daemon --help` for the commands supported by the installed version.

## Windows Computers And Servers

Windows 10 or newer on x64 supports the desktop app, the CLI, the background daemon and local voice. Connecting the computer asks for administrator approval to install
an automatic Windows service. The computer can reconnect after reboot before
anyone signs in; signing out or closing the desktop app does not disconnect it.

Commands run as the dedicated `NT SERVICE\gsvd` account. Tools on the computer
share that account's OS permissions, including access to its daemon state; the
workspace is a starting directory, not a sandbox. Choose a workspace
whose permissions the enrolling user can change without elevation. Administrator
approval installs the service; workspace access is granted using that user's
existing permissions. Approval alone does not grant Ship or its helpers extra
access to protected application or system folders. Its default workspace
is `%USERPROFILE%\GSV`, and installation grants that account access to the
selected folder. Personal SSH keys, mapped drives and user-installed tools do
not automatically become available to the service. Install tools for the computer
and configure credentials for the service identity. Use UNC paths for network
shares. An administrator can choose a different Log On account in Windows
Services when that computer needs one. Reinstallation and upgrades preserve the
service's account, startup mode, recovery settings and state-directory permissions.
If another service uses
the `gsvd` registration, an administrator must resolve that conflict first.

`gsv daemon status`, `stop`, `start`, `restart`, `diagnostics` and `logs` inspect
or control the enrolled owner's service. `reload` applies that owner's changed
computer settings; run `gsv daemon install` again to change the workspace and its
permissions. Uninstalling the service removes its workspace grant and keeps
saved enrollment, logs and files. The desktop app login and computer enrollment
are separate credentials; removing one does not revoke the other.
Damaged configuration does not block service removal. If uninstall cannot revoke
the workspace grant, it reports that an administrator must remove it manually.
Reinstalling then uses the enrolling user's configuration instead of damaged
daemon configuration retained from the removed service.

Installer upgrades remember the previously selected installation directory.
Windows service updates require administrator approval. Close the desktop app and
run the host installer again; it updates the service and rolls back if the new
daemon cannot start. For servers, `install.ps1 -Headless` installs just the CLI
and daemon. Voice and the desktop app need an interactive login.

## Connect A Browser

Connect the **Your Ship** extension to make a browser profile a connection. Ship then reaches any site that profile is signed into, with no separate integration. See [Use a browser connection](browser-targets.md).

## Find Where Work Can Run

```bash
targets list
targets search "laptop"
targets show <target-id>
```

The connection ID is the stable name used in commands. A friendly label helps people recognize it.

## What Belongs On A Computer

Prefer a connected computer for:

- files that should remain there;
- locally installed programs;
- VPN or private-network access;
- local credentials that should not be copied elsewhere;
- GPUs, cameras, microphones, and other hardware;
- platform-specific automation.

## What Belongs In A Browser

Prefer a connected browser for:

- sites the user is signed into;
- web apps with no API or export;
- pages to watch for a change;
- browser-local state such as tabs, history, bookmarks, and downloads.

## Pages In This Section

- [Run commands and copy files across connections](targets-copy.md)
- [Use a browser connection](browser-targets.md)
- [Start a cloud browser and remember website logins](cloud-browsers.md)
- [Use a cloud computer](cloud-computers.md)
