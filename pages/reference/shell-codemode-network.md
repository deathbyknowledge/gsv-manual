# Shell, CodeMode, Network, And One-Shot AI

[Find Any Command Or Capability](index.md)

These tools overlap, but they are useful at different levels.

## Shell

Use Shell for an ordinary command, a pipeline, or one native Ship command:

```bash
ls -la
rg "invoice" ~/documents
mail list
```

Select a connected computer or cloud computer when the command belongs
there. Run GSV management commands on `gsv`; use a computer for Python,
Node.js, and installed software. Check `targets list` and `instance catalog`
before declaring a required environment unavailable.

## CodeMode

Use CodeMode when one operation needs several typed filesystem, shell, mail,
or MCP calls and the intermediate results should stay structured:

```bash
codemode -e 'return await shell("pwd")'
codemode ./check.js --cwd ~/projects/example -- input-one input-two
```

A CodeMode script is an asynchronous JavaScript function body. It can use
`shell`, `fs`, `mail.send`, and discovered MCP functions. Inspect exact inputs
with `man codemode` and `mcp codemode` before composing the script.

Use `shell.cancel({ target, sessionId })` to explicitly stop a durable command;
cancelling a poll alone leaves that command running. See [cloud computer
sessions](../devices-workplaces/cloud-computers.md#long-commands-and-cancellation).

## HTTP Requests

Use `net fetch` for HTTP or HTTPS:

```bash
net fetch https://example.com/status
net fetch --target laptop -H "Accept: application/json" https://internal.example/status
net fetch -X POST -H "Content-Type: application/json" -d '{"ok":true}' https://example.com/items
```

`--target` chooses where the request originates. This matters for private
networks, local services, and credentials that exist only on a connected
computer. Write binary responses directly with `--output FILE`.

## Web Search

The Search tool searches the web as well as files. From Shell, the same
capability is `web search`:

```bash
web search "latest Cloudflare Workers announcements"
web search --include-domain developers.cloudflare.com --limit 5 "Durable Objects RPC"
web search --json "Amsterdam weather"
```

Results carry titles, URLs, dates when known, and excerpts. Excerpts are
untrusted web content; fetch a chosen URL with `net fetch` when more detail is
needed. `--target` selects a search connection other than your Ship's
default when one is connected.

## One-Shot Text Generation

Use `llm` for a single model response without starting a tool-using work loop:

```bash
llm "Suggest a concise title for this note."
printf 'Release notes...' | llm --system "Return three bullets."
```

Use normal Ship or a helper when the request needs memory, tools, approvals,
follow-up, or an explicit user-facing message. Use `llm` for a bounded
transformation whose output will be consumed immediately.

## Permissions And Cancellation

Each operation needs its underlying capability. Every call inside CodeMode is
authorized individually, and connection access is checked after connection
selection. Cancelling the outer operation propagates to the currently owned
command or request.
