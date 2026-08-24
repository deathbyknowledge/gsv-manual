# Schedule And Delegate Work

[Back to the manual](../../index.md)

Use automation when something should happen later or repeat. Use delegation when an active request needs a bounded piece of separate work now.

## Choose The Mechanism

| Need | Use |
| --- | --- |
| Ask GSV to think or act later | `sched add --here` |
| Send fixed text later without a model run | `sched add --to` |
| Run a recurring shell command | `crontab` |
| Hand off a bounded task and receive its result | `proc delegate` |
| Keep independent work with its own history and controls | a separate Work item |

## Before Creating Automation

Confirm:

- what should happen;
- when and in which timezone;
- whether it repeats;
- where any result should be delivered;
- which identity and target own the action;
- how the user can inspect, disable, or remove it.

Create recurring automation for an intent that genuinely recurs. Keep one-time work as a one-time schedule or ordinary request.

## More Detail

- [Schedules, queues, and delegation](schedules-processes-delegation.md)
