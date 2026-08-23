# Settings

[Back to GSV Manual](../../index.md)

Settings control model profiles, context limits, tools, approvals, voice behavior, authentication,
adapters, and runtime defaults. Start with the curated Web surfaces and use raw configuration only
for an exact documented key or recovery.

Settings have owners and scopes. A platform-managed inference choice is not the same setting as a
user's model profile; a Desktop microphone choice is local host configuration, not Kernel config.

## Main Areas

- AI providers, models, reasoning, context, and output limits.
- Tool visibility and human-approval policy.
- Desktop microphone, voice, and gesture behavior.
- Authentication and sessions.
- Managed-service operator configuration and limits.
- Low-level configuration inspection and recovery.

## Pages In This Section

- [AI, Voice & Approval Settings](ai-voice-approvals.md)
- [Authentication, Sessions & Raw Config](raw-config-recovery.md)

## For Agents

Name the setting, scope, owner, and rollback when changing behavior. Do not write standing context to
work around a runtime or configuration bug.
