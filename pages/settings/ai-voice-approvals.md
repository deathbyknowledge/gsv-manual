# Models, Voice, Gestures, And Approvals

[Settings And Recovery](index.md)

## AI Profiles

An AI profile can select a provider and model, reasoning behavior, output limit, context budget, and tool policy. Different work identities may use different profiles when configured.

In a self-hosted installation, availability follows the credentials and providers the owner configured. In a managed installation, the service may offer a curated set of models and enforce usage limits. A profile selects among the providers available to that installation.

When generation behaves unexpectedly, inspect:

1. the active account and profile;
2. selected model and reasoning options;
3. context and output limits;
4. provider availability or allowance;
5. cancellation, timeout, or malformed provider output.

Search and bounded Read keep large files from consuming the context budget. Adjust context limits only when the task itself needs more model context.

## Voice And Gestures

Desktop owns microphone, camera, transcription, and gesture settings for that computer. Check operating-system permission, selected device, helper status, and armed/muted state there.

Voice and gesture settings belong to Desktop on that computer; model profiles belong to the GSV account. See [Use voice and gestures](../apps-desktop/voice-gestures.md).

## Tool Approval

Approval policy can automatically allow, ask, or deny operations. Rules may differ by action, target, path, command, arguments, or risk.

Interactive work can pause for an exact approval request. Scheduled and unattended work cannot rely on somebody eventually answering; an “ask” decision becomes a visible tool failure there.

Before loosening approval policy, identify the exact operation and why the current rule blocks a legitimate workflow. Prefer a narrow rule over disabling approval broadly.
