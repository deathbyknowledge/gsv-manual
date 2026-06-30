# Operating Model

[Advanced System Internals](index.md)

GSV is an OS-shaped cloud computer. The user-facing concepts are apps, files, agents, devices, settings, integrations, and packages. The implementation maps those concepts onto workers, durable runtime state, package source, and connected targets.

## Control Plane

The gateway is the control plane. It handles identity, auth, package management, adapter routing, inference routing, process lifecycle, and system configuration.

Source area:

- `gateway/src/kernel/*`
- `gateway/src/syscalls/*`
- `gateway/src/inference/*`
- `gateway/src/fs/*`

## Durable Agent Runtime

Processes are durable agent runtimes. They hold conversation history, queued input, active runs, pending tool calls, media references, checkpoints, and archives.

Source area:

- `gateway/src/process/do.ts`
- `gateway/src/process/store.ts`
- `gateway/src/process/checkpoint.ts`
- `gateway/src/process/media.ts`

## Web Shell, Native Surfaces, And Apps

The web shell hosts the desktop and most first-party user work surfaces directly. Chat, Files, Terminal, Library, Repositories, Settings, Crew, Runtime/Tasks, Machines, Messengers, Integrations, and Applications are implemented under `web/src/app/features/*`.

Installable package apps still open inside the desktop through package app frames. The host bridge gives those package frames shell-owned app sessions, backend RPC, status/title/dirty-state integration, and constrained access to granted syscalls.

Source area:

- `web/src/app/App.tsx`
- `web/src/app/features/desktop/*`
- `web/src/app/features/gsv-shell/*`
- `web/src/app/features/gsv-console/*`
- `web/src/app/features/chat/*`
- `web/src/app/features/files/*`
- `web/src/app/features/terminal/*`
- `web/src/app/features/repositories/*`
- `web/src/app/features/apps/components/AppFramePage.tsx`
- `web/src/app/features/desktop/runtime/host/hostBridge.ts`

## Targets

Only target-routed file and shell work should move to devices, browser targets, or adapter targets. Control-plane domains remain gateway-facing. When debugging, separate "where the command ran" from "which control-plane operation authorized it."

## Advanced Agent Note

When implementation behavior and the visible system disagree, identify the source of truth first: live runtime state, package source, deployed worker code, local CLI config, a device target, or the repository.
