# Use A Browser Target

[Computers And Browser](index.md)

A browser target lets GSV use operations deliberately exposed by a connected browser extension or profile. It is useful for browser-local state and actions that should happen in that profile.

## Find It

```bash
targets search "browser"
targets show <browser-target-id>
```

The target description lists the operations, permissions, and online state of that browser connection.

## Address Browser Files

Target IDs containing a colon use brackets in file syntax:

```bash
cp [browser:work]:/downloads/report.pdf ~/reports/report.pdf
img2txt [browser:work]:/screenshots/error.png
```

## Permission And Presence

Browser access uses the signed-in GSV identity and only the operations and permissions exposed by the current browser connection. Its target description is the complete list of what that browser can do for GSV.

If a requested action is unavailable, inspect the target before asking the user to reinstall or reconnect anything.
