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

## GSV Repositories

The `rgit` command works with repositories stored by GSV. It can list repositories, inspect files and history, search, compare revisions, show status and diffs, commit changes, import content, and pull updates.

Start with:

```bash
rgit list
rgit info <repo>
rgit status <repo>
rgit diff <repo>
rgit log <repo>
```

Use `rgit --help` for exact syntax before a write, discard, import, or commit. Read the relevant files and diff first. A repository operation should preserve unrelated user changes.

## Source References

Wiki pages can record the target and path of source material so knowledge remains traceable without copying an entire source document into the page:

```bash
wiki source add <wiki-id/path.md> --source <target:/path::title>
```

References identify the source; they do not grant access to it.
