# Automation & Delegation

[Back to GSV Manual](../../index.md)

Automation admits explicit future work into Processes or sends direct scheduled text through an
authorized adapter destination. Delegation creates bounded child Processes. Both remain visible and
controllable.

## Choices

- Use a **Process event schedule** when an agent should think at firing time.
- Use a **direct adapter schedule** for fixed text that needs no model run.
- Use **cron** for background shell commands.
- Use **delegation** when an active Process needs a bounded subtask result.
- Use a separate long-lived Work Process when the work needs independent history and control.

## Safety

Scheduled/background profiles cannot depend on interactive approval. Schedules target a physical PID
or authorized destination; killing a Process does not silently retarget its schedule to a new
Personal Process.

Every automation must expose ownership, next fire, enabled state, latest outcome, and a stop/remove
path.

## Page In This Section

- [Schedules, Queues & Delegation](schedules-processes-delegation.md)

## For Agents

Do not create recurring work merely because one execution was useful. State the cadence, target,
delivery behavior, and how the user can disable it.
