# Authentication, Sessions & Raw Config

[Settings](index.md)

## Authentication And Sessions

Use setup/login, logout, token revoke, machine revoke, and adapter disconnect before low-level repair.
Browser/Desktop user sessions, machine driver credentials, and service bindings have different
lifecycles and should not be cleared as a group.

When a browser appears to log in and immediately disconnect, inspect the WebSocket response and
Gateway/Access routing rather than treating unrelated manifest or analytics errors as the cause.

## Raw Configuration

Raw config is useful when:

- an exact setting has no curated UI;
- a bad override must be removed;
- support identifies one key to inspect;
- the normal settings page cannot load.

Some state lives in dedicated SQLite stores or external services and is intentionally absent from
generic config. Do not invent a config key because a value exists conceptually.

## Safe Recovery

1. Identify the component that owns the state.
2. Record the non-secret old value.
3. Change or remove the smallest exact override.
4. Reconnect or restart only the affected component.
5. Test the original workflow.

Never edit a shipped schema migration or use an ad hoc constructor migration as recovery.

## For Agents

Do not guess raw keys, print auth material, or reset unrelated services. Explain why the normal path
is insufficient before using the recovery surface.
