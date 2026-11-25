# Passwords, Sessions, Tokens, And People

[Accounts And Permissions](index.md)

## Sign-In Sessions

Where the owner verified an email at signup, the web app and the desktop app sign in to the
personal account with that email: the person enters it, then the six-digit code sent to it, or
uses the **Sign in** button in that email from the same browser. The page only says a code is on its
way "if this is this Ship's email". A sign-in lasts 30 days on that device. **Sign in with a
password** uses a password instead. A person who signs in by email has no password until they add
one in **Settings → Account**, for example to use the command line. Other Ships ask for the
personal password.

The small **admin** link in the sign-in footer explicitly selects the administrator, which always
signs in with its password. The CLI also defaults to personal sign-in with `gsv login SPACE`: it
asks for the email and then the code where the Ship offers that, and Enter at the email prompt uses
the password instead. Use `gsv login SPACE --username root` for administration. Locking or signing
out clears that client's private cached data and active session.

Ship cannot sign in for the person. When someone can't sign in, point them to the sign-in page or
`gsv login`; never ask for an email code or password in chat.

A browser or desktop app session is separate from a connected computer, messenger, or OAuth account. Signing out ends that client session; those other relationships remain connected.

## User Tokens

User tokens support non-interactive clients with bounded authority. Create, list, and revoke them with `gsv auth token create`, `list` and `revoke`, which remain available for one release for CI and other scripts. Label each token by purpose and revoke it when that purpose ends.

A newly created raw token may be shown once. Do not place it in a message, prompt, ordinary file, log, or screenshot.

## Computer Credentials

Each connected computer has a credential bound to its computer identity. The desktop app can connect the computer and install its background service. Pairing with `gsv pair CODE` saves that credential; do not create a token and copy it into the computer's configuration by hand. Revoking that computer, with `gsv places forget NAME` or `gsv unpair` on the computer itself, stops its connection without signing the person out everywhere else.

See [Connections](../devices-workplaces/index.md).

## Messenger Accounts

Connecting a messaging account gives Ship access to the service. A separate, short-lived one-time challenge connects an external sender to the owner from inside an authenticated Ship session.

An external account is connected only through the authenticated challenge, not from a display name, typed provider ID, or untrusted message. See [Connect and route messaging](../integrations/adapters-routing.md).

## External Account Secrets

Provider tokens and OAuth credentials belong to the connection that uses them. Prefer supported connection flows over asking the user to paste secrets into chat. Report account name, scope, and connection status—not secret values.

## Connecting With People

Each Ship has one personal account. Invite someone through
[People](../integrations/contacts.md) to connect your Ships.
An invitation link does not create a local account or grant access to your connections.
Someone without a Ship creates their own from their operator's signup page; no invite code is needed.

## Password Recovery

**Forgot your password?** on the Ship's sign-in page offers two ways back, and neither asks for a
username. **Email me a code** takes you to the operator's sign-in page with the Ship's handle filled
in. Enter the email you signed up with, type the code, and come back to the Ship to set a new
personal password. Or request a code through an eligible messenger you previously connected, on the
same page. Ship cannot do either on your behalf, and it should point the person to the sign-in page
rather than ask for a password or code in chat.

The email page never says whether an address owns a Ship. It says a code was sent "if this is the
email for this Ship", so no code arriving can mean a different address or no email recovery on that
Ship. Then use a messenger, sign in through the **admin** link in the sign-in footer and use
**Settings → Sign-in → Personal sign-in**, or ask the operator.

A reset revokes personal sessions and disconnects your messenger accounts; sign in again and
reconnect them. Your account, files and running work remain. If the administrator password is still
the one you chose at signup, it changes to the new password too, so the old one stops working
everywhere. An administrator password you set separately stays as it is.

To configure recovery for a Ship not yet linked to your verified identity, sign in
as the administrator and choose **Settings → Sign-in → Account recovery → set up recovery**.
Verify your email or sign in with the identity provider offered by your operator.

To recover administrator access, use the same emailed link and choose **Reset the administrator
password instead** on the page where you set the new password. Each attempt needs its own fresh code;
being signed in to **My Ships** is not enough to reset either password. Passkeys are not supported.
A Ship activated without a password has no administrator password until it is reset this way.
