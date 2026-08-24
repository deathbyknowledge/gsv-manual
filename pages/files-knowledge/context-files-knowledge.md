# Memory, Context, And Skills

[Files, Memory, And Skills](index.md)

These mechanisms answer different questions:

| Need | Put it here |
| --- | --- |
| “This fact may matter again; retrieve it when relevant.” | personal wiki |
| “This preference or commitment must affect nearly every request.” | personal context |
| “Use these instructions whenever doing this kind of task.” | a skill |
| “This is source material or a deliverable.” | an ordinary file |

## Personal Memory

Use the `personal` wiki for long-term, searchable facts, people, projects, decisions, preferences, routines, and dated events. Search it when personal history could change the answer:

```bash
wiki search "project atlas decision" --prefix personal
wiki info personal
wiki read personal/pages/projects/atlas.md
```

Personal memory contains concise, supported facts in the person's terms. It excludes raw transcripts, secrets, unsupported personality inferences, and routine actions. Replace information that has been corrected.

## Standing Context

Files in `context.d` are loaded automatically. Use them only for concise identity, preferences, constraints, voice, and open commitments that should remain visible without a search.

Account context lives under `~/context.d/`. Shared personal context belongs to the person and is available to owned work. Context files are ordered by filename.

Standing context contains only broadly applicable facts and commitments. Journals, detailed knowledge, tool instructions, and conversation history belong in the personal wiki or a skill and are retrieved when needed.

## Skills

Skills are reusable procedures loaded only for relevant work. The standing prompt contains a compact index; GSV reads the selected `SKILL.md` and any required supporting files before using it.

Useful commands:

```bash
skills list
skills search "workflow"
skills show <skill>
skills files <skill>
skills read <skill> <file>
skills create <name> --description "when to use it" --from /path/to/SKILL.md
skills validate <skill>
```

Use context for a rule that applies broadly. Use a skill for a repeatable workflow with a clear trigger.

## Updating Memory Safely

When a person explicitly asks GSV to remember or forget something, update the narrowest owning file or wiki page. Read before editing, preserve unrelated content, and report what changed without exposing private contents unnecessarily.
