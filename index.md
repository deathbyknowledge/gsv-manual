# GSV Manual

GSV is a user-owned personal intelligence operating environment. You interact with one Personal
intelligence while GSV runs inspectable Processes, reaches connected machines, and talks through
the Web, Desktop, CLI, and messaging adapters.

This manual is for both people and agents. It describes the product that exists now. When a page
mentions planned architecture, it says so explicitly.

## Start Here

1. [Orientation](pages/orientation.md)
2. [Personal Intelligence & Work](pages/agents-assistants/index.md)
3. [Files, Resources & Knowledge](pages/files-knowledge/index.md)
4. [Web & Desktop](pages/apps-desktop/index.md)
5. [Machines & Targets](pages/devices-workplaces/index.md)
6. [Accounts & Access](pages/accounts-access/index.md)
7. [Settings](pages/settings/index.md)
8. [Messaging, Email & Integrations](pages/integrations/index.md)
9. [Automation & Delegation](pages/automation/index.md)
10. [Clients, Adapters & Extensions](pages/packages-extensions/index.md)
11. [System Internals](pages/advanced-system-internals/index.md)

## Everyday Map

- Open **Chat** to speak with your Personal intelligence.
- Open **Work** to inspect and control the Processes doing its work. Entering a Work Session does
  not replace your Personal intelligence.
- Open **Messages** for the durable stream of user-visible messages across Web, Desktop, and linked
  private messengers. Open **Process activity** when you want reasoning, drafts, tool calls, results,
  retries, or errors.
- Open **Machines** to connect a computer and make its filesystem, shell, and network available as a
  target.
- Open **Messengers** to link Telegram, WhatsApp, or Discord. Private messages normally reach
  Personal Home.
- Use **Integrations** for MCP servers and OAuth-backed external services.
- Use `gsv` for administration and scripting, and `gsvd` to expose a machine as a target.

## The Three Records To Keep Straight

- A **Conversation** stores what people and the Personal intelligence deliberately said to each
  other. It survives Process replacement and deletion.
- A **Process** stores how work happened: inputs, reasoning, model output, tools, approvals, queues,
  and lifecycle state.
- A **resource reference** identifies an exact immutable file revision. Messages and histories keep
  the reference; bytes move only when a model, client, or adapter resolves it.

## For Agents

Use the manual as product guidance, not as authorization. Runtime capabilities, ownership checks,
and approval rules remain authoritative. Do not infer secrets, user identities, filesystem access,
or delivery authority from prose, labels, paths, message IDs, or resource references.
