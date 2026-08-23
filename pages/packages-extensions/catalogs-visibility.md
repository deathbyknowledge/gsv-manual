# Extensions Today & Roadmap

[Clients, Adapters & Extensions](index.md)

## What Exists Today

- Public TypeScript protocol/client types in `packages/gsv`.
- Rust host applications and shared protocol crates in `host/`.
- First-party adapter Workers under `adapters/`.
- A browser extension under `extension/`.
- MCP servers and OAuth accounts configured as integrations.
- Skills and context files that extend agent behavior without adding new model-facing tools.

## What Was Removed

The historical installable package runtime, framed package apps, catalogs, remotes, package agents,
and public package routes were removed. Old manual pages and commands describing them are not valid
for current GSV.

## What Is Planned

Protocol-peer unification may eventually let authenticated participants negotiate facilities such as
syscall access, interactive input, directed output, signals, or target execution. The design must
keep principal, transport, and facilities independent and attenuate external-user authority.

An entitlements service is also planned for managed product limits such as inference and email. Its
records are expected to be simple typed-by-caller keys such as `inference.credits` or
`email.daily_messages`, cached by services for roughly 5–15 minutes. Enforcement and atomic usage
settlement still belong to the service that owns the scarce operation; the entitlement value is not
itself a quota counter or usage ledger.

Neither proposal should revive the old package system or add a second message model.

## For Agents

Describe an extension by the current boundary it uses: SDK client, host app, driver, adapter,
browser target, MCP integration, skill, or source contribution. Do not promise a catalog/install flow
that is not present.
