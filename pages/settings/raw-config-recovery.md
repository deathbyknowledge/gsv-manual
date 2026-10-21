# Sessions, Raw Configuration, And Recovery

[Settings And Recovery](index.md)

## Use The Normal Control First

Prefer the action that owns the relationship:

- sign out or revoke a user session;
- revoke a user token;
- disconnect a messenger or OAuth account;
- revoke or reconnect one computer;
- change the selected model or approval profile;
- reset or kill only the affected helper.

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

## Keys Worth Knowing

Configuration is a key/value store. System keys live under `config/` and are visible at `/sys/config/*`; a person's overrides live under `users/{uid}/` at `/sys/users/{uid}/*`. Only the `ai/`, `ui/`, and `locale/` prefixes can be overridden per person; server and shell keys are system-only.

| Key | Purpose |
| --- | --- |
| `users/{uid}/ai/models`, `config/ai/models` | Ordered model entries, layered ahead of the base models |
| `users/{uid}/ai/model_order` | The owner's fallback order across all layers, by stable id |
| `users/{uid}/ai/preferred_model` | The entry an account or piece of work prefers |
| `users/{uid}/ai/reasoning`, `config/ai/reasoning` | Reasoning mode hint, `off` to `xhigh` |
| `users/{uid}/ai/tools/approval`, `config/ai/tools/approval` | Approval policy |
| `config/ai/context.d/*.md` | System instructions, concatenated in name order |
| `users/{uid}/locale/timezone` | The person's IANA timezone for routines and context |
| `config/server/name`, `config/server/timezone`, `config/server/version` | Ship name, default timezone, and read-only version |
| `config/shell/timeout_ms`, `config/shell/network_enabled`, `config/shell/max_output_bytes` | Native shell limits |

Read a key with `cat /sys/config/ai/reasoning` or `cat /sys/users/1000/ai/models`; write with a redirect to the same path. Credentials are stored beside an entry as `.../api_key` and are never returned by a list read.

## Session Problems

If login succeeds but the UI immediately disconnects, inspect the actual connection error and session status. Browser manifest, analytics, content-blocker, and form warnings may be unrelated noise.

If another person's data appears after switching accounts, lock or sign out immediately and report a session-isolation failure. Preserve the evidence for diagnosis.

## Recovery

Use [Troubleshooting](../reference/troubleshooting.md) to isolate the failing action. A data-store repair, Ship reset, or operator action should be the last step, not the first.
