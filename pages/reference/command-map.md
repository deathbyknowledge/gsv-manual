# Command Map

[Find Any Command Or Capability](index.md)

This page maps common outcomes to the command family that owns them. Run `man <command>` for the exact syntax supported by the current Ship.

| Need | Start with |
| --- | --- |
| Find a command, skill, connection, or integration | `man --search -- "goal"` |
| Inspect the current identity or Ship version | `whoami`, `id`, `hostname`, `uname` |
| Read, write, edit, search, or delete files | the built-in file tools; `ls`, `stat`, `cp` in Shell |
| Copy between Ship and a connected or cloud computer | `cp`, `targets` |
| Inspect or control work | `proc`, `ps` |
| Hand over the current working context | `proc compact --summary '...'` from Ship or the active helper |
| Send, attach, silence, or route messages | `message` |
| Connect the owner's messenger using a code | `messenger list`, `messenger setup ADAPTER`, `messenger connect ADAPTER < code.txt` |
| Find an earlier conversation message | `message search`, then `message history` |
| Find Ship's email address, read, or send email | `mail` |
| Create reminders or routines | `sched`; use `crontab` for recurring shell commands |
| Discover a computer or browser | `targets` or `devices` |
| Start or reuse a cloud browser and wait for readiness | `instance start browser --request-id ID --wait` on `gsv` |
| Start an on-demand computer for documents, data, media, or software | [`instance start computer --request-id ID --wait`](../devices-workplaces/cloud-computers.md) on `gsv` |
| Stop a cloud computer after saving needed files | `instance stop ID --wait` on `gsv`; its disk is temporary |
| Save and stop a cloud browser, waiting for release | `instance stop ID --wait` on `gsv`; a failed save leaves it running |
| Retry saving website state | `browser profile save ID` on `gsv`; inspect the returned save status |
| Inspect or forget remembered browser logins | `browser profile list`, `browser profile get <profile-id>`, `browser profile delete <profile-id>`; deletion stops its browser and forgets the state |
| Connect a computer or browser for the owner | `targets pair` |
| Make an HTTP request | `net` |
| Use an MCP integration | `mcp` |
| Connect or remove an OAuth account | `oauth` |
| Search or maintain saved knowledge | `wiki` |
| Search the web | `web search`, or the Search tool |
| Track promises, follow-ups, and handed-off work | `r12y` |
| Find a person's Ship by handle or address | `contact find` |
| Connect with a person on another Ship | `contact` |
| Publish a public record or file, print the Ship's DID, or see what the operator took down | [`atproto`](../integrations/open-network.md) |
| Find or maintain reusable procedures | `skills` |
| Inspect or commit a Ship repository | `rgit` or `ripgit` |
| Run a composed JavaScript workflow | `codemode` |
| Generate text without starting a work loop | `llm` |
| Read an image | `img2txt` |
| Generate an image | `txt2img` |
| Transcribe audio | `stt` |
| Create spoken audio | `tts` |
| Report a bug or suggestion to your operator | `feedback` (when configured) |

## The Main Work Tools

When Ship is handling a request, its compact work surface is eight tools: Read, Write, Edit, Delete, Search, Shell, CodeMode, and Send. These are the normal first choice:

- Use Read, Write, Edit, Delete, and Search for direct file work and web search.
- Use Shell for commands and the native command families above.
- Use CodeMode when one operation must coordinate several typed calls or integrations.
- Use Send to reply. Text alone sends and keeps working; text with `yield` sends and finishes the run; `yield` alone finishes quietly. Send is the run control and the only one of the eight that is not a capability.

Every capability tool also takes an optional `purpose`: one sentence written for the person, saying why the call is being made. It is shown in an approval prompt and recorded in Logs, and it never reaches the underlying command.

Choose the command that owns the action: Send replies, `proc` manages work, `wiki` maintains saved knowledge, and `cp` copies across connections. The Shell forms `message send` and `yield` remain the same actions as Send.

## Machine-Readable Output

Many commands support `--json`. Use it when another operation must consume the result, and use ordinary text when a person is reading it. Structured output keeps callers independent of presentation tables.

## Availability

A command may require a capability, connection, configured provider, linked account, or human approval. Discovery output and command errors identify the missing prerequisite. The requested account, path, and destination stay unchanged until an authorized alternative is chosen.

## External CLI Name

The installed host CLI is `gsv`. Examples such as `gsv login`, `gsv ship`,
`gsv pair` and `gsv desktop` refer to that external CLI. Inside Ship's shell,
continue using the native commands listed above without adding a `gsv` prefix.

When a person asks how to do something from their own terminal, point them to
the CLI's own commands:

- `gsv login SPACE` signs in, `gsv status` checks sign-in and pairing, and
  `gsv logout` signs out.
- `gsv ship "MESSAGE"` talks to Ship; `gsv ship` alone opens a prompt.
- `gsv contacts`, `gsv requests` and `gsv mail` cover people and mail.
- `gsv work` lists running work; `gsv work show ID`, `open`, `stop`, `reset`
  and `end` act on one piece of it.
- `gsv routines`, `gsv memory` and `gsv activity` cover schedules, the wiki and
  recent activity.
- `gsv files` and `gsv places` reach files and connected places, and
  `gsv run [--on PLACE] COMMAND` runs one command, including a native command
  on Ship such as `gsv run r12y list`.

The older `gsv chat` still works as an alias of `gsv ship`. `gsv shell`,
`gsv proc`, `gsv auth login` and remote `gsv config` were replaced; they print
the new command instead of running.
