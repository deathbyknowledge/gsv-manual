# Messaging, Email, And Connected Services

[Back to the manual](../../index.md)

GSV can continue conversations through messaging apps, receive and send managed email, and use external services connected through MCP or OAuth. What is available depends on the installation and the accounts the user has linked. Messengers are connected under **Settings → messengers** and MCP servers under **Settings → mcp** in the Web app.

A website the user is already signed into does not need an integration. A paired browser reaches it through the user's own session; see [Use a browser target](../devices-workplaces/browser-targets.md). Prefer the browser when the goal is to read or act on a web app, and use MCP or OAuth when a service exposes operations GSV should call directly.

## Contacts

A Contact connects your Ship to a person on another GSV. Both sides retain
their own conversations and permissions while exchanging messages, structured
requests, and exact file revisions. See [Connect with another GSV](contacts.md).

## Messaging

Private messages from a linked Telegram, Slack, or Discord identity normally continue Ship. Groups, channels, and threads can be directed to selected work when authorized. WhatsApp is not currently available.

Connecting a provider account and proving which external person is the signed-in GSV owner are separate steps. See [Connect and route messaging](adapters-routing.md).

## Email

Managed email can receive, search, send, and reply to email. Ship receives new-mail summaries through restricted notification runs. See [Use email](email.md).

## MCP

MCP exposes tools from connected services such as issue trackers, databases, design systems, and search providers:

```bash
mcp list
mcp search "what you need"
mcp describe <server> <tool>
mcp call <server> <tool> --args-json '<arguments>' --json
```

See [MCP and OAuth](mcp-oauth.md).

## OAuth

OAuth lets a user authorize an external account without pasting an access token into chat. Use `oauth list` to inspect connections and `oauth help` for supported connection or removal flows.

## Pages In This Section

- [Connect and route messaging](adapters-routing.md)
- [Connect with another GSV](contacts.md)
- [Use email](email.md)
- [MCP and OAuth](mcp-oauth.md)
