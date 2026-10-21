# Routines And Handing Off Work

[Back to the manual](../../index.md)

Use a reminder when something should happen once later, a routine when it should repeat. Hand off to a helper when an active request needs a bounded piece of separate work now.

## Choose The Mechanism

| Need | Use |
| --- | --- |
| Ask Ship to think or act later | `sched add --here` |
| Send fixed text later without a model run | `sched add --to` |
| Run a recurring shell command | `crontab` |
| Hand off a bounded task and receive its result | [`proc delegate --as ACCOUNT --check-after`](../agents-assistants/conversations-delegation.md#handing-off-a-bounded-task) |
| Keep independent work with its own history and controls | a separate helper |

## Before Creating A Routine

Confirm:

- what should happen;
- when and in which timezone;
- whether it repeats;
- where any result should be delivered;
- which identity and connection own the action;
- how the user can inspect, disable, or remove it.

Create a recurring routine for an intent that genuinely recurs. Keep one-time work as a reminder or ordinary request.

## More Detail

- [Routines, queues, and handing off](schedules-processes-delegation.md)
