# Troubleshooting

[Find Any Command Or Capability](index.md)

Start with the failed outcome, then inspect the smallest owner of that outcome. Avoid resetting unrelated parts of GSV.

## A Useful Sequence

1. Repeat the exact action only if it is safe and idempotent.
2. Read the complete error, including its code and missing requirement.
3. Check the current identity with `whoami` and `id`.
4. Check the relevant target, work item, integration, or destination.
5. Check capability and approval requirements.
6. Change the smallest setting or connection that explains the failure.
7. Retry the original action and confirm the observable result.

## Common Failure Areas

| Symptom | Inspect first |
| --- | --- |
| A reply is missing | Messages, the active work activity, and `message current` |
| Reasoning or tools are missing | The selected Work activity, not only Messages |
| A computer command fails | `targets show <target>` and the machine connection |
| A file cannot be read | target, path, permissions, exact revision, and size limits |
| An integration tool is absent | `mcp status`, `mcp list`, OAuth status, and current capability |
| A message is not delivered externally | linked destination, route, attachment limits, and provider result |
| A model fails | selected profile, provider availability, allowance, context size, and cancellation |
| An action is waiting | pending approval, active tool, target connection, or queued work |

## Preserve The Original Error

An unavailable file revision stays an exact-revision error. An offline target stays the selected target until the user chooses another. An ambiguous provider result keeps the same logical delivery ID for status checks or safe retries.

## Recovery Actions Have Different Meanings

- **Abort** stops the current run.
- **Reset** clears a work item's activity while preserving the work item.
- **Kill** permanently removes that work item.
- **Sign out** ends a user session; it does not revoke a connected computer.
- **Disconnect** removes the selected integration or machine relationship; it should not reset unrelated accounts.

Inspect before choosing one.
