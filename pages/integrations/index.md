# Messaging, Email, And Connected Services

[Back to the manual](../../index.md)

Ship can continue conversations through messaging apps, receive and send managed email, and use external services connected through MCP or OAuth. What is available depends on the operator and the accounts the user has connected. Messengers are connected under **Settings → Messengers** and MCP servers under **Settings → MCP servers** in the web app.

A website the user is already signed into does not need an integration. A connected browser reaches it through the user's own session; see [Use a browser connection](../devices-workplaces/browser-targets.md). Prefer the browser when the goal is to read or act on a web app, and use MCP or OAuth when a service exposes operations Ship should call directly.

## Contacts

A contact connects your Ship to a person on another Ship. Both sides retain
their own conversations and permissions while exchanging messages, structured
requests, and exact file revisions. See [Connect with another Ship](contacts.md).

## Open Network

Each Ship has a public account on the open network, the AT Protocol network
that Bluesky and other apps read. Its public profile lives there, and Ship can
publish records and files the owner asks to make public, with their approval.
See [Publish on the open network](open-network.md).

## Messaging

Private messages from a connected Telegram, Slack, or Discord account normally continue Ship. Groups, channels, and threads can be directed to a selected helper when authorized. WhatsApp Business direct messaging is also available when the operator offers it.

Connecting a provider account and proving which external person is the signed-in Ship owner are separate steps. See [Connect and route messaging](adapters-routing.md).

## Email

Your Ship has its own address (`<handle>@gsv.space` on the public service; `mail address` prints the exact one), kept for the owner's convenience: sign-ups, verification codes, receipts, parcel tracking, bills and newsletters can go there instead of the owner's personal inbox. Ship reads, searches, sends and replies from it, and each new message becomes a `mail.received` responsibility for Ship. See [Use Ship's email address](email.md).

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
- [Connect with another Ship](contacts.md)
- [Use Ship's email address](email.md)
- [MCP and OAuth](mcp-oauth.md)
