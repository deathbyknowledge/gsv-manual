# Schedules, Queues & Delegation

[Automation & Delegation](index.md)

## Process Event Schedules

`sched add --here` from a Process-backed shell captures the current Process. At each firing it admits
a typed event to that PID. If the schedule was created during an authorized adapter run, it may also
retain that opaque destination for the resulting committed Message.

A successful firing means admission succeeded; it does not mean the model finished or delivery was
confirmed. If the Process is killed, recreate or remove the schedule explicitly.

## Direct Delivery Schedules

`sched add --to DESTINATION` sends fixed text through an authorized adapter without running a model.
Use an opaque destination from `message destinations --all`; provider IDs do not belong in the
schedule contract.

## Cron

Crontab entries run background shell commands. They have no Process caller and cannot use delegation.
If they spawn an agent, make it non-interactive and do not assume its raw answer appears in Home.

## Queues

Each Process runs one agent turn at a time. Human input supersedes an active direct turn. Scheduler
and Process events queue FIFO and become separate runs. Queueing preserves ordering; it is not a
delivery failure.

## Delegation

`proc delegate` creates a child, bounds its execution, and reports the terminal result to the caller
as a Process event. `proc.call` provides bounded IPC to an existing Process. Neither automatically
creates a user Message.

Delegated work should return a compact result, stable artifact/reference, status, and any remaining
follow-up. The parent decides what to expose to the user.

## Lifecycle

- Abort stops only the current run.
- Reset archives and clears Process activity but preserves the Process.
- Kill archives as requested, permanently tombstones the PID, and performs retryable cleanup.

Canonical Conversations remain separate from all three operations.

## For Agents

Use typed events and bounded IPC rather than transcript copying. Never create a recurring automation
without an observable owner and cancellation path.
