# Settings And Recovery

[Back to the manual](../../index.md)

Settings control models, tools, approvals, voice input, sessions, MCP servers, and defaults. Change the smallest setting that owns the behavior.

## Where A Setting Belongs

| Setting | Where it belongs |
| --- | --- |
| Model order and reasoning | **Settings → Preferences** (`users/{uid}/ai/models`, `users/{uid}/ai/reasoning`) |
| Language | **Settings → Preferences → Language** (`users/{uid}/locale/language`), initially detected from the browser; Ship starts in it and follows explicit language requests and the language the person is speaking. The interface uses it when a translation exists: English, Spanish or Brazilian Portuguese |
| Match system, Light or Dark appearance | **Settings → Preferences → Appearance**, saved on this device |
| Background stars | **Settings → Preferences → Appearance → Show stars**, saved on this device and applied to the app and sign-in |
| Interface size | Press **x** outside a text field to cycle through 75%, 85%, 100%, 150% and 200%; 75% uses compact message text and tighter spacing to fit more conversation on screen. Saved on this device |
| When Ship asks before using a capability | **Settings → Permissions** (`users/{uid}/ai/tools/approval`) |
| Event-driven responsibilities Ship takes care of | **Settings → Standing responsibilities** |
| Instructions for Ship and its helpers | **Settings → Instructions** (`~/context.d/`) |
| Messenger | **Settings → Messengers**, with WhatsApp first; Slack and Discord are marked Coming soon and cannot be connected or reconnected from Settings |
| MCP server | **Settings → MCP servers** |
| Actions, outcomes and request details | **Settings → Logs**; select an entry for details |
| Request account deletion | **Settings → Account**; email [hello@humansandmachin.es](mailto:hello@humansandmachin.es) for manual deletion during early access |
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

## Saving Preferences

Appearance is first in Preferences. Theme and background stars apply immediately on this device. Model order, reasoning, language and timezone share one **Save changes** bar that stays visible while scrolling. The language dropdown offers English, Spanish and Portuguese. Regional saved codes display the matching supported language without changing the saved value until you choose one.

Changes are checked before saving. If a save fails, the draft remains available to retry; individual preferences may already have saved. Leaving unsaved Preferences prompts first and keeps the draft in the open app if you continue. **Discard changes** restores the saved values. Reloading or closing the app warns before losing unsaved work.

**Settings → Account** explains that account deletion is handled manually during early access because a self-service option is not available yet. Email support to request deletion.

## Pages In This Section

- [Models, voice, and approvals](ai-voice-approvals.md)
- [Sessions, raw configuration, and recovery](raw-config-recovery.md)
- [Recovery sheet](recovery-sheet.md)
