# Recovery Sheet

[Settings And Recovery](index.md)

A recovery sheet is a piece of paper that keeps the Ship's identity on the
open network the person's own, even if their host can't help. It holds 12
words, a QR code and a sheet code.

- If the Ship ever moves to another host, the sheet takes its identity with it,
  so the people the person is connected with keep reaching them.
- If someone changes the Ship's identity without asking, the sheet can undo the
  change within 3 days.
- Anyone who has the sheet can take the Ship's identity. It belongs somewhere
  safe, like a passport.

## Making One

Only the person can make, replace or remove the sheet, in **Settings →
Recovery sheet**, with their password and a code emailed to them. Ship can't see
or change it: its syscalls refuse every process, whatever its capabilities.
Point the person to the section instead of trying a command.

The section appears once the Ship has its identity, which its first publish,
invitation or message request creates. Making a sheet never creates one. If
`atproto identity` prints `null`, there is no identity yet, and no sheet to
make.

It takes about five minutes and a printer, or a pen and paper. The person's
browser makes the words and shows them once; only the sheet's public half
reaches the Ship.

## The Words Stay On Paper

- Never ask for the words or the QR code, and never offer to keep them.
- If the words appear anyway, in a message, a photo or a file, don't repeat,
  read out or save them anywhere: not in memory, the wiki, files or
  responsibilities. Tell the person that sheet is no longer safe and ask them
  to make a new one in **Settings → Recovery sheet → make a new sheet**.
- The sheet code, such as `E35-BAN`, is safe to share. It tells the person
  which sheet is current; Settings and the sheet both show it.

## When Something Changes

The person gets an email whenever their sheet is made, replaced or removed,
with its sheet code. If they didn't make the change, they reply to that email
straight away. For 3 days, the host can undo the change with its recovery key,
and so can their previous sheet, if they had one. After 3 days nothing can, so
never suggest waiting.

A new sheet replaces the old one. For 3 days the old sheet can still undo the
change; after that it stops working. Suggest a new sheet when the person lost
theirs or someone else may have seen it.

Removing the sheet leaves the identity in the host's hands again. For 3 days
the current sheet can still undo the removal.

A reset gives the Ship a new identity; the old sheet stays with the old one, so
the person makes a new sheet afterwards.

## If Settings Refuses

| Settings says | What to do |
| --- | --- |
| That password isn't right | The person checks their password. Wrong passwords here count with the ones they type to sign in |
| Too many wrong passwords | Wait until the time it shows: 30 seconds at first, longer after each wrong one. Until then even the right password is refused, here and when signing in from the same place |
| That code isn't right | A code allows five tries; check the latest email |
| That code has expired | A code lasts 10 minutes; choose **continue** for a new one |
| We sent a code moments ago | Codes go out at most once a minute and five times an hour; wait until the time it shows |
| Add an email address to your account first | The person adds and verifies an email address for their account, then tries again |

## Using The Sheet

Moving the identity or undoing a change happens with atproto tools on the
person's own computer, following
[the recovery sheet guide](https://docs.gsv.space/how-to/recovery-sheet). Ship
never handles the words or the key, even to help.
