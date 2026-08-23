# Schema & Migration Guidance

[System Internals](index.md)

## Migration Owners

- Accounts D1: `accounts/migrations/`
- Kernel Durable Object SQLite: `gateway/src/kernel/schema/`
- Process Durable Object SQLite: `gateway/src/process/schema/`
- Conversation Durable Object SQLite: `gateway/src/conversation/schema/`
- Shared DO migration runner: `gateway/src/schema/runner.ts`
- Managed Inference Durable Object SQLite: `inference/src/schema/`
- ripgit: its Rust schema owner

## Rules

- Never edit a migration that may have shipped.
- Add the next numbered migration in the owning store.
- Do not create tables/indexes or `ensureColumn` repairs from store constructors.
- Preserve supported standalone and managed upgrade paths in tests.
- Migration IDs, names, and checksums are part of deployed state. Reusing an ID for a different
  migration breaks startup even if the SQL happens to be compatible.
- Collapse to a new baseline only for an explicit release/reset policy.

Managed and standalone may share runtime code while applying different surrounding services. A
managed migration number already deployed for mail or installation state cannot be renumbered to
make room for another branch.

## Validation

Test a fresh database, the oldest supported upgrade, and any historic ledger edge the release policy
claims to support. Cross-boundary lifecycle changes also need clean-instance runtime tests; a schema
unit test alone cannot prove that Process, Kernel, adapter, and client state agree.

## For Agents

Before editing, identify the physical store, current migration sequence, deployed environments, and
support policy. If any are unknown, investigate rather than adding runtime repair code.
