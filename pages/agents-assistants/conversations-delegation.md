# Messages, Work, And Delegation

[Talk With GSV And Manage Work](index.md)

## What Becomes A Message

Reasoning and draft text belong to activity. A user-visible reply is sent only when the active GSV intelligence deliberately finishes with:

```bash
message send --message "text for the user"
```

If no reply should be sent:

```bash
message silence --reason "why no message is needed"
```

Files can be attached before completion:

```bash
message attach /path/to/file
message send --message "Here it is."
```

Use `message current --json` to inspect the endpoint for the current interaction. Use `message destinations --all --json` when sending a separate message to another authorized destination.

If a run ends without sending or silencing, GSV asks it once to choose. A second omission ends with an error visible in activity.

## One Conversation, Separate Work

The conversation stores sent messages. Each work item separately stores its inputs, reasoning, tools, results, approvals, retries, and errors. Removing a work item therefore does not erase messages that were already exchanged.

Ship is the main conversation. A Work Session is a temporary direct conversation with one selected work item. Groups and channels have their own conversations.

## Delegating A Bounded Task

Use delegation when an active request needs investigation, several steps, waiting, or parallel work:

```bash
proc delegate --label research --timeout 5m "Find the answer and return the evidence."
```

The delegated task gets its own activity. Its result returns to the caller, which evaluates it and then sends a useful answer or remains silent.

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

One work item handles one model turn at a time. New direct human input may supersede an active direct turn. Scheduled events and results from other work queue in order.

Only the active run can modify its state. If an older result arrives after the conversation has moved on, GSV decides whether it is still useful before sending anything.

## Abort, Reset, And Kill

- **Abort** stops only the active run and keeps its history.
- **Reset** archives and clears activity while keeping the work item and its identity.
- **Kill** permanently removes that work item after cleanup.

None of these actions deletes already committed conversation messages.

## Retention

GSV keeps recent conversation messages readily searchable and archives older conversation history in segments as it grows. Work activity has its own retention and archive lifecycle, so conversation history and work history can each be retrieved at the level of detail they need.
