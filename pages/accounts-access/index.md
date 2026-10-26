# Accounts And Permissions

[Back to the manual](../../index.md)

Accounts identify who is acting. Permissions decide which actions that identity may request. Ownership and approval rules narrow those permissions for a particular file, computer, integration, message, or helper.

## Common Identities

- The **owner account** signs in and owns the Ship's conversations, work, files, computers, messengers and connected services.
- The **Ship account** holds Ship's context, skills, and working identity for that owner.
- Additional **helper identities** can have focused context and permissions.
- A **computer identity** authenticates one connected computer.
- A connected messenger account proves that an external sender represents the signed-in owner.

Each Ship has one personal human account. Activation also creates a Ship account
and a helper account for handed-off work. The administrator is a separate sign-in;
ordinary use does not run as the administrator. The final local-account activation
step asks for a password and derives the internal username from the Ship's handle.
Existing Ships retain their username, UID, home and connections. See [Passwords, sessions, and access](credentials-sharing.md).

Other people have their own Ships. Connect with them through
[People](../integrations/contacts.md), without adding a local account.

Signup and sign-in start in light mode unless you have saved a theme choice.
The Ship logo on signup returns to the homepage. The handle/email form has no
Back button.

During signup, **Email me occasionally with cool Ship updates** is optional and starts unchecked.
It is separate from the required account agreement. Only an explicit choice made
while creating a Ship with a verified email requests a subscription; signing in
or verifying an email alone does not. Use the unsubscribe link in a product email
to stop receiving updates. Existing subscribers, including unsubscribed addresses,
are left unchanged.

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

- the file or helper has another owner;
- the selected computer or integration is unavailable;
- the destination is not connected to this person;
- the path or operation is outside the allowed scope;
- approval policy asks or blocks;
- the operator has disabled or limited that service.

Authority comes from authenticated identity, ownership, capability, and approval checks; process IDs, labels, paths, provider usernames, and destination IDs are selectors.

## Pages In This Section

- [Passwords, sessions, tokens, computers, and external accounts](credentials-sharing.md)
