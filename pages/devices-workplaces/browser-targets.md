# Use A Browser Target

[Computers And Browser](index.md)

Browser use is a built-in GSV capability. A browser target can be the user's
browser connected through the **Your GSV** extension, or an on-demand
[cloud browser](cloud-browsers.md) that Ship starts and manages. Both use the
same page and tab commands described below; inspect each target's advertised
capabilities for additional features.

The extension uses the user's existing signed-in sessions. A cloud browser
keeps its own saved sessions, with the person signing in through GSV's live view.
Either can reach a calendar, mail, billing portal, admin dashboard or private
forum through its website. A site the selected browser is already logged into
needs no MCP server, OAuth account or other integration.

To connect the user's browser, choose **connect** beside Places in Fleet, pick **Browser**, and pair the **Your GSV** extension with the invitation shown. See [Use the Web and Desktop surfaces](../apps-desktop/desktop-surfaces-and-apps.md). Cloud provisioning, saved sessions and human handoffs are covered in [Use a cloud browser](cloud-browsers.md).

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
It can run while personal devices are offline and automatically remembers
website logins for the local account. Use `instance catalog` to discover
availability. Ordinary starts reuse the current browser; use tabs for additional
work. Its first website login happens through GSV's browser view, which also lets
the person watch and interact while Ship works.

Check for a browser before telling the user that GSV cannot reach a service:

```bash
targets search "browser"
targets show <browser-target-id>
```

The target description lists the operations, permissions and online state of
that browser. If none is available, check `instance catalog` for cloud browser
support or offer to pair the Your GSV extension. Choose the browser containing
the relevant tab or website session; a new cloud browser does not inherit the
extension browser's logins.

## Work In A Browser

Load `skills show browser-target` for the exact commands. The usual sequence on the browser target is `tabs open <url>`, then `page text` or `page snapshot` to read, and `page click` or `page type` to act. Approval follows the policy in [Models and approvals](../settings/ai-voice-approvals.md).

`tabs list` returns a bounded page of tabs. If it includes `nextOffset`, continue
with `tabs list --offset <nextOffset>` until that field is absent. `count` is the
number returned in this page and `total` is the current inventory size. An
ellipsis marks shortened titles or URLs; use the tab ID to address the page.

Snapshots retain the individual controls inside calendar rows, list items, and
web components. Click the desired button's reference; a reference addresses one
element and takes no selector index. Click and type briefly wait for temporary
overlays to clear before failing, without repeating input that was already sent.
For a persistent obstruction, inspect a fresh snapshot and handle the visible
dialog or menu. If a control remains outside the viewport after scrolling, the
command reports that no input was sent. Inspect `page screenshot` for a misplaced
popup or other layout problem instead of repeating the click or scrolling again.

Use `page key Space` (or a quoted literal space), `Enter`, `Tab`, `ArrowDown`,
`Escape`, `Ctrl+a`, or `Shift+Tab` for keyboard interaction. Keys go to the focused
control, including controls inside open shadow roots. Action results distinguish
input delivery from observed changes; inspect the resulting page to confirm the
website did what the task required.

Use `page fill` to replace a field's value, including native date/time inputs;
`page type` inserts text. Form commands verify the resulting state:

```bash
page fill --label 'From' 'Amsterdam Centraal'
page fill --role input-time '10:00'
page select --label 'Class' --option-label 'First'
page check --label 'Direct only'
page click --role button --name 'Plan' --snapshot
```

Dates use `YYYY-MM-DD`; times use `HH:mm`. `page select` addresses native
dropdowns; custom listboxes use `page click --role option --name '…'`. Use
`--unchecked` to clear checked state. An already matching checkbox is not
clicked again. Password values are omitted from snapshots and action results.

Role/name and field-label locators require one exact accessible match and
return candidate refs when ambiguous. Add `--within @ref` using a form or
dialog reference from a snapshot to narrow the lookup. `page snapshot --within
@ref` inspects just that region. Action `--snapshot` returns the complete JSON
receipt on its first line followed by a readable outline with fresh state and
refs. Add `--json` when you need one JSON object containing the receipt and
structured snapshot tree. `page wait` also accepts role/label locators.
`page --help` is the current command reference.

`snapshot | grep` is useful for reading a large page, but locating a known field
or button should use a precise locator or reference. Do not depend on extracting
reference IDs from prose. Visible dialogs appear above the snapshot outline with
usable references, even when the outline is truncated. A missing semantic
locator also mentions visible dialogs. If a search is empty, inspect the dialog
before retrying: it may hide background content from accessibility. Use
`page snapshot --within <dialog-ref>` to inspect its controls.
Use action `--snapshot` when input reveals new
controls or you need to inspect the resulting form; a verified value change
usually needs only its receipt. If the optional snapshot fails, `snapshotError`
is included in the completed action's receipt. Inspect again instead of
repeating the input.

Keep action receipts intact instead of cutting them with `head`. Chain dependent
actions with `&&` so a failure stops the sequence. If an action must be piped,
enable `set -o pipefail`; otherwise the pipe reader can hide its failure. Exit
zero means the command completed; check verification and observed state before
proceeding. Prefer `page wait` for the expected control over a fixed sleep.

## Address Browser Files

Target IDs containing a colon use brackets in file syntax:

```bash
cp [browser:work]:/downloads/report.pdf ~/reports/report.pdf
img2txt [browser:work]:/screenshots/error.png
```

## Permission And Presence

Browser access uses the signed-in GSV identity and only the operations and permissions exposed by the current browser connection. Its target description is the complete list of what that browser can do for GSV.

If a requested action is unavailable, inspect the target before asking the user to reinstall or reconnect anything.
