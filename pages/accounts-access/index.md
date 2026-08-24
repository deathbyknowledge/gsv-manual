# Accounts And Permissions

[Back to the manual](../../index.md)

Accounts identify who is acting. Permissions decide which actions that identity may request. Ownership and approval rules narrow those permissions for a particular file, computer, integration, message, or work item.

## Common Identities

- The **owner account** signs in and owns the installation's conversations, work, files, computers, and connections.
- The **personal-intelligence account** holds Home's context, skills, and working identity for that owner.
- Additional **work identities** can have focused context and permissions.
- A **machine identity** authenticates one connected computer.
- A linked messaging identity proves that an external sender represents the signed-in owner.

Onboarding creates one human owner. Invitations and multi-human administration are not yet available.

## Inspect Identity

Inside a work shell:

```bash
whoami
id
proc agents --json
```

The first two show the current run-as identity and groups. `proc agents` lists identities available for owned work.

## Permission Checks

A capability allows a kind of action, such as reading files, sending messages, or calling an integration. A specific action may still fail because:

- the file or work item has another owner;
- the selected computer or integration is unavailable;
- the destination is not linked to this person;
- the path or operation is outside the allowed scope;
- approval policy asks or denies;
- the installation has disabled or limited that service.

Authority comes from authenticated identity, ownership, capability, and approval checks; process IDs, labels, paths, provider usernames, and destination IDs are selectors.

## Pages In This Section

- [Passwords, sessions, tokens, machines, and external identities](credentials-sharing.md)
