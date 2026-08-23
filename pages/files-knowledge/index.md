# Files, Resources & Knowledge

[Back to GSV Manual](../../index.md)

GSV uses ordinary files for artifacts and standing knowledge, immutable resource references for
durable media, and Process/Conversation records for interaction state.

## Choose The Right Place

- Put documents, code, exports, and project artifacts in files.
- Put durable identity and preferences in `context.d`.
- Put reusable operating procedures in `skills.d`.
- Put reference material in an appropriate file or repository and search it when needed.
- Let Conversations retain what users deliberately said.
- Let Process activity retain how a run happened.

## Files And Revisions

Filesystem targets expose the same `fs.*` and transfer primitives through the Gateway or a connected
machine. Exact revisions let a transcript refer to old bytes even after the visible path changes.
Binary bodies stream separately from structured protocol metadata.

## Pages In This Section

- [Home Files, Immutable Resources & Search](home-wiki-knowledge.md)
- [Context, Skills & Knowledge](context-files-knowledge.md)

## For Agents

Do not paste large or binary content into messages when a resource reference or file path is enough.
Resolve bytes only for the consumer that actually needs them.
