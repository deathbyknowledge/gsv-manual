# Home Files, Wiki & Knowledge Bases

[Files & Knowledge](index.md)

## Home Files

`/home` is the user's ordinary working area. It is the place for documents, downloads, notes, project folders, generated output, and files that should be easy to inspect later.

Use home files when:

- The user expects a normal file or folder.
- An artifact should be edited, downloaded, copied, or shared.
- A task produces a report, script, dataset, image, archive, or source file.
- An agent needs a stable path to continue work later.

Agents should avoid scattering files into unexpected locations. Prefer a clear project folder, a user-named path, or a path the user already gave.

Each account also has a small account-home overlay for standing agent context and reusable skills. The important user-facing folders are:

- `~/context.d/`: short standing context loaded into that account's agent prompt.
- `~/skills.d/`: reusable skills available to that account's agents.

For what to put in these folders and how agents should update them, see [Context, Skills & Knowledge Boundaries](context-files-knowledge.md).

Older profile-folder workflows have been replaced by real agent accounts and package profile agents. Do not use `~/profiles.d/` for new work.

## Wiki And Knowledge Bases

Wiki is for durable knowledge, not just file storage. A Wiki page should be useful when found later by search or browsing. It can hold manuals, operating notes, project background, imported reference material, summaries, and source references.

Use Wiki when:

- The information should be searchable by people and agents.
- The material explains how to do something.
- The user wants a knowledge base rather than one loose file.
- Several notes should be linked as a navigable set.
- An imported document should become reference material.

## Durable References

A durable reference is a stable pointer to material that should not depend on one conversation. It can be a Wiki page, a file path, a repository path, an external URL, or a package source location.

Good durable references are specific. "See the note in Wiki" is weaker than "See `gsv-manual/pages/files-knowledge/home-wiki-knowledge.md`".

## Search

Search works best when pages have clear titles, concise summaries, and terms a user would naturally search for. Avoid stuffing pages with raw logs or large unrelated dumps. Put raw material in files and summarize it in Wiki.
