# Wikis And Repositories

[Files, Memory, And Skills](index.md)

## Wikis

A wiki is a repository organized for searchable knowledge. List available wikis with:

```bash
wiki list
wiki info <wiki-id>
```

Search or read one:

```bash
wiki search "query" --prefix <wiki-id-or-path>
wiki brief "query" --prefix <wiki-id-or-path>
wiki read <wiki-id/path.md>
```

Create a new knowledge collection only when a separate long-term subject really benefits from one:

```bash
wiki db init <wiki-id> --title "Readable title"
```

Use the person's `personal` wiki for personal memory instead of creating private memory for every work identity.

## Ship Manual

`gsv-manual` is the reference for using Ship. Its local copy updates automatically
when the installed Gateway selects a newer compatible Manual revision. An older
Gateway does not follow the Manual's latest development branch.

```bash
wiki info gsv-manual
wiki refresh gsv-manual
```

`wiki info` shows the last synchronization outcome and observed revision.
`wiki refresh` retries immediately when your capabilities permit it; it does not
change account skills. A failed update leaves the installed copy available, and
Ship retries on later activity. `diverged` means local edits were preserved rather
than replaced. Inspect those edits with the owner before changing them.

## Ship Repositories

The `rgit` command works with repositories stored by Ship. It can list repositories, inspect files and history, search, compare revisions, show commit diffs, import content, and pull updates.

Start with:

```bash
rgit list
rgit info <repo>
rgit refs <repo>
rgit log <repo> --limit 1
rgit diff <repo> <commit>
```

Edit files under `/src/repos/OWNER/REPO` with ordinary file tools. Writable
filesystem operations commit immediately; there is no separate `rgit commit`
step. `rgit log` returns full commit hashes. Read the relevant files and history
first, and preserve unrelated user changes. Use `rgit --help` for current import
and pull syntax.

Keep source for a [published website or game](publish-site.md) in a repository.
`sites init` creates the starter there and `sites publish` records the exact
source commit with each release. A build computer's temporary disk is not a
durable source repository.

## Source References

Wiki pages can record the target and path of source material so knowledge remains traceable without copying an entire source document into the page:

```bash
wiki source add <wiki-id/path.md> --source <target:/path::title>
```

References identify the source; they do not grant access to it.
