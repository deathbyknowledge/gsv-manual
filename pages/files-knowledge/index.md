# Files & Knowledge

[Back to GSV Manual](../../index.md)

Files and knowledge are where GSV keeps durable material. Conversations are useful for doing work, but files, Wiki pages, standing context, and reusable skills are where important results should land.

## Main Places

- `/home` is the ordinary home area for users, agents, documents, project folders, and durable artifacts.
- Files is the app for browsing, opening, editing, and organizing files.
- Wiki is the app for structured knowledge bases, manuals, notes, imports, durable references, and search.
- `~/context.d/` stores short standing instructions for an account or agent.
- `~/skills.d/` stores reusable procedures that agents can open when a task calls for them.
- Knowledge bases are collections of material that people and agents can search, browse, and cite when needed.

## What Belongs Where

- Use context for short, stable instructions that should shape an agent's behavior.
- Use skills for repeatable procedures, command sequences, and task-specific guardrails.
- Use Wiki for durable reference material that should be searchable.
- Use Files for artifacts, documents, project data, scripts, and anything the user should directly manage.
- Use conversations for current work, decisions in progress, and task coordination.
- Use package source for code or assets that belong to an installed package.

## Pages In This Section

- [Home Files, Wiki & Knowledge Bases](home-wiki-knowledge.md)
- [Context, Skills & Knowledge Boundaries](context-files-knowledge.md)

## For Agents

When a user says "remember this", clarify whether it should become standing context, a reusable skill, a Wiki note, or a file. Hidden memory is not the preferred durable record in GSV; user-visible storage is.
