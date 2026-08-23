# System Internals

[Back to GSV Manual](../../index.md)

This section is for developers and operators debugging implementation ownership, deployment state,
protocol behavior, migrations, and upgrades.

## Runtime Pieces

- **Gateway/Kernel:** auth, capabilities, config, routing, lifecycle, schedules, Conversations,
  adapter coordination, and inference coordination.
- **Process Durable Objects:** raw agent history, model loop, queues, tools, approvals, resources,
  cancellation, reset, and kill.
- **Conversation Durable Objects:** canonical user-visible Messages and archive segments.
- **Accounts:** managed installation directory, onboarding, lifecycle, and operator policy.
- **Inference:** managed provider credentials, routing, usage reservation, and settlement.
- **Adapters:** provider identity, transport, replay, media, and delivery.
- **Web/host clients:** user presentation and local machine integration.

## Pages In This Section

- [Operating Model](operating-model.md)
- [Source, Deployment & Debugging](source-update-debugging.md)
- [Schema & Migration Guidance](schema-migrations.md)

## For Agents

Say whether evidence came from source, tests, local state, deployed Workers, Durable Object data, or
provider state. Those are not interchangeable sources of truth.
