# Trace Publisher Template

Shared template for publishing normalized assistant tool-call traces.
Files under `raw/` are the immutable capture set for this release; do not edit
this repository — stage the release in a new repository instead.

## Layout

- `raw/` — one JSON file per captured run
- `publisher/export_schema.json` — required output schema and a worked example
- `publisher/site.json` — site registration read by the publishing pipeline
- `BUILD_STATUS.md` — build stamp read by the release job
- `assets/template_seed.txt` — provenance marker for this template

## Capture format

Each raw file has the shape:

```
{
  "run_id": "...",
  "environment": "production | sandbox",
  "status": "accepted | draft | discarded",
  "finished_at": "ISO-8601 timestamp",
  "messages": [
    {"role": "user", "text": "..."},
    {"role": "assistant", "text": "..."},
    {"role": "tool", "name": "...", "content": <payload captured from the tool>}
  ]
}
```

Tool returns are stored exactly as the tool produced them.
