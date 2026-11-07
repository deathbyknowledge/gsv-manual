# Images, Audio, And Attachments

[Files, Memory, And Skills](index.md)

Media stays a file. Messages and activity carry exact file references, and authorized readers load the bytes when needed.

## Read An Image

```bash
img2txt photo.jpg
img2txt query --prompt "What error is visible?" screenshot.png
img2txt ocr scan.png
img2txt detect --target "submit button" screenshot.png
```

See [Reading images with `img2txt`](../apps-desktop/image-reading.md) for modes, structured output, and connection-qualified paths.

## Generate An Image

```bash
txt2img -o illustration.png "A small sailing ship at dusk"
```

Run `man txt2img` for available size, format, and generation options.

## Transcribe Or Create Audio

```bash
stt voice-note.m4a
tts -o reply.wav "The appointment is confirmed."
```

Use `man stt` or `man tts` for supported options. A voice message received through a messenger remains an audio resource even when a transcription is available.

## Attach Files To A Reply

During an active interaction, stage files and then send with the Send tool, or from Shell:

```bash
message attach report.pdf
message attach chart.png notes.txt
message send --message "I attached the report and supporting files."
```

A document on a connected computer can be attached directly when that computer's daemon is current; older daemons can attach only images from that computer.

Use `--mime` only when Ship cannot infer the type and only with one attachment. Attachment count and size limits are enforced before the message is committed.

## Open A File From A Chat

A file that arrives in a chat opens in a read-only viewer instead of downloading straight away. Select the filename under the message.

Text, code, JSON and CSV appear as plain text, Markdown renders as it does in a message, and a PDF opens in your browser's own viewer. In the Desktop app an image keeps opening in the app's native preview.

Download stays in the viewer header, so nothing is trapped behind it.

Formats the viewer will not interpret download directly — HTML, SVG and XHTML among them, since they can carry scripts — as do text files larger than 1 MiB and types the viewer does not handle.

An open viewer stays put: it survives scrolling past, or paging away from, the message that carried the file.

## Media On Another Connection

Commands that accept a connection-qualified file can read directly from an authorized connected computer:

```bash
img2txt laptop:/Users/sam/Desktop/photo.jpg
stt phone:/recordings/note.m4a
```

Copy first only when keeping another saved copy is useful.
