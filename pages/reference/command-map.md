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
| Find an earlier conversation message | `message search`, then `message history` |
| Read or send email | `mail` |
| Create reminders or scheduled work | `sched`; use `crontab` for recurring shell commands |
| Discover a computer or browser target | `targets` or `devices` |
| Make an HTTP request | `net` |
| Use an MCP integration | `mcp` |
| Connect or remove an OAuth account | `oauth` |
| Search or maintain saved knowledge | `wiki` |
| Search the web | `web search`, or the Search tool |
| Track promises, follow-ups, and delegated work | `r12y` |
| Connect with a person on another GSV | `contact` |
| Find or maintain reusable procedures | `skills` |
| Inspect or commit a GSV repository | `rgit` or `ripgit` |
| Run a composed JavaScript workflow | `codemode` |
| Generate text without starting a work loop | `llm` |
| Read an image | `img2txt` |
| Generate an image | `txt2img` |
| Transcribe audio | `stt` |
| Create spoken audio | `tts` |

## The Main Work Tools

When GSV is handling a request, its compact work surface is eight tools: Read, Write, Edit, Delete, Search, Shell, CodeMode, and Send. These are the normal first choice:

- Use Read, Write, Edit, Delete, and Search for direct file work and web search.
- Use Shell for commands and the native command families above.
- Use CodeMode when one operation must coordinate several typed calls or integrations.
- Use Send to reply. Text alone sends and keeps working; text with `yield` sends and finishes the run; `yield` alone finishes quietly. Send is the run control and the only one of the eight that is not a capability.

Every capability tool also takes an optional `purpose`: one sentence written for the person, saying why the call is being made. It is shown in an approval prompt and recorded in the ledger, and it never reaches the underlying command.

Choose the command that owns the action: Send replies, `proc` manages work, `wiki` maintains saved knowledge, and `cp` copies across targets. The Shell forms `message send` and `yield` remain the same actions as Send.

## Machine-Readable Output

Many commands support `--json`. Use it when another operation must consume the result, and use ordinary text when a person is reading it. Structured output keeps callers independent of presentation tables.

## Availability

A command may require a capability, connected target, configured provider, linked account, or human approval. Discovery output and command errors identify the missing prerequisite. The requested account, path, and destination stay unchanged until an authorized alternative is chosen.
