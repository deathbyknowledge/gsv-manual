# Sessions, Raw Configuration, And Recovery

[Settings And Recovery](index.md)

## Use The Normal Control First

Prefer the action that owns the relationship:

- sign out or revoke a user session;
- revoke a user token;
- disconnect a messenger or OAuth account;
- revoke or reconnect one computer;
- change the selected model or approval profile;
- reset or kill only the affected work item.

Change or revoke only the relationship that owns the problem.

## Raw Configuration

Raw configuration is appropriate when:

- the exact setting has no curated control;
- a known override must be inspected or removed;
- the normal settings page cannot load;
- a documented support procedure names the exact key.

Before changing it:

1. identify the exact key and scope;
2. record the non-secret old value;
3. understand the default when the key is absent;
4. make the smallest change;
5. reconnect only the affected component;
6. retry the original workflow.

Use keys discovered in the live configuration or named by a documented recovery procedure. Keep authentication material out of diagnostic output.

## Session Problems

If login succeeds but the UI immediately disconnects, inspect the actual connection error and session status. Browser manifest, analytics, content-blocker, and form warnings may be unrelated noise.

If another person's data appears after switching accounts, lock or sign out immediately and report a session-isolation failure. Preserve the evidence for diagnosis.

## Recovery

Use [Troubleshooting](../reference/troubleshooting.md) to isolate the failing action. A data-store repair, installation reset, or operator action should be the last step, not the first.
