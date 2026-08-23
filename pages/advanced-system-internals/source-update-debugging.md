# Source, Deployment & Debugging

[System Internals](index.md)

## Source Map

- `gateway/`: Kernel, Process, Conversations, syscalls, routing, inference client, filesystem.
- `packages/gsv/`: public TypeScript client and protocol.
- `web/`: Web shell and browser-side Gateway integration.
- `host/`: Cargo workspace containing Desktop, CLI, daemon, helpers, and shared host protocols.
- `adapters/`: Telegram, WhatsApp, Discord, email, test, and shared adapter code.
- `accounts/`: managed installation directory, onboarding, and operator APIs.
- `inference/`: managed inference and mail-summary service.
- `extension/`: browser target.
- `docs/` and `engineering/`: developer/product source documentation.
- `../gsv-manual/`: this built-in human/agent manual.
- `../infrastructure/`: managed deployment graph, environment configuration, and operator guide.

## Validation By Boundary

Run the smallest relevant set, plus each real protocol consumer:

```text
Gateway:        cd gateway && npx tsc --noEmit && npm run test:run
Web:            cd web && npm run check && npm run test:run && npm run build
SDK:            npm run gsv:check && npm test --workspace packages/gsv
Host:           cd host && cargo fmt --all -- --check && cargo test --workspace
Accounts:       cd accounts && npm run typecheck && npm test
Inference:      cd inference && npm run typecheck && npm test
Adapter:        cd adapters/<name> && run its typecheck/tests
Extension:      cd extension && npm run check && npm run test:run && npm run build
```

Run `npm run lint` and `npm run protocol:check` at the repository root. Protocol changes often affect
Gateway, SDK, Web, Desktop/CLI, and adapters even if only one public type changed.

## Deployment Boundaries

A Gateway deploy updates Kernel/Process code and serves the currently built `web/dist`. It does not
update adapter Workers, Accounts, Inference, host binaries, or the extension. Deploy those through
their own release paths.

Managed infrastructure composes all Workers and bindings but still preserves their independent state
and migrations. Standalone deploys omit managed Accounts/Inference/email resources and must retain
the `singleton` Durable Object projection for upgrades.

## Debugging Ownership

- Login/installation hostname: Web, Gateway ingress, Accounts directory, and Access configuration.
- Canonical message missing: Conversation admission/commit and exact endpoint route.
- Reasoning/tool activity missing: Process observation and Process history.
- Provider generation: Process inference client, managed Inference/provider, streaming cancellation.
- External delivery: adapter ledger and provider state.
- File/media failure: resource reference, exact revision, transfer body, target/R2 owner.
- Machine command: Kernel target route, driver connection, `gsvd`, and local OS.

## Source Of Truth

A local branch, managed infrastructure gitlink, deployed Worker version, Durable Object migration
ledger, adapter provider state, and client binary can all differ. Record exact revisions and
environment before concluding that source behavior is deployed.

## For Agents

Preserve unrelated dirty changes. Commit logical batches with short imperative subjects, and never
deploy merely because local tests passed unless the user authorized deployment.
