# Anchor Data Format

Anchor stores user-owned journal data as plain Markdown.

Real data should live in a private folder or repository. The public Anchor repo should only contain fictional examples.

## Entry Files

Entries live in a flat `entries/` folder and use the date as the filename:

```text
entries/YYYY-MM-DD.md
```

Each entry has YAML frontmatter:

```yaml
---
date: YYYY-MM-DD
source_type: typed
source: [optional freeform provenance — e.g. "Memoir_untitled_v1", "driving home, Anzac Bridge"]
people: [Name One, Name Two]
place: Location
tags: [scene, reflection, work]
---
```

Then the entry body:

```markdown
# Monday, 13 April 2026

Entry text goes here.
```

## Source fields

Each entry has two source fields:

- `source_type:` — *how* the entry arrived. One of the enum values below. Always present.
- `source:` — *where* the entry came from, freeform. Examples: `Memoir_untitled_v1` (a Google Doc), `driving home, Anzac Bridge` (dictation context), `notebook page, blue ink`. Omit if not meaningful (e.g. a typed in-session entry with no external provenance).

`source_type` enum — describes the form of the original source material:

- `typed` — typed by user directly
- `dictated` — spoken aloud, transcribed live, no recording kept
- `audio` — voice recording (live or uploaded)
- `handwritten` — handwriting (typically arrived via photo)
- `imported` — text from an external document (Google Doc, .txt, etc.)
- `photo` — photograph of a non-text subject (a scene, an object)

Neither field describes what the entry is about — that's what `tags`, `people`, and `place` are for.

## Metadata Rules

- `people` includes people central to the entry — those the user interacted with or who feature in a scene. Excludes passing mentions and figures referenced thematically (e.g. a book's author the user is reading but did not meet).
- `place` is only filled when the location matters.
- `tags` should stay broad and useful for later retrieval.
- The entry body should preserve the user's voice. Clean transcription errors, but do not rewrite the memory.

## Monthly Files

Monthly summaries live in `monthlies/`:

```text
monthlies/YYYY-MM_monthly.md
```

The monthly file includes:

- moments worth remembering
- the shape of the month
- threads to carry forward
- dominant tags

The most important section is "Moments worth remembering". Each moment should be concrete enough that the user can reconstruct what happened without reopening the original entry.
