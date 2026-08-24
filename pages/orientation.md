# Meet GSV

[Back to the manual](../index.md)

GSV gives you one personal intelligence that can hold a conversation, work with files, use connected computers and services, remember what matters, and keep longer work visible while you continue talking.

## Your Home Conversation

Home is the ordinary place to talk with GSV. The Web app, Desktop app, and linked private messengers all continue the same relationship with the same personal intelligence.

GSV may do work in separate work sessions, but results return through the same personal intelligence unless you deliberately open a direct work session.

## Messages And Activity

GSV separates two things that are useful for different reasons:

- **Messages** are what you or GSV deliberately sent in the conversation.
- **Activity** is how a piece of work happened: reasoning, drafts, commands, tools, approvals, retries, and errors.

Use Messages for the conversation. Open a work item's Activity when you want to inspect, debug, approve, interrupt, or understand how something was done.

## Work You Can See And Control

GSV can hand off parts of a request or keep longer tasks separate so Home remains responsive. The Work area shows those tasks and lets you inspect, reset, stop, or open one directly.

Sent messages remain in the conversation when work stops. Returning Home leaves other work running; Abort, Reset, and Kill provide explicit lifecycle controls.

## Places GSV Can Act

GSV can act in several places when they are connected and authorized:

- its own files and tools;
- a connected computer running the machine service;
- a supported browser connection;
- linked messaging and email accounts;
- MCP and OAuth-connected services.

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
