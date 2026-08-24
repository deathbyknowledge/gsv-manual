# GSV Manual

This is the operating manual for GSV and the person using it. It explains what GSV can do, how to do it, what to inspect when something goes wrong, and which actions need permission.

Start with the outcome you want. Each section begins with common actions and leads to exact commands, permissions, and recovery.

## Start Here

- [Meet GSV](pages/orientation.md)
- [Talk with GSV and manage work](pages/agents-assistants/index.md)
- [Work with files, memory, and skills](pages/files-knowledge/index.md)
- [Use your computers and browser](pages/devices-workplaces/index.md)
- [Use messaging, email, and connected services](pages/integrations/index.md)
- [Schedule and delegate work](pages/automation/index.md)
- [Manage accounts and permissions](pages/accounts-access/index.md)
- [Change settings and recover from problems](pages/settings/index.md)
- [Use the Web and Desktop apps](pages/apps-desktop/index.md)
- [Find any command or capability](pages/reference/index.md)

## I Want To…

| Goal | Go here |
| --- | --- |
| Ask GSV something or continue a conversation | [Ship, messages, and work](pages/agents-assistants/index.md) |
| See what GSV is thinking or doing | [Messages and activity](pages/agents-assistants/conversations-delegation.md) |
| Send a reply, attachment, or message somewhere else | [Messaging and routing](pages/integrations/adapters-routing.md) |
| Read, edit, find, copy, or preserve a file | [Files and exact revisions](pages/files-knowledge/home-wiki-knowledge.md) |
| Remember something or create a reusable procedure | [Memory, context, and skills](pages/files-knowledge/context-files-knowledge.md) |
| Run something on a laptop, server, or browser | [Computers and targets](pages/devices-workplaces/targets-copy.md) |
| Connect Telegram, WhatsApp, Discord, email, MCP, or OAuth | [Connected services](pages/integrations/index.md) |
| Set a reminder or recurring job | [Schedules and automation](pages/automation/index.md) |
| Create, inspect, reset, or stop a piece of work | [Work controls](pages/agents-assistants/conversations-delegation.md) |
| Read an image, transcribe audio, or create media | [Media tools](pages/files-knowledge/media.md) |
| Run shell commands, HTTP requests, or a composed workflow | [Shell, CodeMode, and network](pages/reference/shell-codemode-network.md) |
| Diagnose a failure | [Troubleshooting](pages/reference/troubleshooting.md) |

## When GSV Needs To Discover How

Search this manual for product workflows:

```bash
wiki search "what you need to do" --prefix gsv-manual
wiki info gsv-manual
```

Search the capabilities available in the current GSV:

```bash
man --search -- "plain-language goal"
man <command>
```

The live search includes commands, connected computers, installed skills, and ready integrations. Results also say when a capability exists but is unavailable to the current identity.

## Four Useful Ideas

- **Ship** is the main conversation with GSV.
- **Work** is a task with its own activity and controls. Open it to inspect or intervene.
- **Messages** are what was deliberately sent. **Activity** shows the reasoning, tools, retries, and errors behind the work.
- A **target** is a place where an action can run, such as GSV itself, a connected computer, or a browser.
