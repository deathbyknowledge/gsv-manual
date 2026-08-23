# Adapters, Identity Links & Routing

[Messaging, Email & Integrations](index.md)

## Adapter Ownership

Each adapter Worker owns provider authentication, account state, webhook/socket lifecycle, event
normalization, media download, outbound formatting, retry ledgers, and provider-specific IDs. The
Gateway receives generic actor, surface, message, resource, and reply metadata.

Provider payloads are untrusted. The adapter authenticates and bounds them before parsing, then keeps
durable replay state so a retry cannot duplicate Process admission or provider delivery.

## Connecting And Linking

Connecting establishes the provider account or managed service. Linking proves which external actor
represents the signed-in GSV human.

- **Managed Telegram:** message the platform bot, receive a short-lived code, enter it in the signed-
  in installation, inspect the actor, and confirm. The platform owns the bot token. A linked actor has
  one active installation route and can be explicitly disconnected.
- **Standalone Telegram:** create a BotFather bot, connect its token to the user's adapter, then redeem
  the bot's link challenge.
- **WhatsApp:** pair the GSV adapter account as a linked device, then message it from the human's own
  account and redeem the separate identity-link code.
- **Discord:** connect a bot with the required message-content and delivery permissions, then link or
  address it according to direct-message/channel policy.

The first challenge-producing message is consumed by linking; send another message to start a
Conversation.

## Personal Home And Work

An unoverridden private DM goes to Personal Home. `/where` reports the selection. `/home` clears a
Work selection immediately and returns future messages to Personal.

Personal can offer a direct line to an owned interactive Work Process from the exact current DM run.
The adapter visibly labels that selection as a Work Session. This is a routing change for future
messages, not a replacement of Personal and not a redirect of the answer already being generated.

Groups, channels, and threads use persistent Kernel-owned mappings. Provider IDs never appear in
agent-facing commands; opaque GSV destination IDs and generic labels are used instead.

## Voice, Images, And Attachments

Standalone and managed adapter paths use the same resource contract. The adapter downloads provider
media once and streams the body into an immutable Process resource. Telegram voice messages, images,
video, and documents therefore reach the same model/history boundary as Web or Desktop attachments.
Transcription is metadata on the resource when available, not a substitute for retaining the audio.

Outbound media resolves the committed immutable reference lazily and streams it to the adapter. A
retry can read the agent-owned archive even after the originating Process has been killed.

## Delivery Guarantees

Inbound events and outbound messages use stable delivery IDs and payload fingerprints. Reusing an ID
for different content fails. Provider acceptance that cannot be confirmed is reported as ambiguous
rather than retried as a new logical message.

The exact run route wins for a direct reply. Background Personal events may use the most recently
authorized linked private destination. A disconnected client-origin run never silently falls back to
Telegram or WhatsApp.

## Approvals

Adapter approval prompts include the exact `hil[...]` request ID. A bare “approve” or a stale token
cannot authorize a different request.

## For Agents

Do not ask users to enter raw provider IDs or use hidden adapter commands. Personal may establish a
Work direct line itself; users always retain `/home` as the escape back to Personal.
