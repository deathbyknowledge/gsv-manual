# Messaging, Email & Integrations

[Back to GSV Manual](../../index.md)

Adapters own third-party transport. MCP adds callable external tools. OAuth grants delegated access
to external accounts. The Kernel owns local identity, authorization, Process admission, Conversation
messages, and generic routing.

## Messaging

Telegram, WhatsApp, and Discord normalize provider actors, surfaces, messages, media, replay IDs, and
delivery outcomes. Linked private messages normally enter Personal Home. Group/channel/thread routes
remain explicitly bound.

## Managed Email

Managed installations can receive and send email through the platform email service. Inbound email
is stored in the owner's mailbox and summarized by the isolated mail pipeline. Personal receives only
a small untrusted notify-only event and decides whether to send a Message or remain silent.

Outbound version one sends one plain-text recipient or replies to an existing mailbox message. The
email Worker owns provider delivery, quotas, and idempotent attempt state. Standalone deployments do
not deploy or advertise managed delivery resources.

## MCP And OAuth

MCP servers expose tools/resources. OAuth grants an external account permission. One integration may
use both.

## Pages In This Section

- [Adapters, Identity Links & Routing](adapters-routing.md)
- [MCP Servers & OAuth Accounts](mcp-oauth.md)

## For Agents

An external provider name or message ID is not a GSV identity. Use the adapter's established link and
opaque destination records, and make externally visible delivery explicit.
