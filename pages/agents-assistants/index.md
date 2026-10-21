# Talk With Ship And Manage Work

[Back to the manual](../../index.md)

Most of the time, use Ship and speak naturally. Ship decides whether it can answer immediately or should hand part of the request off to a helper.

## Ship

Ship is your main conversation with Ship. It keeps the same identity, files, preferences, and memory even when its current work history is reset or replaced.

Private messages from connected messengers normally return to Ship. Ask for the outcome there; Ship hands off and coordinates work when useful.

## Work

Work contains helpers with their own activity and controls. Open it when you want to:

- see what is running or waiting;
- inspect reasoning, commands, tools, or errors;
- approve, interrupt, reset, or remove work;
- talk directly to one helper for a while.

A direct conversation with a helper is clearly labeled. Leaving it returns to Ship while that helper keeps its own identity.

## Messages Versus Activity

- **Messages** show the conversation: what people and Ship deliberately sent.
- **Activity** shows how an answer or task was produced.

This separation keeps the conversation readable and the reasoning and tool use inspectable.

## Common Actions

| Goal | Action |
| --- | --- |
| See helpers | Open **Work → Helpers** or run `proc list` |
| Inspect Ship or the current helper | Run `proc self`, then `proc history --pid <pid>` (`--tail` for the newest) |
| See every action taken and why | Open **Settings → Logs** |
| Review open promises and follow-ups | Open **N ongoing** (or **plans**) above Chat's prompt, then **ongoing**; or run `r12y list` |
| Hand off a bounded subtask | `proc delegate --as ACCOUNT --label LABEL --check-after DURATION TASK`; select the account named in Ship's `~/context.d/10-delegation.md` |
| Stop only the active run | use **Abort** in the active client |
| Clear activity but keep the helper | Reset / `proc reset --pid <pid>` |
| Remove a helper | Kill / `proc kill <pid>` |
| Return a messenger chat to Ship | `/ship` |

## More Detail

- [Messages, work, and delegation](conversations-delegation.md)
- [Identity, context, files, and approvals](identity-context-approvals.md)
- [Logs](ledger.md)

## Operator Updates

The operator can supply release briefs as ordinary `operator.update`
responsibilities. They show the publisher, update ID, publication time and brief.
Kernel adds each eligible update once when an existing Ship is used.
New users skip historical updates covered by their initial activation date.

Explain relevant changes at a suitable moment in the next conversation. Follow
the user's instructions and permissions, and check runtime facts before claiming
that a feature or address is available. Do not interrupt urgent work, send an
unsolicited announcement solely for this record, or rename files for branding.
Resolve the responsibility after communicating the relevant information, noting
the committed Message when available, or record why it is irrelevant. Resolved
and cancelled updates stay deduplicated.
