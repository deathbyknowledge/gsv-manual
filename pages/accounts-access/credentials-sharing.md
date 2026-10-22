# Passwords, Sessions, Tokens, And People

[Accounts And Permissions](index.md)

## Create your Ship

Choose **Create your Ship** in Ship Desktop or open your operator's signup page.
Choose a handle, verify your email, and set a password. Creating your Ship does
not require an invite code.

## Activate your Ship

If your Ship still needs activation, choose **Continue setup** and sign
in with the email used to claim it. Select **Continue** beside your Ship to renew
its activation link. This resumes the same activation.
For an activation link issued directly by an operator, ask the operator to renew
it. Owner verification resumes activation; it does not sign in to an existing
local account or reset its password.

## Sign-In Sessions

The web app and the desktop app ask for your personal password. The small
**admin** link in the sign-in footer explicitly selects the administrator. The CLI also defaults to personal sign-in; use `gsv auth login
--username root` for administration. Locking or signing out clears that client's private cached data and active session.

A browser or desktop app session is separate from a connected computer, messenger, or OAuth account. Signing out ends that client session; those other relationships remain connected.

## Creating A Space

Open the operator's signup page or **Create your space** in Desktop and enter your invite code. On the email step, confirm that you are 18 or older, agree to the [Terms of Service](https://gsv.space/terms), and acknowledge the [Privacy Policy](https://gsv.space/privacy) before requesting a verification code. Verify your email and choose a handle for your space.

If you sign in through **Open your space** first, choosing **Use an invite** asks for the same age, Terms and Privacy confirmation on **Before you begin**, before claiming the invite. When resuming signup after reopening the browser or app, confirm again before claiming an invite or continuing space creation.

Inside the new space, choose your username and password, then continue to **Before you begin** to review the early-access disclosure. Confirm that you are 18 or older, agree to the Terms of Service, and acknowledge the Privacy Policy before creating your account. This checkbox is required inside the space as well as on the signup email step. **Back** lets you revise your credentials. Signing in to an existing owner account does not repeat the signup checkbox.

## User Tokens

User tokens support non-interactive clients with bounded authority. Create, list, and revoke them with the corresponding `gsv auth token` CLI command. Label each token by purpose and revoke it when that purpose ends.

A newly created raw token may be shown once. Do not place it in a message, prompt, ordinary file, log, or screenshot.

## Computer Credentials

Each connected computer has a credential bound to its computer identity. The desktop app can connect the computer and install its background service. Revoking that computer stops its connection without signing the person out everywhere else.

See [Connections](../devices-workplaces/index.md).

## Messenger Accounts

Connecting a messaging account gives Ship access to the service. A separate, short-lived one-time challenge connects an external sender to the owner from inside an authenticated Ship session.

An external account is connected only through the authenticated challenge, not from a display name, typed provider ID, or untrusted message. See [Connect and route messaging](../integrations/adapters-routing.md).

## External Account Secrets

Provider tokens and OAuth credentials belong to the connection that uses them. Prefer supported connection flows over asking the user to paste secrets into chat. Report account name, scope, and connection status—not secret values.

## Connecting With People

Each Ship has one personal account. Invite someone through
[People](../integrations/contacts.md) to connect your Ships.
Contact invitations do not create local accounts or grant access to your connections.

## Password Recovery

**Forgot password?** can send a code through an eligible messenger you previously
connected. It does not ask for a username. Without an eligible messenger, sign in through
the **admin** link in the sign-in footer, then use **Settings → Sign-in → Personal sign-in** to
reset the personal password. This requires a direct administrator session; Ship cannot do
it on your behalf. Reset revokes personal sessions and disconnects your messenger accounts; sign
in again and reconnect them. Your account, files and running work remain.

To configure recovery for a Ship not yet linked to your verified identity, sign in
as the administrator and choose **Settings → Sign-in → Account recovery → set up recovery**.
Verify your email or sign in with the identity provider offered by your operator.

To recover administrator access, start from **My Ships** and complete the fresh
verification bound to that attempt. An ordinary owner session cannot reset the
administrator credentials. Passkeys are not supported.
