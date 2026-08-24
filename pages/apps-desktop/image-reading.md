# Read Images With `img2txt`

[Web And Desktop](index.md)

`img2txt` can describe an image, answer a precise visual question, transcribe
visible text, or locate objects. Run `man img2txt` for the live option list.

## Start With The Smallest Useful Mode

```bash
# General description
img2txt photo.jpg

# Answer a specific question
img2txt query --prompt "Which setting is selected?" screenshot.png

# Transcribe visible text
img2txt ocr receipt.jpg

# Return object centers or bounding boxes
img2txt point --target "red button" controls.png
img2txt detect --target "person wearing a helmet" worksite.jpg
```

| Mode | Use it for | Output |
| --- | --- | --- |
| `caption` | A short, normal, or long general description | Text |
| `query` | A caller-written question or instruction | Text or a requested structure |
| `ocr` | Visible text or document fields | Text or a requested structure |
| `point` | Centers of matching objects | Normalized `{x, y}` points |
| `detect` | Extents of matching objects | Normalized bounding boxes |

Caption is the default. `query` requires `--prompt`; use it when wording the
question precisely will improve the answer. OCR has a general transcription
instruction unless a narrower `--prompt` is supplied.

## Read From Another Target

An image may be on GSV, a connected computer, or a browser target:

```bash
img2txt laptop:/home/alice/photos/receipt.jpg
img2txt query --prompt "What error is shown?" laptop:/tmp/screenshot.png
img2txt detect --target "submit button" [browser:work]:/screenshots/form.png
```

Target IDs containing colons use brackets. Reading a target-qualified path does
not first create a duplicate GSV file. Use `cp` when preserving a separate copy
is itself useful.

## Structured Results

`query` and `ocr` accept `--response-format text|json|xml|markdown|csv`. JSON
can also be checked against a schema:

```bash
img2txt query \
  --prompt "Extract the product name and displayed price." \
  --response-format json \
  --schema '{"type":"object","required":["name","price"],"properties":{"name":{"type":"string"},"price":{"type":"string"}}}' \
  product.png
```

Use `--response-format json` to request JSON from image reading. Add the shell
command's `--json` flag when you also need the complete result envelope and
metadata. Point and detect already return structured JSON.

## Long Answers And Reasoning

Caption, query, and OCR can stream text with `--stream`. Streaming cannot be
combined with the full JSON envelope, reasoning, schemas, non-text formats,
point, or detect.

Query mode can request visual reasoning with `--reasoning`. Use it when the
answer depends on spatial evidence, not merely because a longer answer sounds
useful.

## Limits And Failures

- `--mime image/...` supplies a MIME type when it cannot be inferred.
- Generation modes accept token, temperature, and top-p controls.
- Point and detect accept `--max-objects`.
- Missing files, unavailable targets, disconnects, unsupported images,
  permission failures, and invalid structured results fail explicitly.
- Cancellation stops the active read instead of silently retrying elsewhere.

The current identity needs the image-reading capability. Search with `man
--search -- "read an image"` if `img2txt` is unavailable.
