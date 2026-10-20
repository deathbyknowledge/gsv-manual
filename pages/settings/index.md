# Settings And Recovery

[Back to the manual](../../index.md)

Settings control models, tools, approvals, voice input, sessions, integrations, and defaults. Change the smallest setting that owns the behavior.

## Where A Setting Belongs

| Setting | Where it belongs |
| --- | --- |
| Model order and reasoning | **Settings → preferences** (`users/{uid}/ai/models`, `users/{uid}/ai/reasoning`) |
| Language | **Settings → preferences → Language** (`users/{uid}/locale/language`), initially detected from the browser; Ship starts in it and follows explicit language requests and the language the person is speaking. The interface uses it when a translation exists: English or Spanish |
| Match system, Light or Dark appearance | **Settings → preferences → Appearance**, saved on this device |
| When Ship asks before using a capability | **Settings → permissions** (`users/{uid}/ai/tools/approval`) |
| Event-driven responsibilities Ship takes care of | **Settings → standing** |
| Standing instructions for your agents | **Settings → instructions** (`~/context.d/`) |
| Messaging connection | **Settings → messengers** |
| MCP connection | **Settings → mcp** |
| Action history, outcomes and request details | **Settings → Logs** |
| Personal password reset | **Settings → sign-in → Personal sign-in** (root only) |
| Set up administrator recovery | **Settings → sign-in → Account recovery → set up recovery** (root only) |
| Recover administrator access | **My Ships**; see [Password recovery](../accounts-access/credentials-sharing.md#password-recovery) |
| Your public profile | **your profile** at the bottom of **People** |
| Computer or browser connection | **Fleet → Places → connect**, or Desktop machine setup |
| Web microphone access | Browser site permissions; **record** in Chat starts capture |
| Web audio transcription | Your Ship's transcription configuration for the conversation process |
| Desktop microphone and local voice | Desktop on that computer |
| Provider or service availability in a managed installation | installation operator policy |

Start with the normal Web or Desktop settings. Use raw configuration only for an exact known key or recovery when the normal surface cannot load.

## Pages In This Section

- [Models, voice, and approvals](ai-voice-approvals.md)
- [Sessions, raw configuration, and recovery](raw-config-recovery.md)
