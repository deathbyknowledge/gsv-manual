# Troubleshooting

[Find Any Command Or Capability](index.md)

Start with the failed outcome, then inspect the smallest owner of that outcome. Avoid resetting unrelated parts of Ship.

## A Useful Sequence

1. Repeat the exact action only if it is safe and idempotent.
2. Read the complete error, including its code and missing requirement.
3. Check the current identity with `whoami` and `id`.
4. Check the relevant connection, helper, integration, or destination.
5. Check capability and approval requirements.
6. Change the smallest setting or connection that explains the failure.
7. Retry the original action and confirm the observable result.

## Common Failure Areas

| Symptom | Inspect first |
| --- | --- |
| A reply is missing | Messages, the active work activity, and `message current` |
| Reasoning or tools are missing | The selected Work activity, not only Messages |
| A computer command fails | `targets show <target>` and the computer's connection |
| A file cannot be read | connection, path, permissions, exact revision, and size limits |
| An integration tool is absent | `mcp status`, `mcp list`, OAuth status, and current capability |
| A website or web app seems out of reach | `targets search "browser"`; a connected [browser](../devices-workplaces/browser-targets.md) reaches signed-in sites without an integration |
| A message is not delivered externally | connected destination, route, attachment limits, and provider result |
| A contact message, message request or publish fails | `atproto identity` for an operator [takedown](../integrations/open-network.md#if-the-operator-takes-something-down), then `message delivery show` |
| A model fails | the model order in **Settings → Preferences**, provider availability, allowance, context size, and cancellation |
| An action is waiting | pending approval, active tool, connection, or queued work |
| An action was refused or asked for approval | the approval policy in **Settings → Permissions**, and the Logs entry's purpose and outcome |
| Something ran that should not have | **Settings → Logs**, then the policy that allowed it |

## Preserve The Original Error

An unavailable file revision stays an exact-revision error. An offline connection stays the selected connection until the user chooses another. An ambiguous provider result keeps the same logical delivery ID for status checks or safe retries.

## Recovery Actions Have Different Meanings

- **Abort** stops the current run.
- **Reset** clears a helper's activity while preserving the helper.
- **Kill** permanently removes that helper.
- **Sign out** ends a user session; it does not revoke a connected computer.
- **Disconnect** removes the selected integration or computer relationship; it should not reset unrelated accounts.

Inspect before choosing one.
