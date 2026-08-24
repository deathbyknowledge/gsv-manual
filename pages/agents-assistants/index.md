# Talk With GSV And Manage Work

[Back to the manual](../../index.md)

Most of the time, use Home and speak naturally. GSV decides whether it can answer immediately or should separate part of the request into visible work.

## Home

Home is the main conversation with your personal intelligence. It keeps the same identity, files, preferences, and memory even when its current work history is reset or replaced.

Private messages from linked apps normally return to Home. Ask for the outcome there; Home separates and coordinates work when useful.

## Work

Work contains tasks with their own activity and controls. Open it when you want to:

- see what is running or waiting;
- inspect reasoning, commands, tools, or errors;
- approve, interrupt, reset, or remove work;
- talk directly to one work item for a while.

A direct Work Session is clearly labeled. Leaving it returns to the personal intelligence in Home while that work item keeps its own identity.

## Messages Versus Activity

- **Messages** show the conversation: what people and GSV deliberately sent.
- **Activity** shows how an answer or task was produced.

This separation keeps the conversation readable and the reasoning and tool use inspectable.

## Common Actions

| Goal | Action |
| --- | --- |
| See visible work | Open **Work** or run `proc list` |
| Inspect the current work item | Run `proc self`, then `proc history --pid <pid>` |
| Hand off a bounded subtask | `proc delegate --label LABEL --timeout DURATION TASK` |
| Stop only the active run | use **Abort** in the active client |
| Clear activity but keep the work item | Reset / `proc reset --pid <pid>` |
| Remove a work item | Kill / `proc kill <pid>` |
| Return a messenger chat to Home | `/home` |

## More Detail

- [Messages, work, and delegation](conversations-delegation.md)
- [Identity, context, files, and approvals](identity-context-approvals.md)
