# Advanced System Internals

[Back to GSV Manual](../../index.md)

This section is for operators, developers, and agents that need implementation details. It is intentionally separate from the everyday manual.

Use these pages when you need to debug source-of-truth questions, inspect code paths, validate a deployment, understand runtime components, or change GSV itself.

## Pages In This Section

- [Operating Model](operating-model.md)
- [Source Maps, Updates & Debugging](source-update-debugging.md)
- [Schema & Migration Guidance](schema-migrations.md)

## User-Level Warning

Most user tasks should not start here. If the question is "how do I use GSV?", go back to the everyday sections. If the question is "where is this implemented, how do I update it, or what validates it?", this section is the right place.

## Main Runtime Pieces

- Gateway worker: control plane, auth, packages, adapters, inference, and routing.
- Process runtime: durable agent conversations, queues, tool calls, media, and checkpoints.
- Web shell: setup/login, desktop, native Chat/Files/Terminal/Library/Repositories/Settings/Crew/Runtime/Inventory surfaces, and package app host bridge.
- Package runtime: installable package apps, package commands, package agents, backend RPC, public routes, and package-scoped storage.
- Adapter workers: external platform connections such as WhatsApp and Discord.
- CLI: device, deployment, administration, and package sync commands.
- ripgit: git-backed storage and content operations.
