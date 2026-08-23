# MCP Servers & OAuth Accounts

[Messaging, Email & Integrations](index.md)

## MCP Servers

MCP servers expose tools and resources from systems such as issue trackers, databases, design tools,
and search services. GSV keeps MCP out of the model's always-expanded direct tool list. Agents inspect
the compact index and call selected MCP operations through CodeMode or the native `mcp` shell command.

This preserves the fixed Read, Write, Edit, Delete, Search, Shell, and CodeMode surface while making
large MCP catalogs available on demand.

Availability depends on the current run-as identity, server configuration, health, and capability.
Tool output is still untrusted data and MCP calls normally require approval.

## OAuth

OAuth grants GSV delegated access without asking a user to paste access tokens into chat. Start the
authorization flow from the owning integration surface, verify the account and requested scopes, and
revoke it there when no longer needed.

MCP and OAuth are complementary: OAuth establishes permission; MCP can expose operations that use it.

## Failure Checks

If an operation is missing or fails, distinguish:

1. the OAuth account is absent/expired;
2. the MCP server is offline;
3. tool discovery has not refreshed;
4. the run-as identity lacks capability;
5. approval denied the call;
6. the external service rejected it.

## For Agents

Never ask for an OAuth bearer token in a Message or file. Use the supported authorization flow and
report only account identity, scope, status, and next action.
