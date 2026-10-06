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

Web and Desktop sign in as a person. Locking, signing out, or switching users clears that client's private cached data and active session.

A browser or Desktop session is separate from a connected computer, messenger, or OAuth account. Signing out ends that client session; those other relationships remain connected.

## User Tokens

User tokens support non-interactive clients with bounded authority. Create, list, and revoke them under **Settings → sign-in** or with the corresponding `gsv` CLI command. Label each token by purpose and revoke it when that purpose ends.

A newly created raw token may be shown once. Do not place it in a message, prompt, ordinary file, log, or screenshot.

## Machine Credentials

Each connected computer has a credential bound to its machine identity. Desktop can enroll the computer and install its background service. Revoking that machine stops its connection without signing the person out everywhere else.

See [Computers and browser](../devices-workplaces/index.md).

## Messaging Identities

Connecting a messaging account gives GSV access to the service. A separate, short-lived one-time challenge links an external sender to the owner from inside an authenticated GSV session.

An external identity is linked only through the authenticated challenge, not from a display name, typed provider ID, or untrusted message. See [Connect and route messaging](../integrations/adapters-routing.md).

## External Account Secrets

Provider tokens and OAuth credentials belong to the connection that uses them. Prefer supported connection flows over asking the user to paste secrets into chat. Report account name, scope, and connection status—not secret values.

## Inviting People

Only root sees **Settings → people**. To invite someone, enter the username they will use (lowercase, starting with a letter or `_`, up to 32 characters) and choose **create invitation**. GSV shows a private link that expires after ten minutes; share it through a channel you trust. The person opens it, chooses a password, and is signed in to their own account. Pending invitations are listed with **cancel invitation**.

For each other account, root can **set password** (at least 8 characters; existing credentials and messenger links are revoked, so the person signs in again and re-links messengers) and **remove access** (their credentials and messenger links stop working; their data and running work remain).

Ship can do the same on root's behalf when asked; delegated work cannot invite or remove people.

## Password Recovery

Root recovery goes through the installation's owner sign-in: the verified owner starts recovery from **My spaces**, and a fresh verification bound to that attempt is required. An ordinary owner session is not enough. Other people in a space ask root to set a new password. Passkeys are not supported; keep each person's password and linked identities exclusive to that person.
