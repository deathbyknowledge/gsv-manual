# Web & Desktop

[Back to GSV Manual](../../index.md)

GSV currently has two first-party graphical clients:

- the Web shell served by the Gateway;
- the cross-platform Rust Desktop client in the host workspace.

Both authenticate as a human, send canonical Conversation messages, synchronize committed Messages,
and may explicitly observe Process activity. Neither becomes the owner of agent state merely because
it renders it.

## Web

The Web shell owns setup/login, Personal Chat, Work inspection, Messages, Files, Terminal,
Repositories, Machines, Messengers, Integrations, Settings, and administrative surfaces. Its cached
queries are scoped to the authenticated session so signing out or switching users cannot retain the
previous user's private results.

## Desktop

Desktop owns its selected Process/Conversation, drafts, attachments, approvals, voice and gesture
presentation, and local same-user control endpoint. It can chat without `gsvd`; connecting the local
computer adds it as a machine target.

The packaged application includes matching `gsv`, `gsvd`, transcription and vision helpers, and the
gesture model weights. Desktop can enroll the computer, install the per-user daemon service, and
control it without requiring users to assemble components manually.

## Distribution Status

The repository can build an architecture-native macOS development application and ZIP. Public macOS
distribution still requires Developer ID signing, hardened-runtime entitlements, notarization, and
stapling. Host release artifacts cover the supported CLI/daemon platforms; a polished single-package
Linux and Windows Desktop release remains active product work.

## Pages In This Section

- [Surfaces, Desktop Host & Local Helpers](desktop-surfaces-and-apps.md)
- [Reading Images With `img2txt`](image-reading.md)

## For Agents

Treat Web and Desktop as presentations of shared protocol primitives. Keep visual state in the
client, authorization in the Kernel, and machine execution in `gsvd`.
