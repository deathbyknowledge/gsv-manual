# Schedules, Queues, And Delegation

[Schedule And Delegate Work](index.md)

## Ask GSV To Act Later

From an active GSV work shell, schedule a message back to that work item:

```bash
sched add --here --name follow-up --after 2h --message "Check whether the export completed."
```

Other time forms include:

```bash
sched add --here --name daily-review --every 1d --message "Review today's open commitments."
sched add --here --name weekday-review --cron "0 9 * * 1-5" --timezone Europe/Amsterdam --message "Prepare the weekday review."
sched add --here --name appointment --at 2026-09-01T14:00:00Z --message "Remind the user about the appointment."
```

A successful firing means the event reached the work item. Later model work and external delivery report their own outcomes.

## Send Fixed Text Later

Choose an authorized destination from GSV's destination list:

```bash
message destinations --all --json
sched add --to DESTINATION --name reminder --after 30m --message "The oven timer is done."
```

This sends the fixed text without asking a model to compose it at firing time.

## Inspect And Control Schedules

```bash
sched list --all
sched disable <id>
sched enable <id>
sched run <id> --force
sched remove <id>
```

A schedule remains attached to its original work item. After that work item is killed, recreate the schedule for its replacement or remove it.

## Recurring Shell Commands

Use `crontab` for a recurring shell command. Cron runs unattended, so every operation must already be authorized.

## Delegation

Delegation is immediate, bounded work:

```bash
proc delegate --label invoices --timeout 5m "Compare the invoices and return discrepancies."
```

The result returns to the calling work item. The caller decides what to send to the person. See [Messages, work, and delegation](../agents-assistants/conversations-delegation.md).

## Queued Work

One work item runs one turn at a time. Schedule events and delegated results queue in order. New direct human input may supersede current direct work; queued events remain in order.

Scheduled work runs without an interactive approver. An operation whose policy requires interactive confirmation fails visibly.
