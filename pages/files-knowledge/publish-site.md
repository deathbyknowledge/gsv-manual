# Build And Publish A Site

[Files, Memory, And Skills](index.md)

Build websites, browser games and interactive explanations as static browser
files. `sites` saves source in a GSV repository, builds on a Linux computer and
publishes at the space's `/public/SLUG` URL. The computer can stop afterward.

## Create And Edit

Run on `gsv`:

```bash
sites init my-game
```

This creates a Vite, React and TypeScript project at
`/src/repos/YOUR-ACCOUNT/my-game`. Edit it with ordinary file tools; writes commit
automatically. Keep source there so a later process can update the site without
the original build computer. Init never overwrites an existing project's files.

Use ordinary [Crew delegation](../agents-assistants/conversations-delegation.md#delegating-a-bounded-task)
for substantial build work. Give Crew the desired experience and source
repository. Keep the repository and computer receipt with the responsibility;
assign one publisher when multiple workers contribute.

## Build And Publish

Start a [cloud computer](../devices-workplaces/cloud-computers.md), or select an
accessible Linux computer with Node.js and npm. Then run on `gsv`:

```bash
sites publish my-game --target COMPUTER
```

Set the Shell timeout to 300000 ms for dependency installation and build. The command
builds an exact snapshot of the saved source, uploads the result and returns the
public share URL. It handles asset paths, file transfers, checksums and release
activation. An unsuccessful build leaves the previous publication online.
Cancellation stops its build session without stopping the computer. If cleanup
cannot finish, the error gives the temporary directory; stopping a cloud
computer discards those files.

Use `OWNER/REPO` for another accessible repository, or omit the repository when
running from inside `/src/repos/OWNER/REPO`. Save any computer-side source edits
back to GSV first: publishing builds the repository, not a computer's checkout.

Verify the share page and its behavior, then give the user the URL. Stop a
temporary computer when finished. The published output lives with the space;
the computer is not the host.

## Metadata And Other Frameworks

The starter includes `site.json`:

```json
{
  "slug": "my-game",
  "title": "My game",
  "description": "A browser game made with Ship",
  "routing": "spa",
  "output": "dist"
}
```

Set the title and description for sharing previews. Optional `image` names a
built PNG, JPEG or WebP; without it the preview uses the Ship image. Use
`routing: "static"` when the site should not fall back to HTML for client routes.

Other npm-based projects work too: provide `npm run build`, write `dist/index.html`
and use `GSV_SITE_BASE` as the public asset base. The starter's
Vite configuration already does this. A client-side router should use
`import.meta.env.BASE_URL` as its basename. Only built files become public;
keep secrets and private information out of them.

Hosting serves static files on an isolated origin. It does not run a server,
provide a database or connect the page to GSV. WASM is supported; threaded WASM
requiring cross-origin isolation is not. Releases allow 1,024 files, up to
256 MiB per file and 1 GiB total. Publishing does not change the source
repository's visibility.

## Update Or Unpublish

Edit the saved source and run `sites publish` again. Inspect or remove a site:

```bash
sites list
sites unpublish my-game
```

Unpublishing makes subsequent server requests return 404; downloaded or cached
bytes cannot be recalled. Source remains editable, and previous release files
are retained until installation cleanup. Up to 1,024 releases are retained per
site. Deleting the source repository does not take an existing publication down.

For direct integrations, CodeMode and the public client also expose
`site.create/list/get/publish/unpublish`. `site.get` returns the last published
manifest with its source repository and exact revision, even after unpublishing.
