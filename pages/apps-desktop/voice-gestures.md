# Use Voice

[Web And Desktop](index.md)

Web and Desktop turn speech into a message draft. Web records audio for
transcription through your Ship. Desktop transcribes locally as you speak.
Review the words before sending them.

## Web

In Chat, choose **record** and allow browser microphone access. The prompt
becomes a live waveform; your typed draft stays underneath. Choose **stop** when
finished. After **transcribing…**, the draft returns with the words added at its
cursor. Enter during recording stops it for review. **cancel** or Escape discards
recording or pending transcription and restores the typed draft. Recordings stop
automatically after five minutes and are limited to 25 MiB, or your Ship's smaller
limit.

The finished audio goes through your Ship to its configured transcription
provider. It is not attached to the message. If the connection drops or the tab
is hidden, capture stops and the audio stays in that tab. When ready, choose
**retry transcription**; returning to the tab or reconnecting does not upload it
automatically. Failed or empty transcriptions also retain the audio. You can
**download audio** to save it, or **discard recording** to remove it. Sending or
clearing typed text does not discard a finished recording awaiting retry.

Audio is kept in memory. Retry or download it before closing or reloading the tab,
signing out, or changing conversations or places. Late results cannot enter
another conversation.

Use HTTPS and a browser that supports microphone recording. If permission is
denied, enable the microphone in the browser's site settings. Provider or
permission errors come from your Ship's transcription configuration; web voice
does not need a connected computer or the Desktop helper.

## Desktop

In Chat, open **voice** and choose **listen**. Words appear in the draft as you
speak. Choose **pause** to stop while keeping the draft. Enter finalizes the
current segment, sends it, and keeps listening. Editing inside dictated text
stops dictation so later output cannot undo your correction.

Open **Settings → voice** to choose the microphone and configure Handsfree mode
and spoken replies. These preferences stay on
that computer. Leaving Chat stops local dictation and keeps the typed draft.

The first use asks for microphone permission and downloads a local speech model;
Desktop shows its progress. Choose the intended microphone if more than one is
available. After the model is ready, transcription runs on the computer without
a cloud transcription connection. On Windows, allow microphone access for desktop
apps in Privacy settings. The background machine service does not capture audio.

A session stops after ten minutes. If the speech helper fails or the connection
drops, words already displayed in the prompt remain available for editing.
Desktop does not retain the original audio for replay, so words not yet
transcribed may need repeating. Local voice includes a baseline CPU backend;
AVX2 and AVX-512 are optional.

## Handsfree Mode

Enable **Handsfree mode** under **Settings → voice**. Keep Desktop running and
signed in; any page can stay selected, and the window can be minimized or behind
another application. The talk shortcut starts recording; pressing it again
finishes and sends. **Hold to talk** instead sends when you release it. Wait for
the listening sound before speaking. The stop shortcut stops spoken replies and
cancels recording while retaining transcribed words.

Handsfree uses a separate voice draft and always sends to your personal Ship.
It leaves Chat's typed text, attachments and selected place untouched, including
while you view a People conversation or another process. Starting a recording
interrupts the current spoken reply without changing pages or focusing Desktop.

The small handsfree status panel follows you between pages. Cancelled recordings
stay under **review voice draft**, with edit, send and discard controls; starting
again continues that draft. Connection loss stops recording and keeps its text.
Failed sends remain available for explicit **retry** or **discard**. Reconnecting
does not send automatically. Sign-out and Quit warn before discarding unsent work.
Raw audio is not saved for replay.

**Read replies** can follow the voice conversation, read all new Ship replies or
stay off. Sending a typed message to your personal Ship ends the voice
conversation. Old history is not read on opening or reconnecting, and replies
arriving while recording stay in Chat without being spoken. Code blocks and
tables get a short cue to inspect Chat. Very long replies stop with a spoken cue
to read the rest in Chat. Speech is generated locally and follows
**Settings → Preferences → Response language**. Regional codes such as `es-MX`
use the matching language; changes saved there apply without restarting Desktop.
Without a saved preference, it uses the device's language when supported, otherwise English. Spoken replies support
English and Spanish; other preferences show an availability message in voice
settings while recording remains available.

The normal Desktop installation includes the speech runtime. On first use it
downloads and verifies the voice model, then generates speech locally from its
cache. Spoken replies require macOS 13 or newer on a Mac. Recording remains
available on Desktop's other supported macOS versions.

Choose **change** beside a shortcut, press the desired keys, then **save shortcuts**.
On Wayland, the desktop controls key assignment; use its shortcut settings or
bind the registered `talk` and `stop` actions in the compositor configuration.

## If Desktop Voice Does Not Work

1. Check **voice**; **input needs attention** explains the failure and offers
   **reconnect input** when needed.
2. Confirm microphone permission and the selected microphone.
3. Close applications that may have exclusive access to that microphone.
4. Start voice again. Text already in the draft remains available.

Voice input belongs to Desktop on that computer. Its machine connection is
separate; check **this computer** in the Ship menu for that connection. Typing,
clicking and ordinary message sending remain available when voice is unavailable.
