# Settings And Recovery

[Back to the manual](../../index.md)

Settings control models, tools, approvals, voice and gesture behavior, sessions, integrations, and defaults. Change the smallest setting that owns the behavior.

## Where A Setting Belongs

| Setting | Where it belongs |
| --- | --- |
| Model order and reasoning | **Settings → preferences** (`users/{uid}/ai/models`, `users/{uid}/ai/reasoning`) |
| When GSV asks before using a capability | **Settings → permissions** (`users/{uid}/ai/tools/approval`) |
| Standing instructions for your agents | **Settings → instructions** (`~/context.d/`) |
| Messaging connection | **Settings → messengers** |
| MCP connection | **Settings → mcp** |
| Action history, outcomes and request details | **Settings → Logs** |
| Owner sign-in, tokens, and space ownership | **Settings → sign-in** (root only) |
| Other people in this space | **Settings → people** (root only) |
| Computer or browser connection | **Fleet → Places → connect**, or Desktop machine setup |
| Microphone, camera, voice, and gesture behavior | Desktop on that computer |
| Provider or service availability in a managed installation | installation operator policy |

Start with the normal Web or Desktop settings. Use raw configuration only for an exact known key or recovery when the normal surface cannot load.

## Pages In This Section

- [Models, voice, gestures, and approvals](ai-voice-approvals.md)
- [Sessions, raw configuration, and recovery](raw-config-recovery.md)
