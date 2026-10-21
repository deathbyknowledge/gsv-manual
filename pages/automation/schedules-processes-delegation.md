# Schedules, Queues, And Delegation

[Routines And Handing Off Work](index.md)

## Ask Ship To Act Later

From the shell of Ship or an active helper, schedule a reminder that sends a message back to it:

```bash
sched add --here --name follow-up --after 2h --message "Check whether the export completed."
```

Other time forms include:

```bash
sched add --here --name daily-review --every 1d --message "Review today's open commitments."
sched add --here --name weekday-review --cron "0 9 * * 1-5" --timezone Europe/Amsterdam --message "Prepare the weekday review."
sched add --here --name appointment --at 2026-09-01T14:00:00Z --message "Remind the user about the appointment."
```

A successful firing means the event reached Ship or the helper. Later model work and external delivery report their own outcomes.

## Send Fixed Text Later

Choose an authorized destination from Ship's destination list:

```bash
message destinations --all --json
sched add --to DESTINATION --name reminder --after 30m --message "The oven timer is done."
```

This sends the fixed text without asking a model to compose it at firing time.

## Inspect And Control Routines

In the web app or the desktop app, open **N ongoing** (or **plans**) above
Chat's prompt, then select **routines**. Open a routine to inspect or
pause/enable it; editable routines also offer **edit routine**. **new routine**,
or **+ → create a routine** beneath the Chat prompt, stages a request to Ship.
Add the desired outcome and timing, then send it normally. The shortcut itself
does not create a routine.

```bash
sched list --all
sched disable <id>
sched enable <id>
sched run <id> --force
sched remove <id>
```

A routine remains attached to Ship or the helper it was created from. After that one is killed, recreate the routine for its replacement or remove it.

## Recurring Shell Commands

Use `crontab` for a recurring shell command. It runs unattended, so every operation must already be authorized.

## Handing Off Work

Handing off is for immediate, bounded work. Replace `ACCOUNT` with the helper account named in Ship's `~/context.d/10-delegation.md`:

```bash
proc delegate --as ACCOUNT --label invoices --check-after 10m "Compare the invoices and return discrepancies."
```

The result returns to the calling Ship or helper, and the caller is told at each checkpoint while the helper is still running. The caller decides what to send to the person. See [Messages, work, and delegation](../agents-assistants/conversations-delegation.md).

## Queued Work

Ship and each helper have one provider request in flight at a time. Routine events that need their own run queue in order. Handed-off results enter the caller's active context as soon as the current provider request can observe them. New direct human input may supersede current direct work.

Routines run without an interactive approver. An operation whose policy requires interactive confirmation fails visibly.
