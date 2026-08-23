# Conversations & Delegation

[Personal Intelligence & Work](index.md)

## Conversation Kinds

- **Home** is the stable Conversation with Personal. Linked private surfaces contribute to the same
  stream.
- **Work** is handled by one explicit interactive Work Process.
- **Group** belongs to one normalized adapter group, channel, or thread. The schema can represent
  multiple members, but current authorization is still owner-centered.

A Conversation owns canonical Messages. A Process owns execution activity. Deleting one does not
delete the other.

## Explicit Completion

Each model turn must finish with one terminal control:

- `Message` commits one user-visible message and its resource references.
- `Silence` records that nothing should be delivered.

Reasoning and ordinary assistant text remain Process activity. If the model omits both controls, GSV
adds one correction event and retries once; a second omission ends with an inspectable error.

For direct clients, the initiating connection receives streaming Message arguments. For adapters,
GSV commits first and the adapter performs durable provider delivery. Other clients synchronize the
committed Message rather than receiving the transient stream as though it were addressed to them.

## Delegation And IPC

Delegation creates a child Process and returns a bounded result event to its caller. It does not
append the child's transcript to Home. The caller may inspect it, continue working, send a summary,
or remain silent.

Process IPC follows the same rule. `proc.send` is asynchronous Process mail; `proc.call` waits for a
bounded `ipc.reply` or `ipc.timeout`. An IPC terminal Message returns to the calling Process, not to a
human Conversation.

## Queueing And Interruption

A Process runs one model turn at a time. New direct human input supersedes active direct work and
terminates pending tool calls consistently. Process events and scheduled work queue in FIFO order.
Late output from a superseded run cannot mutate the new run.

`proc.abort` stops the current run, `proc.reset` archives and clears Process activity while keeping
the Process, and `proc.kill` tears it down. None of them deletes canonical Conversation Messages.

## Inspection

Use the Messages view for what people saw. Use Process activity for reasoning, drafts, tools,
approvals, retries, and errors. A client explicitly observes a Process; closing the inspector removes
that subscription.

## Retention

Each Conversation has its own installation-scoped Durable Object. SQLite keeps the newest 1,000
Messages for indexed access. When that hot set grows, the oldest 500 become an immutable gzip JSON
segment in installation-scoped R2; SQLite retains the segment index and idempotency receipts. The
archive object is uploaded and verified before the synchronous commit removes hot rows.

Process history has a separate archive lifecycle. Conversation and Process retention can therefore
rotate independently without confusing what the user saw with how the answer was produced.

## For Agents

Do not copy an entire child transcript into Home. Return the smallest useful result, preserve links
or resource references where relevant, and let the owning Process decide what becomes a Message.
