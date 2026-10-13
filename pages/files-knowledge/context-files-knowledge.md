# Memory, Context, And Skills

[Files, Memory, And Skills](index.md)

These mechanisms answer different questions:

| Need | Put it here |
| --- | --- |
| “This fact may matter again; retrieve it when relevant.” | personal wiki |
| “This preference must affect nearly every request.” | personal context |
| “This unfinished outcome needs follow-through.” | responsibility ledger (`r12y`) |
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

Files in `context.d` are loaded automatically. Use them for concise identity, preferences, constraints, and voice that should remain visible without a search. Keep unfinished commitments in `r12y`.

Account context lives under `~/context.d/`. Shared personal context belongs to the person and is available to owned work. Context files are ordered by filename.

Ship's voice lives in its own `~/context.d/05-voice.md`; Crew's execution guidance lives in Crew's separate home. Put shared preferences in the human owner's `context.d/10-personal.md`.

Onboarding is not a context file. While a person is new, Ship's ledger holds
one system responsibility, `onboarding.initial`, titled "Welcome to gsv",
whose details are rendered in Ship's standing context. The shared
responsibilities context puts it first: Ship follows those instructions to get
to know the person and complete one small task with them, parks or delegates
other work meanwhile, and resolves it once the acceptance criteria are met. Confirmed facts learned
along the way go in the person's `context.d/10-personal.md`.

Standing context contains broadly applicable facts and instructions. Journals, detailed knowledge, tool instructions, and conversation history belong in the personal wiki or a skill and are retrieved when needed.

## Continuing Across Context Windows

Save useful knowledge as you learn it. The human's `context.d/10-personal.md`
stays loaded for Ship and owned workers; detailed knowledge remains searchable
in the personal wiki. A history handover is working context, not another memory
store. Keep commitments in `r12y` and artifacts in files.

When the runtime requests a handover, update those stores and submit:

```bash
proc compact --summary 'The user corrected the deadline to Friday. The report is in /report.md; verify its citations next.'
```

This saves your handover for installation after the current tools finish. Your
original request, unseen tool results and recent original exchanges remain
intact; continue the same work. The runtime targets 40% of the usable input
budget by default, including standing instructions, tools and the handover.
History that already fits stays unchanged.
New input or cancellation may supersede the pending handover. No new process or
responsibility is needed just to compact. Exact evidence stays available through
`proc segments` and `proc segment ID`.

Ship carries ongoing topics, decisions and unanswered questions across context
windows. A worker carries its assignment, constraints, verified findings and next
steps. Neither restarts completed onboarding or treats compaction as completing
work. Avoid copying transcripts, standing context or the responsibility ledger
into the handover.

Newly archived Ship history can also create a memory-review responsibility. Ship
delegates that bounded slice while continuing to respond to the user. Read its
`archivePath` with `proc history --archive PATH --generation N
--after-message-id N --through-message-id N --limit 10 --full` on `gsv`, using
the supplied generation and original message ID range. Continue with `--offset`
set to `next_offset` until `has_more=false`, reducing the page size if output is
truncated. This streams the archive and remains available after the source
Process is replaced.
Read current memory first, merge only useful new information with revision-checked
repository writes, and resolve the responsibility after the whole slice has been
reviewed and any writes have succeeded. A review may correctly make no changes.
If it fails, retain the blocker instead of marking the slice reviewed. These
reviews are serialized per owner; `memory.review` in responsibility sources
controls whether new reviews are admitted.

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
