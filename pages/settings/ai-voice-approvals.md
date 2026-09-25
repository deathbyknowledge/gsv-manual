# Models, Voice, Gestures, And Approvals

[Settings And Recovery](index.md)

## Model Order

Text models form one ordered stack. The first entry answers first; if it cannot complete the reply, the next entry takes over. Edit the stack under **Settings → preferences → Model order**: **add model** connects a provider and key, **use first** moves an entry to the top, and the rows are labelled **First choice**, **Fallback 1**, and so on.

The stack is layered. A person's own models at `users/{uid}/ai/models` sit ahead of the installation's list at `config/ai/models`, which sits ahead of the deployment's base models (GSV Included on a managed installation, the Workers AI pair on a self-hosted one). Nothing replaces the base. An owner may reorder across all layers with `users/{uid}/ai/model_order`, and an agent or a piece of work may prefer one entry by its stable id through `users/{uid}/ai/preferred_model`. Reasoning is a separate preference, `users/{uid}/ai/reasoning`, from `off` to `xhigh`.

In a self-hosted installation, availability follows the credentials and providers the owner configured. In a managed installation, the service may offer a curated set of models and enforce usage limits; when the managed route is unavailable, the next entry in the stack is tried.

When generation behaves unexpectedly, inspect:

1. the active account and its model order;
2. the selected model and reasoning options;
3. context and output limits;
4. provider availability or allowance;
5. cancellation, timeout, or malformed provider output.

Search and bounded Read keep large files from consuming the context budget. Adjust context limits only when the task itself needs more model context.

## Voice And Gestures

Desktop owns microphone, camera, transcription, and gesture settings for that computer. Check operating-system permission, the selected microphone, and the hands-free state (Off, Ready, Listening) in Zen's **Voice and hands-free** control there.

Voice and gesture settings belong to Desktop on that computer; model profiles belong to the GSV account. See [Use voice and gestures](../apps-desktop/voice-gestures.md).

## Tool Approval

The approval policy decides whether an agent's tool call runs, asks the person first, or is refused. The installation default lives at `config/ai/tools/approval`; each person's override lives at `users/{uid}/ai/tools/approval` and is edited under **Settings → permissions**, where the actions are shown as **Allow**, **Ask**, and **Block**.

A policy is a default action plus ordered rules:

```json
{
  "default": "auto",
  "rules": [
    { "match": "shell.exec", "action": "ask" },
    { "match": "fs.*", "target": "targets/*", "action": "ask" },
    { "match": "mail.send", "action": "auto" }
  ]
}
```

- `action` is `auto`, `ask`, or `deny`.
- `match` is an exact capability name or a domain wildcard such as `fs.*`.
- `target` scopes a rule: omit it for every target, `gsv` for the installation itself, `targets/*` for any connected computer or browser, or one target id.
- The most specific target wins, then an exact match beats a wildcard, then list order.

The default policy lets native work in the installation itself run automatically: files, commands, and network requests on `gsv`, and web search anywhere. On a connected computer or browser it reads, searches, and transfers files automatically but asks before changing files, running a command, or making a network request. `sys.mcp.call` and `mail.send` ask everywhere. Mail is guarded separately: sending mail without asking needs an explicit `auto` rule for `mail.send`, even when the default is `auto`.

Every call carries an optional purpose, one sentence written for the person. The approval prompt leads with it and the ledger records it, so a person can judge a request without reading the arguments.

Interactive work can pause for an exact approval request. Scheduled and unattended work cannot rely on somebody eventually answering; an "ask" decision becomes a visible tool failure there.

Before loosening approval policy, identify the exact operation and why the current rule blocks a legitimate workflow. Prefer a narrow rule over disabling approval broadly.
