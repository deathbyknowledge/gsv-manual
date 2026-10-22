# Files, Paths, Copies, And Exact Revisions

[Files, Memory, And Skills](index.md)

## Everyday File Work

Ship can read, search, create, edit, and delete files it is authorized to access. Use the dedicated file tools for direct work. Shell also provides familiar discovery and copy commands:

```bash
ls /path
stat /path/to/file
cp source destination
```

Read returns a bounded amount by default so one large file cannot consume an entire request. Continue with an offset and limit when more is needed. Search first when only a small part of a large collection matters.

## Home

`~` means the home of the account performing the work. Home commonly contains:

- `~/context.d/` for small standing context;
- `~/skills.d/` for reusable procedures;
- user-created files and project material;
- retained resources associated with past work.

The current working directory can be elsewhere without changing what `~` means.

## The Public Folder

Every Ship has a `/public` folder. Anything saved there is readable by anyone on
the internet, without signing in, at `https://YOUR-SPACE/public/PATH`. The path
after `/public/` is the file's path inside the folder, so `/public/reports/q3.pdf`
is available at `https://YOUR-SPACE/public/reports/q3.pdf`.

Use it to share a document, image, export, or plain page with someone who does
not use Ship. Ship, Crew, and the person can all create files there:

```bash
cp ~/exports/report.pdf /public/report.pdf
```

Then share the link. Replace the file at the same path to update it; readers
may see the previous version for up to five minutes.

A file can be replaced or deleted only by the account that created it, or by
root. Deleting the file is the only way to stop sharing it, and copies that were
already downloaded cannot be recalled. Keep private data, credentials, and
anything the person has not agreed to share out of this folder.

HTML and SVG files are served without scripts, so the folder suits documents and
static pages rather than apps. `/public/gsv/assets/` holds Ship's own branding;
leave it alone.

## Files On Another Computer

Prefix a path with a target ID to address an authorized connected computer or browser target:

```bash
cp laptop:/Users/sam/Desktop/photo.jpg ~/photos/photo.jpg
cp ~/exports/report.pdf laptop:/Users/sam/Downloads/report.pdf
```

If the target ID contains a colon, wrap it in brackets:

```bash
cp [browser:work]:/downloads/invoice.pdf ~/invoices/invoice.pdf
```

Use `targets list` and `targets show <id>` to find the right destination. An offline target remains selected until the user chooses another.

## Why Exact Revisions Matter

A path can change. When a message or activity record must continue to mean the exact file used at that moment, Ship stores a reference containing the target, path, exact revision, content type, and size.

For example:

1. Ship reads `proposal.md`.
2. Ship edits `proposal.md`.
3. Ship reads it again.

The two reads refer to different revisions even though the path is identical. Inspecting the earlier activity must still resolve the earlier content.

Messages store references to exact bytes. Resolving a reference rechecks ownership and permission. If that revision is unavailable, Ship returns an exact-revision error while leaving newer bytes at the same path untouched.

## Copy Versus Reference

- Copy when another saved file should exist at the destination.
- Keep an exact reference when a consumer only needs to retrieve the same bytes later.

Before committing an attachment or work record whose original source may disappear, Ship preserves the exact referenced revision.
