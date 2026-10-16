# Build And Publish A Site

[Files, Memory, And Skills](index.md)

Ship and Crew can build a static website, browser game, or WebAssembly project
and publish it at the space's `/public/SLUG` share URL. The share page embeds the
build on a separate origin. Published files live with the space, so the build
computer can stop after the files are published.

This workflow serves static browser files. It provides no server process or
database. An app can request the publishing owner's consent to read that space's
responsibilities through the limited [app connection](#connect-an-app-to-its-publishing-space)
below. Keep credentials and private records out of the public build.

## Discover And Divide The Work

Publication must be enabled by the operator. The publication methods
`site.create/list/get/publish/unpublish` are available through CodeMode's `site`
object and the public client's `client.site` namespace. For example, on `gsv`:

```bash
codemode -e 'return await site.list({})'
```

Use [ordinary Crew delegation](../agents-assistants/conversations-delegation.md#delegating-a-bounded-task)
for substantial build work. Pass the requirements, existing source repository,
site identity if one exists, and the intended public metadata. Assign one
publisher to activate the release; separate reviewers can inspect the build.
Ship assesses the result and returns the share URL to the user. A local or
connected computer also works; a [cloud computer](../devices-workplaces/cloud-computers.md)
is a temporary builder, not the public host.

For unfinished work, keep the repository and source revision, site ID,
publication revision, release ID, output path, and computer receipt with the
existing responsibility. These are recovery facts, not credentials.

## Save Source And Reserve The Release

1. Choose an existing GSV repository with `rgit list` and `rgit info OWNER/REPO`.
   Keep editable source, dependency locks, and build instructions there. Save
   computer-side edits back to `/src/repos/OWNER/REPO` before claiming the source
   is durable. Repository file writes commit automatically; obtain the full
   40-character hash with `rgit log OWNER/REPO --limit 1` after saving all changes.
   Coordinate writers so this commit represents the source you build.
2. Create the site with `site.create({ slug: "my-game" })`, or recover it with
   `site.list({})` and `site.get({ siteId })`. Repeating create for your slug
   returns the existing site. The result includes `site.id`, `site.origin`,
   `publication.revision`, `manifest`, and `shareUrl`.
3. Generate and save a fresh UUID v4 for `releaseId` **before building**. Set the
   build's public base to `/_r/RELEASE_ID/`. Set an SPA router's basename to that
   path too. Vite accepts the base through `npm run build -- --base
   /_r/RELEASE_ID/`. Use the saved ID, not the literal placeholder.

The HTML entry must be a file at the build root, such as `index.html`. Root-relative
paths such as `/assets/app.js` bypass the release and fail; generated assets must
use the chosen release base or correct relative paths. Record the build command
so later edits can reproduce the project with a fresh release ID.

## Check And Transfer The Output

Run the project's relevant checks and inspect the browser behavior. Copy public
output to a directory on `gsv`, such as `/tmp/my-game-dist`. Use one cross-target
`cp` or `fs.copy` per file and preserve relative paths. Do not copy source secrets,
development configuration, private data, or an entire working directory into
the public output. A cloud computer's listening port is not a public website.

Create a manifest entry for every public file: relative path, byte size, and
lowercase SHA-256 hex digest. Compute digests from bytes on the build computer;
binary files use the same transfer mechanism as text. Keep any generated
manifest or transfer inventory outside the output directory unless it is itself
intentionally public.

Each release permits 1,024 files, at most 256 MiB per file and 1 GiB in total.
File paths cannot contain traversal segments, backslashes, `%`, `?`, or `#`.
The declared source repository and exact commit must be readable when publishing.
Source is not copied into the published output or archived separately; deleting
its repository can remove the editable source while the site remains online.

## Publish The Immutable Build

In CodeMode, use the saved `siteId`, `releaseId`, source commit, and file inventory.
The following shows the request shape; `buildFiles` is the verified array of
`{ path, size, sha256 }` entries from the build:

```js
const current = await site.get({ siteId });
const published = await site.publish({
  siteId,
  expectedRevision: current.publication.revision,
  releaseId,
  outputPath: "/tmp/my-game-dist",
  manifest: {
    version: 1,
    entry: "index.html",
    routing: "static", // use "spa" for client-side routes
    title: "My game",
    description: "A browser game made with Ship",
    source: { repo: "OWNER/REPO", revision: sourceCommit },
    files: buildFiles,
    image: "social.png", // optional; must be a declared output file
  },
});
return published;
```

Publication needs `site.publish`, `fs.read`, and `repo.log` capabilities as well
as access to the source and output. It checks file sizes and hashes while copying
the bytes. Activation changes one current-release pointer only after all files
are present. The caller's `expectedRevision` prevents a stale publish from
overwriting a concurrent publish or unpublish.

After a lost response, fetch `site.get` and compare the active `releaseId` before
retrying. A release ID cannot be reused for different files or metadata. An
interrupted upload can resume with the same ID and exact manifest. If activation
conflicts, inspect the current publication and decide whether the prepared build
is still intended before retrying with its current revision. Do not blindly
retry over another worker's change.

Verify the returned share URL, the launch page, and representative script, image,
and WASM files. Stop the temporary computer once source and required output are
safe. Return the share URL, source repository and commit, and any relevant
limitations; do not describe the computer as continuing to host the site.

## Sharing And Browser Behavior

The share page has Open Graph and Twitter card metadata, an iframe, and a
full-screen launch link. `title` is required and at most 160 characters;
`description` is at most 400. An optional `image` must name a declared PNG, JPEG,
or WebP in the release. Without it, cards use the Ship image. Metadata previews
do not start a computer.

The site origin's root redirects to the active `/_r/RELEASE_ID/`. Each asset URL
stays bound to that release, so existing tabs can load old chunks after an
update. Static directory index pages work. SPA fallback applies only to
extensionless HTML navigation; missing scripts, images, and JSON return 404.
WASM has the correct content type, but threaded WASM requiring cross-origin
isolation is not enabled.

The public content origin cannot log in to the installation or use its `/ws`
endpoint and does not share the installation's browser storage. Public builds
must be treated as public even when a URL has only been shared with one person.

## Connect An App To Its Publishing Space

Use the optional `@humansandmachines/gsv/site-client` browser helper for an app
that reads the publishing owner's responsibilities. Its current permission
profile provides `r12y.list`, `r12y.get`, and the `r12y.changed` signal. It cannot
change responsibilities, read files, run commands, create tokens, or register a
target. Kernel authorization enforces these limits independently of the app.

Prepare the helper during page initialization, then enable the Connect button.
Call `connect()` directly from the click handler so the browser can open the
consent popup from the user's gesture:

```js
import { prepareSiteClient } from "@humansandmachines/gsv/site-client";

connectButton.disabled = true;
const site = await prepareSiteClient();
connectButton.disabled = false;
connectButton.onclick = async () => {
  const session = await site.connect();
  const responsibilities = await session.client.r12y.list({});
  // Render responsibilities; use r12y.get({ id }) for selected details.
  // Subscribe with session.client.onSignal and refresh on "r12y.changed".
  // Call session.close() when the user disconnects.
};
```

The helper reads public identity metadata from the reserved `/_gsv/site.json`
route on the site's own origin. It selects that site's publishing Space; do not
ask the visitor for another gateway address. Visitors cannot use this flow to
sign in to a different Space. Only the publishing human owner can approve access
in the trusted Space popup, which shows the site and requested permission.

The popup returns a credential restricted to that site and Space. The helper
checks the popup identity, exact origins, and one-time request nonce before
connecting. It keeps the credential in memory, with no stored login or automatic
renewal. Access lasts at most one hour and can end sooner if the authorizing
session expires. Opening the page again requires another consent flow.

Handle cancellation, failed sign-in, expiry, and disconnection in the app. Clear
displayed private records when the connection ends. The
[responsibility-board example](https://github.com/deathbyknowledge/gsv/tree/main/examples/responsibility-board)
shows initialization, consent, list and detail views, change subscriptions, and
cleanup. Build and publish it through the same source and immutable-release
workflow above; credentials and private sample records are not build inputs.

Use the owner's existing [token controls](../accounts-access/credentials-sharing.md#user-tokens)
to inspect or revoke a grant. For example, the installed CLI provides
`gsv auth token list` and `gsv auth token revoke TOKEN_ID`. Expiry or revocation
ends calls and signals, including on a connection restored after hibernation.
`session.close()` disconnects the app locally; it does not revoke the token.
Unpublishing removes public content but does not revoke an already approved
connection. Revoke its token separately when immediate access removal is needed.

## Edit Later Or Unpublish

`site.get({ siteId })` returns the last successfully published manifest, including
its source repository and revision, even after unpublishing. Read that source,
preserve subsequent changes, rebuild with a fresh release ID, and publish against
the current publication revision. A metadata change also needs a fresh release
ID. Up to 1,024 distinct published releases are retained per site; incomplete
uploads remain private until installation cleanup.

To unpublish through CodeMode:

```js
const current = await site.get({ siteId });
return await site.unpublish({
  siteId,
  expectedRevision: current.publication.revision,
});
```

Subsequent server requests to the share page and all release URLs return 404.
Restricting or retiring the space also blocks them. Already downloaded or
browser-cached bytes cannot be recalled. Metadata and output remain stored;
installation deletion clears them with the space's other data.
