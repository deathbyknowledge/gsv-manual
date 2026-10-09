# Passwords, Sessions, Tokens, And People

[Accounts And Permissions](index.md)

## Setup Recovery

If a newly claimed space still needs setup, choose **Continue setup** and sign
in with the email used to claim it. Select **Continue** beside the space to renew
its setup link. This resumes the same space and does not require a new invite.
For an invitation issued directly by an operator, ask the operator to renew it.
Owner verification resumes setup; it does not sign in to an existing local account
or reset its password.

## Sign-In Sessions

Web and Desktop ask for your personal password. **Administrator sign-in** explicitly
selects root. The CLI also defaults to personal sign-in; use `gsv auth login
--username root` for administration. Locking or signing out clears that client's private cached data and active session.

A browser or Desktop session is separate from a connected computer, messenger, or OAuth account. Signing out ends that client session; those other relationships remain connected.

## User Tokens

User tokens support non-interactive clients with bounded authority. Create, list, and revoke them with the corresponding `gsv auth token` CLI command. Label each token by purpose and revoke it when that purpose ends.

A newly created raw token may be shown once. Do not place it in a message, prompt, ordinary file, log, or screenshot.

## Machine Credentials

Each connected computer has a credential bound to its machine identity. Desktop can enroll the computer and install its background service. Revoking that machine stops its connection without signing the person out everywhere else.

See [Computers and browser](../devices-workplaces/index.md).

## Messaging Identities

Connecting a messaging account gives GSV access to the service. A separate, short-lived one-time challenge links an external sender to the owner from inside an authenticated GSV session.

An external identity is linked only through the authenticated challenge, not from a display name, typed provider ID, or untrusted message. See [Connect and route messaging](../integrations/adapters-routing.md).

## External Account Secrets

Provider tokens and OAuth credentials belong to the connection that uses them. Prefer supported connection flows over asking the user to paste secrets into chat. Report account name, scope, and connection status—not secret values.

## Connecting With People

Each space has one personal account. Invite someone through
[People](../integrations/contacts.md) to connect your separate spaces.
Contact invitations do not create local accounts or grant access to your machines.

## Password Recovery

**Forgot password?** can send a code through an eligible messenger you previously
linked. It does not ask for a username. Without an eligible link, sign in through
**Administrator sign-in**, then use **Settings → sign-in → Personal sign-in** to
reset the personal password. This requires a direct root session; Ship cannot do
it on your behalf. Reset revokes personal sessions and messenger links; sign in
again and reconnect those messengers. Your account, files and running work remain.

Root recovery goes through the installation's owner sign-in: start recovery from
**My spaces** and complete the fresh verification bound to that attempt. An
ordinary owner session cannot reset root. Passkeys are not supported.
