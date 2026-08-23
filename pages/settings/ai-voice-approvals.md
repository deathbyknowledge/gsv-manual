# AI, Voice & Approval Settings

[Settings](index.md)

## AI Profiles

An AI profile selects provider transport, model, reasoning behavior, output limit, context budget,
tool policy, and related generation settings. Personal and Work may use different profiles when
configured.

Standalone deployments normally use the user's own provider credentials. Managed installations may
use the platform inference Worker, whose operator chooses permitted providers/models and enforces
installation usage policy. The model selected in an account profile does not grant access to a
provider that the owning service has disabled.

Model requests stream through service bindings and Process boundaries. Text chunks and binary bodies
remain streams; intermediary Workers must not collect a complete provider response merely to forward
it.

## Context

Context byte budgets, compaction, system `context.d`, account `context.d`, and skills determine what
the model sees. Increasing a provider token limit does not make unbounded file reads safe; Read keeps
a default result bound and callers page deliberately.

## Voice And Gestures

Desktop voice and gesture settings are local. Microphone selection, local transcription, camera
permission, and gesture arming do not belong in the Gateway's provider profile. Packaged helpers and
models must match the Desktop version.

## Tool Approvals

Approval profiles map operations to `auto`, `ask`, or `deny`. Defaults ask for shell, deletion, and
MCP calls. Rules can match syscall, profile, target type, path, command, arguments, and risk tags.

Background and scheduled profiles cannot wait indefinitely for a person; an `ask` outcome becomes a
tool failure. Interactive approvals carry an exact request ID and may be answered from an authorized
client or linked direct-message surface.

## For Agents

If a model or tool fails, distinguish provider availability, budget, profile configuration,
capability, approval, and target availability before changing anything.
