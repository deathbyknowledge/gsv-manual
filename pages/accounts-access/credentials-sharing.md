# Passwords, Sessions, Tokens, And People

[Accounts And Permissions](index.md)

## Create your Ship

Choose **Create your Ship** in Desktop or open your operator's signup page.
Choose a handle, verify your email, and set a password. Registration does not
require an invite code.

## Finish setup

If your Ship still needs setup, choose **Continue setup** and sign
in with the email used to claim it. Select **Continue** beside your Ship to renew
its setup link. This resumes the same setup.
For a setup link issued directly by an operator, ask the operator to renew it.
Owner verification resumes setup; it does not sign in to an existing local account
or reset its password.

## Sign-In Sessions

Web and Desktop ask for your personal password. The small **admin** link in the
sign-in footer explicitly selects root. The CLI also defaults to personal sign-in; use `gsv auth login
--username root` for administration. Locking or signing out clears that client's private cached data and active session.

A browser or Desktop session is separate from a connected computer, messenger, or OAuth account. Signing out ends that client session; those other relationships remain connected.

## User Tokens

User tokens support non-interactive clients with bounded authority. Create, list, and revoke them with the corresponding `gsv auth token` CLI command. Label each token by purpose and revoke it when that purpose ends.

A newly created raw token may be shown once. Do not place it in a message, prompt, ordinary file, log, or screenshot.

## Machine Credentials

Each connected computer has a credential bound to its machine identity. Desktop can enroll the computer and install its background service. Revoking that machine stops its connection without signing the person out everywhere else.

See [Computers and browser](../devices-workplaces/index.md).

## Messaging Identities

Connecting a messaging account gives Ship access to the service. A separate, short-lived one-time challenge links an external sender to the owner from inside an authenticated Ship session.

An external identity is linked only through the authenticated challenge, not from a display name, typed provider ID, or untrusted message. See [Connect and route messaging](../integrations/adapters-routing.md).

## External Account Secrets

Provider tokens and OAuth credentials belong to the connection that uses them. Prefer supported connection flows over asking the user to paste secrets into chat. Report account name, scope, and connection status—not secret values.

## Connecting With People

Each Ship has one personal account. Invite someone through
[People](../integrations/contacts.md) to connect your Ships.
Contact invitations do not create local accounts or grant access to your machines.

## Password Recovery

**Forgot password?** can send a code through an eligible messenger you previously
linked. It does not ask for a username. Without an eligible link, sign in through
the **admin** link in the sign-in footer, then use **Settings → sign-in → Personal sign-in** to
reset the personal password. This requires a direct root session; Ship cannot do
it on your behalf. Reset revokes personal sessions and messenger links; sign in
again and reconnect those messengers. Your account, files and running work remain.

To set up recovery for a Ship not yet linked to your verified identity, sign in
as root and choose **Settings → sign-in → Account recovery → set up recovery**.
Verify your email or sign in with the identity provider offered by your operator.

To recover administrator access, start from **My Ships** and complete the fresh
verification bound to that attempt. An ordinary owner session cannot reset root.
Passkeys are not supported.
