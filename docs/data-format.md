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
source: typed
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

## Source Values

Use one source value per entry:

- `typed`
- `audio-record`
- `audio-upload`
- `photo-upload`
- `file-upload`

The source describes how the entry arrived, not what the entry is about.

## Metadata Rules

- `people` includes people central to the entry, not passing mentions.
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
