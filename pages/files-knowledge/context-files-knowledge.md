# Context, Skills & Knowledge Boundaries

[Files & Knowledge](index.md)

GSV gives people and agents several ways to keep information. Choosing the right place keeps agents useful and keeps the user's computer understandable.

## Quick Map

| Place | Use It For |
| --- | --- |
| `~/context.d/` | Short standing instructions and preferences that should shape an account or agent. |
| `~/skills.d/` | Reusable procedures, workflows, command recipes, and task-specific guardrails. |
| Library | Durable explanations, manuals, notes, imported reference material, and searchable knowledge bases. |
| Files | Documents, project folders, code, data, media, exports, and artifacts people should manage directly. |
| Conversations | Current work, discussion, decisions in progress, and temporary coordination. |

## Use Context For Standing Behavior

Context is standing behavior for an account or agent. It should be short and stable.

Good context examples:

- "Prefer concise status updates."
- "Use this account for package reviews."
- "This project uses TypeScript with double quotes."
- "Ask before sending external messages."

Poor context examples:

- A full API manual.
- Raw logs.
- An entire source tree.
- Temporary task notes.

Large or changing material belongs in Library or Files.

Use `~/context.d/` for account-wide standing context. Agent accounts can have their own context when they need a different role, responsibility, or style. Use package profile context only when the package owns a dedicated package-agent account.

Do not create `~/profiles.d/` trees for new profile behavior. Create or use the appropriate agent account instead.

## Use Skills For Reusable Procedures

Skills are small manuals for repeatable actions. A skill should answer: "When this kind of task appears, what should the agent do first, what should it inspect, and what should it avoid?"

Good skill examples:

- Reviewing a package before approval.
- Editing a package source tree safely.
- Operating a browser desktop target.
- Following a team-specific release checklist.

Poor skill examples:

- A complete product encyclopedia.
- A dump of every command a system supports.
- A duplicate of a Library manual page.
- One-off task notes that will not be reused.

Use `~/skills.d/` for user or agent skills. Packages may also expose skills from package source when their workflows should travel with the package.

Skills are disclosed progressively. The prompt-visible list should stay compact. Parent skills can describe a broad area and point to narrower child skills under their own `skills.d/`; the child skill should handle one concrete workflow.

Useful shell commands:

```bash
skills list
skills tree
skills search <query>
skills show <skill>
skills files <skill>
skills read <skill> <file>
```

Read the relevant skill before relying on it for a nontrivial workflow.

## Use Library For Reference Knowledge

Library is durable and searchable. Use it for procedures, explanations, design notes, source references, summaries of imported material, and knowledge bases an agent should consult when relevant.

Library should not replace a project directory. If the thing is a build artifact, code file, CSV, archive, or user document, keep it as a file and link to it from Library when useful.

Library is the right home for broad GSV explanations, product manuals, system maps, historical notes, and background material that would make context or skills too large.

## Use Files For Artifacts

Files are the right place for anything the user may open directly, edit with tools, copy across targets, or use outside a knowledge workflow.

Examples:

- Reports and exports.
- Project source.
- Configuration files.
- Images, recordings, and attachments.
- Data files.

## Use Conversations For Work In Progress

Conversation history is useful for review and continuity, but it is not the best storage location for finished facts or deliverables. When a task finishes, agents should point to the durable artifact.

## Updating Context And Skills

Humans can update context or skills directly, or ask an agent to do it. Good updates are small, named clearly, and easy to inspect later.

For context:

- Add one focused file under `~/context.d/` when a preference or standing instruction should persist.
- Keep each file short.
- Remove stale instructions instead of layering contradictory ones.
- Prefer plain language over implementation details unless the context is for a technical agent account.

For skills:

- Add a skill under `~/skills.d/<skill-name>/SKILL.md` for a reusable workflow.
- Use a clear `name` and `description` so agents can recognize when to open it.
- Keep the skill body procedural.
- Put longer references in files beside the skill only when they are truly needed.
- Use nested `skills.d/` only when a parent skill needs narrower child workflows.

Agents should not silently rewrite standing context or skills. Before changing them, confirm that the information is meant to persist. Preserve existing user-authored structure, make the smallest useful change, and explain what changed.

When a package ships context or skills for its own agent account, edit the package source instead of copying those instructions into a user's home unless the user explicitly wants a personal override.

## For Agents

If you need information later, place it somewhere visible and linkable. If you are unsure where it belongs, ask the user: "Should I save this as a file, a Library note, standing context, or a reusable skill?"

Use this rule of thumb:

- Behavior the agent should keep following: context.
- Procedure the agent may need to perform again: skill.
- Explanation or reference material someone may search for later: Library.
- Artifact someone may open, edit, copy, or run: file.
