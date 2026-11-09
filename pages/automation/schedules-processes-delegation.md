# Routines, Queues, And Handing Off

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

## The Hourly Journal

The journal is a Ship routine named `Journal` that wakes Ship every hour while the person is usually awake. At each check-in Ship records what happened since the previous one in the person's journal, `pages/journal/YYYY/MM/YYYY-MM-DD.md` in the `personal` wiki, and decides whether the person would want anything done now. Usually the answer is nothing. The built-in `journal` skill has the steps, the entry format and the command that turns it on:

```bash
sched add --ship --name Journal --cron "0 7-23 * * *" --message "Journal check-in. Use the journal skill."
```

From a terminal, the person can run `gsv journal on`, `gsv journal now` (check in straight away), `gsv journal off`, and `gsv journal` to see a day as a strip of check-ins. Removing the routine stops the check-ins; the journal stays in the wiki.

## Recurring Shell Commands

Use `crontab` for a recurring shell command. It runs unattended, so every operation must already be authorized.

## Telling The Owner When Something Happens

When a routine, script or outside service should tell the person something, give it an event source instead of writing a message from the routine. `event source add NAME` creates one, `event emit NAME --title TEXT --id ID` records an event, and the person's choices for that source decide whether they're told and whether Ship sees it. A repeated `--id` is ignored, so a poller can re-read the same items. An outside service uses a webhook address from `event source add NAME --webhook standard|hmac|url`, chosen by how it signs; the built-in `event-sources` skill has the flags for common senders. See [Your own sources](../settings/when-things-happen.md#your-own-sources).

## Handing Off Work

Handing off is for immediate, bounded work. Replace `ACCOUNT` with the helper account named in Ship's `~/context.d/10-delegation.md`:

```bash
proc delegate --as ACCOUNT --label invoices --check-after 10m "Compare the invoices and return discrepancies."
```

The result returns to the calling Ship or helper, and the caller is told at each checkpoint while the helper is still running. The caller decides what to send to the person. See [Messages, work, and delegation](../agents-assistants/conversations-delegation.md).

## Queued Work

Ship and each helper have one provider request in flight at a time. Routine events that need their own run queue in order. Handed-off results enter the caller's active context as soon as the current provider request can observe them. New direct human input may supersede current direct work.

Routines run without an interactive approver. An operation whose policy requires interactive confirmation fails visibly.
