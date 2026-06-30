# Source Maps, Updates & Debugging

[Advanced System Internals](index.md)

Use this page when changing GSV itself or debugging which layer owns a behavior.

## Source Map

- Gateway control plane: `gateway/src/*`
- Process runtime: `gateway/src/process/*`
- Syscall surface: `gateway/src/syscalls/*`
- Web shell and native UI surfaces: `web/src/*` and `web/public/*`
- Package runtime and installable package source: `gateway/src/app-runner/*`, `packages/gsv/*`, and source repositories under `/src/repos/<owner>/<repo>`
- Adapter workers: `adapters/whatsapp/*`, `adapters/discord/*`, and `adapters/test/*`
- CLI: `cli/*`
- ripgit: `ripgit/*`
- Shared contracts: `shared/*`
- Product and design references: `docs/*` and `engineering/*`
- Shipped manual content: `root/gsv-manual`

Visible repositories are mounted read-first at `/src/repos/<owner>/<repo>`. Writable repository and package-source edits stage into a process-local overlay until `rgit commit` or `rgit discard`. Use `pkg source <package>` to find a package's source repo path, and `pkg update <package> --ref <ref>` after committing source that should affect the installed package.

## Update Paths

- Gateway changes: `cd gateway && npm run deploy`
- Gateway local validation: `cd gateway && npx tsc --noEmit && npm run test:run`
- Web shell changes: `cd web && npm run check && npm run build`
- Package source changes: `rgit diff owner/repo`, `rgit commit owner/repo --message "..."`, then `pkg update <package> --ref <ref>` or `gsv packages sync <package> [--ref REF]`.
- WhatsApp adapter changes: `cd adapters/whatsapp && npx tsc --noEmit`
- Discord adapter changes: `cd adapters/discord && npm run typecheck`
- Test adapter changes: `cd adapters/test && npm run typecheck`
- CLI changes: `cd cli && cargo test && cargo fmt --check`

## Debugging Boundaries

Check the surface that owns the problem:

- Login, desktop windows, previews, or browser target: web shell.
- Chat dock, Files, Terminal, Library, Repositories, Settings, Crew, Runtime/Tasks, Machines, Messengers, Integrations, or Applications pages: web shell.
- Conversation history, queued input, tool approvals, media, or abort/reset behavior: process runtime.
- Package install, enablement, trust, or source workflow: package system.
- Package app UI behavior: the owning package app and the host bridge.
- External platform behavior: the specific adapter worker.
- Filesystem or command location confusion: target routing and devices.
- Knowledge search or Library editing: web shell Library plus repository-backed knowledge storage.

## Source Of Truth

Do not assume the repository, deployed worker, installed package, and live runtime state are identical. A debugging note should say which one was inspected.
