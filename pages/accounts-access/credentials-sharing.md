# Passwords, Sessions, Tokens, And Links

[Accounts And Permissions](index.md)

## Sign-In Sessions

Web and Desktop sign in as a person. Locking, signing out, or switching users clears that client's private cached data and active session.

A browser or Desktop session is separate from a connected computer, messenger, or OAuth account. Signing out ends that client session; those other relationships remain connected.

## User Tokens

User tokens support non-interactive clients with bounded authority. Create, list, and revoke them through the authenticated administration surface or corresponding `gsv` CLI command. Label each token by purpose and revoke it when that purpose ends.

A newly created raw token may be shown once. Do not place it in a message, prompt, ordinary file, log, or screenshot.

## Machine Credentials

Each connected computer has a credential bound to its machine identity. Desktop can enroll the computer and install its background service. Revoking that machine stops its connection without signing the person out everywhere else.

See [Computers and browser](../devices-workplaces/index.md).

## Messaging Identities

Connecting a messaging account gives GSV access to the service. A separate, short-lived one-time challenge links an external sender to the owner from inside an authenticated GSV session.

An external identity is linked only through the authenticated challenge, not from a display name, typed provider ID, or untrusted message. See [Connect and route messaging](../integrations/adapters-routing.md).

## External Account Secrets

Provider tokens and OAuth credentials belong to the connection that uses them. Prefer supported connection flows over asking the user to paste secrets into chat. Report account name, scope, and connection status—not secret values.

## Password Recovery And Additional Humans

Onboarding creates the first owner. Self-service password recovery, invitations, and multi-human conversation membership are not yet available. Use the installation's operator recovery path, and keep the owner's password and linked identities exclusive to that person.
