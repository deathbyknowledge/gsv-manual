# Meet GSV

[Back to the manual](../index.md)

GSV is a personal intelligence operating system: one continuing intelligence across all the technology you choose to connect.

A computer, browser, phone, server, messenger, repository, service, or piece of hardware can become part of that system. Each can provide a place to reach GSV, something GSV can use, or both. The system grows by capability, so specialized technology can join alongside familiar apps and devices.

GSV carries identity, memory, permissions, conversation, and ongoing work across those places. Begin in Web, continue through a messenger, inspect work from Desktop, and let that work use a connected computer or service. You decide what joins the system and what it may expose.

Models and specialized agents can contribute to the work. GSV is the continuing whole that coordinates them and remains yours.

## Your Ship

Ship names your continuing relationship with the personal intelligence. The Web app, Desktop app, and linked private messengers all open that same Ship.

GSV may do work in separate work sessions, but results return through the same personal intelligence unless you deliberately open a direct work session.

## Messages And Activity

GSV separates two things that are useful for different reasons:

- **Messages** are what you or GSV deliberately sent in the conversation.
- **Activity** is how a piece of work happened: reasoning, drafts, commands, tools, approvals, retries, and errors.

Use Messages for the conversation. Open a work item's Activity when you want to inspect, debug, approve, interrupt, or understand how something was done.

## Work You Can See And Control

GSV can hand off parts of a request or keep longer tasks separate so Ship remains responsive. The Work area shows those tasks and lets you inspect, reset, stop, or open one directly.

Sent messages remain in the conversation when work stops. Returning to Ship leaves other work running; Abort, Reset, and Kill provide explicit lifecycle controls.

## How Technology Joins GSV

Connected technology contributes one or more roles:

- a **surface** where you and GSV exchange messages;
- a **target** where GSV can use files, commands, networks, software, or hardware;
- a **service** that contributes an account or specialized capability.

A messenger can be a surface, a laptop can be a target, and a browser or Desktop app can contribute more than one role. GSV combines their capabilities while preserving the identity and permission of every action.

GSV discovers available targets and integrations before acting:

```bash
targets list
mcp list
oauth list
```

## Permission Is Part Of The Action

Every action is authorized against the signed-in account, connected target, file ownership, capabilities, and approval rules. When authority or confirmation is missing, GSV reports that exact requirement and keeps the requested destination unchanged.

## Find The Next Step

For an unfamiliar request, start from the outcome:

```bash
man --search -- "send a photo"
wiki search "connect telegram" --prefix gsv-manual
```

Use the section navigation in the [manual index](../index.md) when browsing as a person.
