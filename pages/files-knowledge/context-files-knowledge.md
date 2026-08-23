# Context, Skills & Knowledge

[Files, Resources & Knowledge](index.md)

## Quick Map

| Need | Use |
| --- | --- |
| Durable identity, preferences, constraints, commitments | `context.d` |
| A reusable procedure an agent should load for a task | `skills.d` |
| Documents, code, data, and deliverables | ordinary files/repositories |
| What people deliberately said | Conversations |
| Reasoning, drafts, tools, retries, and run state | Process activity |

## Context Files

System context lives in `config/ai/context.d/*.md`. Account context lives in
`~/context.d/*.md`. Files are composed in lexical order and cached for the active run.

Keep context concise and durable. Good context states who the agent is, how the user prefers to work,
which commitments persist, and which constraints always apply. Do not use it as a log, dump tool
documentation into it, or copy transient conversation details there.

Repository-defined prompt and seeded context text is owned by the Gateway prompt sources. Runtime,
protocol, routing, or UI bugs must be fixed in code rather than papered over with prompt edits.

## Skills

Skills are task-specific instructions under layered `skills.d` directories. The standing prompt
contains only a compact index. An agent reads the selected `SKILL.md` when needed, which saves context
and keeps procedures independently maintainable.

Use a skill for repeatable workflows, external-system procedures, or specialized rules. Use context
for behavior that should apply across tasks.

## Files And Reference Knowledge

Use ordinary files for source material and artifacts. Search before reading large collections, then
read only relevant ranges. Use immutable resource references when a Message or history entry must
continue to identify exact media bytes after the path changes.

## Conversations And Memory

Conversation history is a record, not automatically standing context. Personal may choose to record
a durable preference or commitment in account files; it should not assume every old Message belongs
in every future prompt.

## For Agents

Prefer the smallest durable representation. Update context only when the user intends a standing
change. Preserve unrelated context and skill files, and never overwrite them merely to complete a
one-off task.
