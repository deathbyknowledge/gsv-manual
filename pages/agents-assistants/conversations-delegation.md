# Messages, Work, And Delegation

[Talk With GSV And Manage Work](index.md)

## What Becomes A Message

Reasoning and draft text belong to activity. A user-visible reply is sent only when the active GSV intelligence deliberately sends it with the Send tool: text alone sends the message and keeps working; text with `yield` sends it and finishes the run; `yield` alone finishes quietly, with no message. Several sends in one run each deliver exactly once, so progress messages are ordinary.

The Shell forms are the same actions:

```bash
message send --message "text for the user"
yield
```

Files can be attached before completion:

```bash
message attach /path/to/file
message send --message "Here it is."
```

Use `message current --json` to inspect the endpoint for the current interaction. Use `message destinations --all --json` when sending a separate message to another authorized destination.

If a human-facing run ends in text without sending, GSV asks it to use Send, for up to three rounds. If that still fails, the person receives "I wrote a reply but did not send it. Ask me again." instead of silence.

## One Conversation, Separate Work

The conversation stores sent messages. Each work item separately stores its inputs, reasoning, tools, results, approvals, retries, and errors. Removing a work item therefore does not erase messages that were already exchanged.

Ship is the main conversation. A Work Session is a temporary direct conversation with one selected work item. Groups and channels have their own conversations.

## Search Past Messages

In Zen, use **search**, `/` in browse mode, or `Ctrl/Cmd+F`. Open a match to read it with the surrounding messages; closing search returns to your place and draft.

Ship can search the same sent messages through Shell:

```bash
message search "Rotterdam cafes" --json
message search "Rotterdam cafes" --before SEQUENCE --limit 20 --json
message search "Rotterdam cafes" --with CONVERSATION_OR_CONTACT --json
message history --with CONVERSATION --before NEXT_SEQUENCE --limit 1 --json
```

Search defaults to Ship's conversation. Words match prefixes and all words must match; results include a snippet, message ID, sequence, author, and date. `--before` pages older matches using `nextBeforeSequence`. To read an exact message, use its sequence plus one as `NEXT_SEQUENCE` in the history command.

Search covers messages saved after the feature was enabled, including those later archived. Earlier messages remain readable through history but are not indexed retroactively. Attachment contents and internal work activity are not searched. Only a signed-in user and their Ship can read these conversations; delegated work does not inherit that access.

## Delegating A Bounded Task

Acknowledge substantial work promptly with Send, then continue. Simple lookups and short tasks can run directly. Delegate when parallel work, separate context, lengthy investigation, or waiting makes a worker useful. Replace `ACCOUNT` with the Crew account named in Ship's `~/context.d/10-delegation.md`:

```bash
proc delegate --as ACCOUNT --label research --check-after 10m "Find the answer and return the evidence."
```

The delegated task gets its own activity. Its ordinary final answer returns directly to the caller; it does not need to send a human message. The caller evaluates that result and then sends a useful answer or yields quietly.

Delegated work is supervised rather than killed on a timer: at each `--check-after` checkpoint (default 10 minutes) the caller is told the child is still running and can intervene. `--timeout` is accepted as an alias for `--check-after` and no longer kills the child.

Useful commands:

```bash
proc agents --json                    # available specialized identities
proc delegate --as ACCOUNT ...        # delegate as a specialized identity
proc list                              # visible work
proc history --pid PID                 # inspect activity
proc send PID "message"               # asynchronous process message
proc call PID "request"               # wait for a bounded process reply
```

Use `proc --help` for the full current syntax.

## New Input, Queues, And Late Results

One work item has one provider request in flight at a time. New direct human input may supersede an active direct turn. Results from other work are recorded as soon as they arrive and enter the active work item's next model context, so it can adjust the work already in progress. Scheduled work and other requests that need their own run remain queued in order.

Only the active run can modify its state. If an older result arrives after the conversation has moved on, GSV decides whether it is still useful before sending anything.

## Abort, Reset, And Kill

- **Abort** stops only the active run and keeps its history.
- **Reset** archives and clears activity while keeping the work item and its identity.
- **Kill** permanently removes that work item after cleanup.

None of these actions deletes already committed conversation messages.

## Responsibilities

Promises, follow-ups, delegated work, and recovery that must survive a run are recorded as responsibilities. Ship sees the whole list; a delegated child sees its assignments and their ancestors. Review them in **Fleet → Responsibilities** or with `r12y list`, and inspect one with `r12y show ID`. Delegated results return through the ordinary process result path; the responsibility retains the unfinished outcome and references to its evidence.

A brief acknowledgment may precede bookkeeping. Record unfinished accepted outcomes before delegation or yielding; pass the record with `proc delegate --as ACCOUNT --responsibility ID ...`. Keep assignments, blockers, and next checks current. A worker's result is evidence for Ship to assess, not automatic completion of the user's outcome. Immediate answers, short tasks completed in the run, and ordinary retries do not need separate records.

## Retention

GSV keeps recent conversation messages readily searchable and archives older conversation history in segments as it grows. Work activity has its own retention and archive lifecycle, so conversation history and work history can each be retrieved at the level of detail they need.
