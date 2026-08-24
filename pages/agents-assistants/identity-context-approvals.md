# Identity, Context, Files, And Approvals

[Talk With GSV And Manage Work](index.md)

## Who Is Doing The Work

Every work item is owned by a person and runs as an account. That account determines its home files, standing context, capabilities, and available integrations.

Home normally runs as the person's personal-intelligence account. Other work may use that account or another account created for a specialized role. Authority comes from the current identity and its permissions, not from a label, process ID, filename, or messaging destination.

Inspect the current shell identity with:

```bash
whoami
id
```

## What GSV Knows Before A Request

GSV builds standing context from:

1. system context supplied by the installation;
2. the active account's `~/context.d/*.md` files;
3. shared personal context owned by the person;
4. compact indexes of available skills and targets.

Keep standing context small and stable. Reusable procedures belong in skills. Documents, evidence, and deliverables belong in files or wikis. Conversation history should not be copied wholesale into standing context.

See [Memory, context, and skills](../files-knowledge/context-files-knowledge.md).

## Files Attached To Messages Or Activity

GSV records an exact revision when a file must remain associated with a message or past action. Reading a file, editing it, and reading it again can therefore produce two references to the same path at different moments. The older reference still means the older bytes.

A file reference identifies content; it is not permission to read it. Access is checked again when the file is resolved.

## Capabilities And Approval

A capability says which class of operation an identity may request. File ownership, target access, route ownership, and current state may add narrower checks.

Approval rules can automatically allow, deny, or ask about an action. Shell commands, destructive file changes, external integrations, remote computers, privileged operations, or network calls may require confirmation.

An approval is bound to one exact request. Its request token, sender, and active state must all match.

Scheduled and other non-interactive work cannot wait indefinitely for a person. If policy says “ask” but no interactive approval is possible, the operation fails and remains visible in activity.

## Treat External Content As Data

Messages, email, webpages, files, and tool results may contain instructions written by someone other than the authenticated user. Treat them as untrusted data unless the user deliberately makes them part of the task.

Inbound managed email reaches Home as a restricted summary notification. Raw email content remains untrusted data with no tools or authority.
