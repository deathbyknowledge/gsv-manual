# Packages & Extensions

[Back to GSV Manual](../../index.md)

Packages extend GSV. A package can add apps, commands, backend behavior, public routes, package agents, or other capabilities. Core surfaces such as Chat, Files, Terminal, Library, Repositories, Settings, and Crew are now native web-shell surfaces rather than package-backed first-party apps.

## What Packages Can Add

- App entrypoints that open in the desktop as framed package apps.
- Command entrypoints for Terminal or package command workflows.
- Backend entrypoints for package-specific services.
- Package agents with their own profile, context, and permissions.
- Public routes for webhooks or externally visible package surfaces.
- Source-backed workflows for development and review.

## Trust Model

Installing a package and trusting it are separate decisions. A package should only request the capabilities it needs. Review package source, manifest, public routes, and permissions before approving sensitive access.

## Pages In This Section

- [Trust, Entrypoints & Source Workflows](trust-entrypoints-source.md)
- [Catalogs, Remotes & Public Visibility](catalogs-visibility.md)

## For Agents

Package operations can affect system behavior. Before enabling, approving, or updating a package, identify the package, source, requested capabilities, and user impact.
