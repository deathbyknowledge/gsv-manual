# Accounts And Permissions

[Back to the manual](../../index.md)

Accounts identify who is acting. Permissions decide which actions that identity may request. Ownership and approval rules narrow those permissions for a particular file, computer, integration, message, or work item.

## Common Identities

- The **owner account** signs in and owns the installation's conversations, work, files, computers, and connections.
- The **personal-intelligence account** holds Ship's context, skills, and working identity for that owner.
- Additional **work identities** can have focused context and permissions.
- A **machine identity** authenticates one connected computer.
- A linked messaging identity proves that an external sender represents the signed-in owner.

Each space has one personal human account. Setup creates that account, its Ship,
and a Crew account for delegated work. Root is a separate administrative login;
ordinary use does not run as root. Setup asks only for a password and derives the
internal username from the space handle. Existing spaces retain their username,
UID, home and paired devices. See [Passwords, sessions, and access](credentials-sharing.md).

Other people have their own spaces. Connect with them through
[People](../integrations/contacts.md), without adding a local account.

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
