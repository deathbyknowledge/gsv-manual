# Settings And Recovery

[Back to the manual](../../index.md)

Settings control models, tools, approvals, voice input, sessions, MCP servers, and defaults. Change the smallest setting that owns the behavior.

## Where A Setting Belongs

| Setting | Where it belongs |
| --- | --- |
| Model order and reasoning | **Settings → Preferences** (`users/{uid}/ai/models`, `users/{uid}/ai/reasoning`) |
| Language | **Settings → Preferences → Language** (`users/{uid}/locale/language`), initially detected from the browser; Ship starts in it and follows explicit language requests and the language the person is speaking. The interface uses it when a translation exists: English or Spanish |
| Match system, Light or Dark appearance | **Settings → Preferences → Appearance**, saved on this device |
| When Ship asks before using a capability | **Settings → Permissions** (`users/{uid}/ai/tools/approval`) |
| Event-driven responsibilities Ship takes care of | **Settings → Standing responsibilities** |
| Instructions for Ship and its helpers | **Settings → Instructions** (`~/context.d/`) |
| Messenger | **Settings → Messengers** |
| MCP server | **Settings → MCP servers** |
| Actions, outcomes and request details | **Settings → Logs** |
| Personal password reset | **Settings → Sign-in → Personal sign-in** (administrator only) |
| Configure administrator recovery | **Settings → Sign-in → Account recovery → set up recovery** (administrator only) |
| Recover administrator access | **My Ships**; see [Password recovery](../accounts-access/credentials-sharing.md#password-recovery) |
| Your public profile | **your profile** at the bottom of **People** |
| Keep the Ship's identity on paper | **Settings → Recovery sheet** (the person only); see [Recovery sheet](recovery-sheet.md) |
| Computer or browser connection | **Work → Connections → connect**, or **Connect this computer** in the desktop app |
| Web app microphone access | Browser site permissions; **record** in Chat starts capture |
| Web app audio transcription | Your Ship's transcription configuration for the conversation |
| Desktop app microphone and local voice | The desktop app on that computer |
| Provider or service availability in a managed Ship | operator policy |

Start with the normal settings in the web app or the desktop app. Use raw configuration only for an exact known key or recovery when the normal surface cannot load.

## Pages In This Section

- [Models, voice, and approvals](ai-voice-approvals.md)
- [Sessions, raw configuration, and recovery](raw-config-recovery.md)
- [Recovery sheet](recovery-sheet.md)
