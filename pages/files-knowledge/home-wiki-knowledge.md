# Files, Paths, Copies, And Exact Revisions

[Files, Memory, And Skills](index.md)

## Everyday File Work

GSV can read, search, create, edit, and delete files it is authorized to access. Use the dedicated file tools for direct work. Shell also provides familiar discovery and copy commands:

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

A path can change. When a message or activity record must continue to mean the exact file used at that moment, GSV stores a reference containing the target, path, exact revision, content type, and size.

For example:

1. GSV reads `proposal.md`.
2. GSV edits `proposal.md`.
3. GSV reads it again.

The two reads refer to different revisions even though the path is identical. Inspecting the earlier activity must still resolve the earlier content.

Messages store references to exact bytes. Resolving a reference rechecks ownership and permission. If that revision is unavailable, GSV returns an exact-revision error while leaving newer bytes at the same path untouched.

## Copy Versus Reference

- Copy when another saved file should exist at the destination.
- Keep an exact reference when a consumer only needs to retrieve the same bytes later.

Before committing an attachment or work record whose original source may disappear, GSV preserves the exact referenced revision.
