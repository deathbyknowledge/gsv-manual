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

See [Reading images with `img2txt`](../apps-desktop/image-reading.md) for modes, structured output, and target-qualified paths.

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

During an active interaction:

```bash
message attach report.pdf
message attach chart.png notes.txt
message send --message "I attached the report and supporting files."
```

Use `--mime` only when GSV cannot infer the type and only with one attachment. Attachment count and size limits are enforced before the message is committed.

## Media On Another Target

Commands that accept a target-qualified file can read directly from an authorized connected computer:

```bash
img2txt laptop:/Users/sam/Desktop/photo.jpg
stt phone:/recordings/note.m4a
```

Copy first only when keeping another saved copy is useful.
