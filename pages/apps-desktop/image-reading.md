# Reading Images With `img2txt`

[Apps & Desktop](index.md)

`img2txt` reads an image from GSV or a connected target with Moondream 3.1 on
Cloudflare Workers AI. Moondream is the only image-reading implementation:
there is no selectable image-reading model and no Gemma fallback.

With no subcommand, `img2txt` returns a normal-length caption:

```bash
img2txt screenshot.png
```

Use a mode when the task is more specific:

| Mode | Use It For | Required Input | Normal Output |
| --- | --- | --- | --- |
| `caption` | A short, normal, or long general description. This is the default mode. | Image path | Text |
| `query` | A caller-written question or instruction about the image. | `--prompt` and image path | Text or requested structured format |
| `ocr` | Transcribing visible text or extracting document fields. | Image path; `--prompt` is optional | Text or requested structured format |
| `point` | Finding the center points of objects matching a phrase. | `--target` and image path | JSON with normalized `{x, y}` points |
| `detect` | Finding the bounding boxes of objects matching a phrase. | `--target` and image path | JSON with normalized `{xMin, yMin, xMax, yMax}` boxes |

## Command Syntax

```bash
img2txt [caption] [--length short|normal|long] [--stream] IMAGE
img2txt query --prompt TEXT [--reasoning] [--response-format FORMAT] [--schema JSON] [--stream] IMAGE
img2txt ocr [--prompt TEXT] [--response-format FORMAT] [--schema JSON] [--stream] IMAGE
img2txt point --target TEXT [--max-objects N] IMAGE
img2txt detect --target TEXT [--max-objects N] IMAGE
```

`IMAGE` may be a local path, `gsv:/path`, `target:/path`, or
`[target-with-colons]:/path`, matching the source syntax accepted by `cp`.

Examples:

```bash
# The default: a normal caption
img2txt /home/alice/photos/receipt.jpg

# An explicit long caption
img2txt caption --length long diagram.png

# Ask exactly what this task needs to know
img2txt query --prompt "Which setting is selected, and what warning is visible?" screenshot.png

# Transcribe all visible text in reading order
img2txt ocr scan.png

# Give OCR a task-specific extraction instruction
img2txt ocr --prompt "Extract only the invoice number, date, and total." invoice.png

# Locate every matching object
img2txt point --target "red button" controls.png
img2txt detect --target "person wearing a helmet" worksite.jpg

# Read directly from connected machine and browser targets
img2txt laptop:/home/alice/photos/receipt.jpg
img2txt ocr [browser:work]:/downloads/invoice.png
```

`query` deliberately has no default prompt. The caller chooses the question or
instruction. Use default `caption` when a general description is enough, and
use `query` when the wording should be specific to the task.

`ocr` does have an extraction-oriented default that asks for all visible text
in reading order while preserving line breaks and layout. Supply `--prompt`
when the desired extraction is narrower or needs a particular representation.
Non-streamed text trims only outer whitespace; meaningful internal spaces and
line breaks are preserved.

## Structured Output

`query` and `ocr` accept:

```text
--response-format text|json|xml|markdown|csv
```

The requested format is added to the caller's own instruction. JSON output is
parsed before it is returned. A JSON Schema can also be supplied:

```bash
img2txt query \
  --prompt "Extract the product name and displayed price." \
  --response-format json \
  --schema '{"type":"object","required":["name","price"],"properties":{"name":{"type":"string"},"price":{"type":"string"}},"additionalProperties":false}' \
  --json \
  product.png
```

`--schema` requires `--response-format json`. GSV checks the returned JSON
against the supplied schema and fails the command if the model returns invalid
JSON or a nonmatching value.

There are two different JSON controls:

- `--response-format json` asks Moondream to make the answer JSON.
- `--json` asks the shell command to print the complete GSV result envelope,
  including mode, model metadata, the text answer, and parsed `structured`
  output when applicable.

Without `--json`, query and OCR print only the answer. Point and detect always
print their structured result as JSON.

## Reasoning And Grounding

Query mode can request Moondream's visual reasoning:

```bash
img2txt query \
  --prompt "Which control should be used to save this form?" \
  --reasoning \
  --json \
  form.png
```

The complete JSON envelope can include reasoning text and grounding entries
that connect answer spans to normalized image points. Use `point` when the task
is simply to locate matching objects, `detect` when it needs their extents, and
query reasoning when the spatial evidence belongs to an answer.

## Streaming

Caption, query, and OCR can stream decoded UTF-8 text:

```bash
img2txt caption --length long --stream scene.jpg
img2txt query --prompt "Describe every visible chart trend." --stream dashboard.png
img2txt ocr --stream long-document.png
```

Streaming cannot be combined with:

- `--json`
- `--reasoning`
- non-text structured output or `--schema`
- `point` or `detect`

At the syscall boundary, streamed text travels in the `ai.image.read` response
body. The gateway shell collects those chunks into the final `shell.exec`
standard output, so callers receive ordinary command text rather than
Cloudflare's raw event stream.

## Options And Limits

The generation modes (`caption`, `query`, and `ocr`) support:

- `--max-tokens N`, from 1 through 28672.
- `--temperature N`, from 0 through 2.
- `--top-p N`, from 0 through 1.

The spatial modes (`point` and `detect`) support `--max-objects N`, from 1
through 500.

All modes support `--mime image/...` when the image MIME type cannot be
inferred from the file. GSV normally infers PNG, JPEG, WebP, and GIF paths.
Unsupported mode/option combinations fail instead of being silently ignored.

The old `--model` and `--input-format` options have been removed. They are not
compatibility aliases and will be rejected. Image reading always uses
`@cf/moondream/moondream3.1-9B-A2B`.

## Files, Targets, And Agents

An unqualified image path is resolved on GSV relative to the shell's current
directory. Prefix the path to read directly from another accessible target:

```bash
img2txt phone:/photos/receipt.jpg
img2txt query --prompt "What error is shown?" laptop:/tmp/screenshot.png
img2txt detect --target "submit button" [browser:work]:/screenshots/form.png
```

Target IDs containing colons use brackets so the target/path boundary stays
unambiguous. The remote file body streams directly into image reading without
creating a temporary GSV file. Access, filesystem-transfer capability, missing
file, disconnect, size mismatch, and cancellation errors are reported instead
of falling back to a local path. Use `cp` first only when a durable GSV copy is
itself useful.

Agents should choose the narrowest useful mode:

- Start with caption for general visual context.
- Write a task-specific query prompt when a decision depends on particular
  details.
- Use OCR for visible text and document extraction.
- Use point or detect when downstream work needs coordinates.
- Request structured output only when the next step benefits from a stable
  machine-readable shape.

The command requires the `ai.image.read` capability. Use `man img2txt` for the
live command synopsis and option list.
