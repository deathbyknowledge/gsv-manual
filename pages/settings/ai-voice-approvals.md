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

Web Zen has **record** and **stop** controls and a live waveform in the prompt.
The finished audio is transcribed through the space's Gateway using the current conversation process's
transcription configuration; the resulting text stays in the draft for review.
Browser site permission controls microphone access. No Desktop helper or
connected computer is required.

Desktop owns microphone, camera, transcription, and gesture settings for that computer. Check operating-system permission, the selected microphone, and the hands-free state (Off, Ready, Listening) in Zen's **Voice and hands-free** control there.

Local voice and gesture settings belong to Desktop on that computer; model profiles belong to the GSV account. See [Use voice and gestures](../apps-desktop/voice-gestures.md).

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
- A structured target selects existing target metadata: `{ "route": "instance", "platform": "browser" }` means GSV-provisioned browsers. Routes are `machine`, `adapter`, or `instance`; platform is optional.
- An exact target id wins over route-and-platform selectors, then route-only selectors, then `targets/*`, then unscoped rules. Then an exact capability match beats a wildcard, then list order breaks ties.

The default policy lets files, commands and network requests run automatically on `gsv` and GSV-provisioned cloud browsers, and permits web search anywhere. On connected personal computers or browsers, it reads, searches and transfers files automatically but asks before changing files, running commands or making network requests. `sys.mcp.call` and `mail.send` ask everywhere. Mail is guarded separately: sending mail without asking needs an explicit `auto` rule for `mail.send`, even when the default is `auto`.

Cloud browsers can retain website logins. To restrict their use, select **Cloud browsers** in Settings and choose **Ask** or **Block**, or set a rule for one target. The Kernel identifies cloud browsers from their instance route and platform; naming a connected device like a cloud browser does not change its permissions. Capability and ownership checks still apply. Existing custom policies retain their rules.

Every call carries an optional purpose, one sentence written for the person. The approval prompt leads with it and the ledger records it, so a person can judge a request without reading the arguments.

Interactive work can pause for an exact approval request. Scheduled and unattended work cannot rely on somebody eventually answering; an "ask" decision becomes a visible tool failure there.

Every approval card — Ship in Zen, delegated work, and Fleet — offers **always allow** alongside the one-time **allow** and **deny**; in Zen the `a` key does the same when you are not typing. It writes a single Allow rule for exactly that capability and target into the approval policy of the account the requesting process resolves — that account's own override when it has one, otherwise the owner's — then approves the pending request once. The rule names its scope, such as *run commands on my mac*, so allowing a command on one machine allows later commands there, not only the one shown. It appears in **Settings → permissions**, where it can be changed or removed, and takes effect from the process's next run; the current run keeps the policy it started with. **always allow** is offered only when the signed-in person can change settings and the policy can be edited without loss. Ordinary **allow** and **deny** decide one request only. Messenger “always” controls are unchanged: they remember the call for that process alone and write no rule.

The card's **why am I being asked?** link explains, in the Ship's own voice, why GSV asks before some tasks and offers to change it. The link never opens on its own, the model is not involved, and nothing it posts enters the conversation history or is recorded. The Ship says it does not need to ask for most of what it does and only asks before sensitive tasks; a box then asks whether to stop asking, with four choices:

- **Yes, turn on auto-approve for everything** allows all six kinds of sensitive task.
- **Only ask before deleting something or contacting someone** allows them all except deleting files and sending email, which stay on ask.
- **What are sensitive tasks?** lists the kinds the Ship asks about today — running commands on your machines, changing files on your machines, deleting files, fetching web pages through your machines, connected tools, and sending email — and offers **allow** or **ask** for each. Each row starts on what the policy does today, and saving writes rules only for the rows you changed.
- **No, keep asking.** closes the box.

Whichever option you pick appears as your own message, and every answer saves ordinary rules to the same account policy shown in **Settings → permissions**; a save that now allows the pending call approves it too. If the signed-in account cannot change settings, the box is replaced by “Sorry, but this user can't edit those settings,” with a **why?** that explains the account lacks the settings permission and the space owner can grant it or change the rules.

When a person asks you to change what you ask about, edit the account policy at `users/{uid}/ai/tools/approval` rather than describing the card back to them. Before loosening policy, identify the exact operation and why the current rule blocks a legitimate workflow, and prefer a narrow rule over disabling approval broadly.
