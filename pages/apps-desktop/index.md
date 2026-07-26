# Apps & Desktop

[Back to GSV Manual](../../index.md)

The GSV desktop is the browser-hosted work surface for the cloud computer. It keeps the session connected, hosts native GSV surfaces, opens package apps, and gives package app frames a safe way to communicate with the host.

## What The Desktop Owns

- Login and setup.
- The desktop frame, launcher, shell rail, and chat dock.
- Grouped inventory for Machines, Messengers, Integrations, and Applications.
- Opening, focusing, and closing native surfaces or package app frames.
- App previews and browser-hosted views.
- The bridge that lets package apps request host actions.
- Browser targets for automation that must happen inside the active web shell.

## What Apps Own

Native surfaces and package apps own their product work:

- Chat owns conversations and agent work.
- Files owns browsing and editing the filesystem.
- Terminal owns command sessions.
- Repositories owns ripgit browsing, history, diffs, pulls, and source inspection.
- Library owns durable markdown knowledge.
- Settings and Crew own system operation, configuration, accounts, agents, models, tasks, devices, messengers, integrations, and applications.
- Package apps own their own app-specific views and behavior inside a frame.

The desktop should feel like the place where work happens, not a dashboard about work.

## Pages In This Section

- [Desktop Surfaces & Apps](desktop-surfaces-and-apps.md)
- [Reading Images With `img2txt`](image-reading.md)

## For Agents

When a task is visual, window-based, or browser-local, use the desktop and browser target. When a task is about files, packages, settings, or devices, prefer the app that owns that work instead of relying on hidden commands.
