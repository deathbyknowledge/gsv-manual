# Meet Ship

[Back to the manual](../index.md)

Ship is your personal spaceship. It stays in orbit while you live your life down here on Earth. You can talk to your Ship, give it work, and keep your files and projects aboard. It uses the technology you connect to it and keeps work running while you are away.

A computer, browser, phone, server, messenger, repository, service, or piece of hardware can become part of that system. Each can provide a place to reach Ship, something Ship can use, or both. The system grows by capability, so specialized technology can join alongside familiar apps and devices.

Your Ship can also connect directly with another person's Ship. Each Ship stays
sovereign while the two exchange messages, requests, and exact file revisions.

Your Ship has an email address of its own, so sign-ups, receipts, tracking and
bills can go to it instead of your personal inbox.

Ship carries identity, memory, permissions, conversation, and ongoing work across those places. Begin in Web, continue through a messenger, inspect work from Desktop, and let that work use a connected computer or service. You decide what joins the system and what it may expose.

Models and specialized agents can contribute to the work. Ship is the continuing whole that coordinates them and remains yours.

## Your Ship

Ship names your continuing relationship with the personal intelligence. The Web app, Desktop app, and linked private messengers all open that same Ship.

The Web app is called **Instrument**. It has five views: **Chat** is Ship and the activity behind each reply, with contextual responsibilities and routines; **Fleet** lists your places and processes, with files opened from a place; **Memory** shows your personal knowledge pages; **People** holds conversations and contacts across Ship spaces; **Settings** holds preferences, standing responsibilities, permissions, instructions, messengers, MCP connections, and Logs.

Ship may do work in separate work sessions, but results return through the same personal intelligence unless you deliberately open a direct work session.

## Messages And Activity

Ship separates two things that are useful for different reasons:

- **Messages** are what you or Ship deliberately sent in the conversation.
- **Activity** is how a piece of work happened: reasoning, drafts, commands, tools, approvals, retries, and errors.

Use Messages for the conversation. Open a work item's Activity when you want to inspect, debug, approve, interrupt, or understand how something was done.

## Work You Can See And Control

Ship can hand off parts of a request or keep longer tasks separate so Ship remains responsive. The **Processes** block in Fleet shows those tasks and lets you inspect, reset, stop, or open one directly.

Sent messages remain in the conversation when work stops. Returning to Ship leaves other work running; Abort, Reset, and Kill provide explicit lifecycle controls.

## How Technology Joins Ship

Connected technology contributes one or more roles:

- a **surface** where you and Ship exchange messages;
- a **target** where Ship can use files, commands, networks, software, or hardware;
- a **service** that contributes an account or specialized capability.

A messenger can be a surface, a laptop can be a target, and a browser or Desktop app can contribute more than one role. Ship combines their capabilities while preserving the identity and permission of every action.

Ship discovers available targets and integrations before acting:

```bash
targets list
mcp list
oauth list
```

## Permission Is Part Of The Action

Every action is authorized against the signed-in account, connected target, file ownership, capabilities, and approval rules. When authority or confirmation is missing, Ship reports that exact requirement and keeps the requested destination unchanged.

## Find The Next Step

For an unfamiliar request, start from the outcome:

```bash
man --search -- "send a photo"
wiki search "connect telegram" --prefix gsv-manual
```

Use the section navigation in the [manual index](../index.md) when browsing as a person.

## Ship And The GSV Runtime

Ship is the product name. GSV remains the runtime name and appears in the `gsv`
target, protocol and package identifiers, and `.gsv` folders. The external CLI
command remains `gsv`.
Do not rename user files, histories, targets, settings, services or stored paths
to match the product name. Internal shell commands are unchanged.

Operators configure the default domain for handles and may retain older domains
as aliases. An alias reaches the same installation and does not create a new
Ship or federation identity. Use the addresses actually configured by the
operator. Opening a new browser origin may require signing in again.
