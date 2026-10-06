# Use A Browser Target

[Computers And Browser](index.md)

A browser target is a browser profile the user paired with the **Your GSV** extension. GSV works inside that profile, so it reaches whatever the user is signed into there: a calendar, mail, a billing portal, an admin dashboard, a private forum. A site the browser is already logged into needs no MCP server, OAuth account, or other integration.

To connect one, choose **connect** beside Places in Fleet, pick **Browser**, and pair the **Your GSV** extension with the invitation shown. See [Use the Web and Desktop surfaces](../apps-desktop/desktop-surfaces-and-apps.md).

Ship can create the invitation with `targets pair --name "My browser" --platform browser`
on `gsv`. Share the returned extension download, installation instructions and code
with the owner. They paste the code into the extension panel; browsers do not use
the terminal's `gsv pair` command.

## What A Browser Reaches

- Any site the profile is signed into, through the user's own session.
- Web apps with no API or export: read the page, fill a form, download a file.
- Pages to watch: open one on a schedule and report when something changes.
- Browser-local state such as tabs, history, bookmarks, cookies, and downloads, when the task calls for it.

"Can you see my calendar?" is a browser question. When a browser is paired, open the calendar's web app in a tab and read it rather than asking the user to describe their schedule or to connect an integration.

## Find It

An operator-enabled [cloud browser](cloud-browsers.md) is another browser target.
It can run while personal devices are offline and restore a saved cloud profile.
Use `instance catalog` to discover availability. Its first website login happens
through GSV's human browser view.

Check for a browser before telling the user that GSV cannot reach a service:

```bash
targets search "browser"
targets show <browser-target-id>
```

The target description lists the operations, permissions, and online state of that browser connection. If no browser is paired, say that pairing the Your GSV extension would give GSV that site through the user's signed-in session, and point to the connection steps above.

## Work In A Browser

Load `skills show browser-target` for the exact commands. The usual sequence on the browser target is `tabs open <url>`, then `page text` or `page snapshot` to read, and `page click` or `page type` to act. Approval follows the policy in [Models and approvals](../settings/ai-voice-approvals.md).

## Address Browser Files

Target IDs containing a colon use brackets in file syntax:

```bash
cp [browser:work]:/downloads/report.pdf ~/reports/report.pdf
img2txt [browser:work]:/screenshots/error.png
```

## Permission And Presence

Browser access uses the signed-in GSV identity and only the operations and permissions exposed by the current browser connection. Its target description is the complete list of what that browser can do for GSV.

If a requested action is unavailable, inspect the target before asking the user to reinstall or reconnect anything.
