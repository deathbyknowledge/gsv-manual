# Command Map

[Find Any Command Or Capability](index.md)

This page maps common outcomes to the command family that owns them. Run `man <command>` for the exact syntax supported by the current GSV.

| Need | Start with |
| --- | --- |
| Find a command, skill, target, or integration | `man --search -- "goal"` |
| Inspect the current identity or GSV version | `whoami`, `id`, `hostname`, `uname` |
| Read, write, edit, search, or delete files | the built-in file tools; `ls`, `stat`, `cp` in Shell |
| Copy between GSV and a connected computer | `cp`, `targets` |
| Inspect or control work | `proc`, `ps` |
| Send, attach, silence, or route messages | `message` |
| Read or send email | `mail` |
| Create reminders or scheduled work | `sched`; use `crontab` for recurring shell commands |
| Discover a computer or browser target | `targets` or `devices` |
| Make an HTTP request | `net` |
| Use an MCP integration | `mcp` |
| Connect or remove an OAuth account | `oauth` |
| Search or maintain saved knowledge | `wiki` |
| Find or maintain reusable procedures | `skills` |
| Inspect or commit a GSV repository | `rgit` or `ripgit` |
| Run a composed JavaScript workflow | `codemode` |
| Generate text without starting a work loop | `llm` |
| Read an image | `img2txt` |
| Generate an image | `txt2img` |
| Transcribe audio | `stt` |
| Create spoken audio | `tts` |

## The Main Work Tools

When GSV is handling a request, its compact work surface is Read, Write, Edit, Delete, Search, Shell, and CodeMode. These are the normal first choice:

- Use Read, Write, Edit, Delete, and Search for direct file work.
- Use Shell for commands and the native command families above.
- Use CodeMode when one operation must coordinate several typed calls or integrations.

Choose the command that owns the action: `message` sends a message, `proc` manages work, `wiki` maintains saved knowledge, and `cp` copies across targets.

## Machine-Readable Output

Many commands support `--json`. Use it when another operation must consume the result, and use ordinary text when a person is reading it. Structured output keeps callers independent of presentation tables.

## Availability

A command may require a capability, connected target, configured provider, linked account, or human approval. Discovery output and command errors identify the missing prerequisite. The requested account, path, and destination stay unchanged until an authorized alternative is chosen.
