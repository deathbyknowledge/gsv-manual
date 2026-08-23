# Machines & Targets

[Back to GSV Manual](../../index.md)

A machine extends GSV without moving its files, credentials, or hardware into the cloud. `gsvd` keeps
one authenticated driver connection open and implements target-routed primitives on that computer.

## Targets

- `gsv` is the Gateway's own execution target.
- A machine ID names a connected `gsvd` target.
- Browser-backed targets expose browser-local primitives through the extension.

Messaging adapters are transports, not generic hardware targets.

## Connecting A Computer

Desktop can guide machine enrollment and install the background daemon. The CLI can perform the same
service lifecycle through `gsv daemon ...`. The visible machine name and normalized machine ID are
stable; restarting Desktop does not create another machine.

Machine credentials are driver-bound and distinct from user login sessions. Revoking a machine does
not sign the user out, and signing out a UI does not implicitly destroy the machine identity.

## Pages In This Section

- [Targets, Execution & File Transfer](targets-copy.md)

## For Agents

Check that a target is online before depending on it. Keep platform-native computation and private
network access on the machine that owns them.
