# Desktop Surfaces & Apps

[Apps & Desktop](index.md)

## Chat

Chat is the conversation surface. Use it to talk with personal agents, custom agents, package agents, and background-capable assistants. In the current web shell, Chat appears as a dock beside the desktop or active page. It is where users can review messages, attach media, approve tools, and continue previous work.

## Files

Files is the filesystem surface. Use it to browse `/home`, project folders, generated artifacts, and other file-backed locations the user can access.

## Terminal

Terminal is the command surface. Use it when the user needs shell commands with visible output, or when an operation does not have an app control.

Before running a command, check the target. A command on the cloud GSV target is not the same as a command on a local laptop, browser target, or adapter target.

## Repositories

Repositories is the ripgit source surface. Use it to browse visible repositories, inspect files, search source, review history and diffs, pull upstream changes, and understand package or manual source state.

## Library

Library is the knowledge product. Use it to build durable manuals, reference collections, imported knowledge bases, and linked notes that agents and people can search later.

## GSV Console

The GSV console is the native system settings and operations area. It is split across Settings, Crew, Runtime/Tasks, and the grouped object pages for Machines, Messengers, Integrations, and Applications. Use it for:

- Runtime and process inspection.
- Devices and machine lifecycle.
- Applications, package trust, and updates.
- Integrations and MCP servers.
- Access, tokens, and identity links.
- Settings and advanced recovery.

## Previews

Previews let users inspect running app views, generated pages, package output, or browser-hosted surfaces without leaving the desktop. If a preview is interactive, keep track of whether it is showing cloud state, local device state, or browser state.

## Host Bridge

Package apps run inside desktop app frames and communicate with the host through a bridge. In user terms, the bridge is what lets an app ask GSV to open files, show status, call backend work, or interact with desktop chrome without taking over the whole computer.

For source-level details, use [Advanced System Internals](../advanced-system-internals/index.md).
