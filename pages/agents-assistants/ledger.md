# Logs

[Talk With GSV And Manage Work](index.md)

The ledger is the installation's record of what ran: one line per action that went through GSV, whoever asked for it. A process reading a file on a computer, a person running a command, an adapter delivering a message: each is one line with who asked, where it ran, the call, its arguments, the purpose the tool gave, the outcome, and the duration.

Use it to answer "what happened" without depending on a work item's history, which is compacted over time and was never meant to be an audit trail.

## Read It

Open **Settings → Logs**; lines arrive live and update when a call completes. Open a line for its request details, duration and any failure. **Inspect process** opens that process in Fleet. The purpose column is the one-sentence reason the tool supplied for the person.

The same record is available to clients through the `sys.ledger.list` capability, scoped to the owning person or root.

## What A Line Holds

- who asked: the principal kind and account, and the process and run when a process asked;
- where: a target id, or `gsv` for the installation itself;
- the call and its arguments as sent, whole, cut at 16 KB with the cut marked;
- the purpose, when the tool supplied one;
- the outcome: `ok`, `failed`, `denied`, or `cancelled`, or empty while in flight;
- the duration, and token and cost figures for a text generation.

Nothing is redacted: the ledger is the owner's own record. A credential handed to a command as an argument is recorded like anything else, so treat ledger output as sensitive when sharing it.

## What Is Not Recorded

Model calls a process makes through the inference service, and federation reads served to a contact, do not cross this path; each keeps its own record.
