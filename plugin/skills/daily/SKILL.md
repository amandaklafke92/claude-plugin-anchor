---
name: anchor-daily
description: >
  This skill should be used when the user says "add entry", "daily capture",
  "log this", "new entry", "add a daily entry", or provides a block of text,
  voice transcript, or notes to be recorded as a journal entry.
version: 0.3.0
---

# Anchor — Daily Capture Skill

## Job

Take raw input (pasted voice transcript, typed notes, or imported text) and format it as a dated entry file. Save to the `entries/` folder. Do not synthesise. Do not over-tag. Just format and file.

---

## Input

The user will provide one of the following:
- A pasted voice transcript
- Typed notes
- Imported text with a source noted

The user may or may not specify the date.

- If the user provides a date, use it.
- If no date is given, use the date of the current session and flag it with a note below the heading: *[date autoselected — correct if needed]*
- Do not infer dates from surrounding context or ask the user for it — use today and flag it.

---

## File naming

```
entries/YYYY-MM-DD.md
```

Example: `entries/2026-04-13.md`

---

## Entry file structure

```
---
date: YYYY-MM-DD
source_type: [typed / dictated / audio / handwritten / imported / photo]
source: [optional freeform provenance — e.g. "Memoir_untitled_v1", "driving home, Anzac Bridge". Omit if not meaningful.]
people: [First Last, First Last — or leave blank]
place: [location — or leave blank]
tags: [tag1, tag2, tag3]
---

# [Weekday, DD Month YYYY]

[Entry content — preserve the user's exact voice and wording]
```

`source_type:` is always present. `source:` is freeform — populate when there's meaningful provenance (imported document name, dictation context, audio file label) and omit otherwise. `place:` is always present as a field, even if blank.

**`people:` rules:**
- Include people the user interacted with or who feature in a scene.
- Exclude passing mentions.
- Exclude authors, public figures, or historical names referenced thematically but not interacted with (e.g. a book's author the user is reading). These live in the entry body, not in `people:`.

If a file already exists for that date (a second entry on the same day), append the new entry below a `---` divider with its own heading.

---

## Source fields

Two fields work together:

**`source_type:`** — required, one of:
- `typed` — typed by user directly
- `dictated` — spoken aloud, transcribed live, no recording kept
- `audio` — voice recording (live or uploaded)
- `handwritten` — handwriting (typically arrived via photo)
- `imported` — text from an external document (Google Doc, .txt, etc.)
- `photo` — photograph of a non-text subject (a scene, an object)

**`source:`** — optional freeform string. Populate when there's meaningful provenance worth preserving:
- Imported document: the document name (e.g. `Memoir_untitled_v1`)
- Dictation: context where dictated (e.g. `driving home, Anzac Bridge`, `walking, Centennial Park`)
- Audio: file label or recording context
- Handwritten/photo: what was photographed or written on (e.g. `notebook page`)

Omit when there's nothing meaningful to add — e.g. a typed in-session entry.

---

## Tag system

Tags are categorical and thematic — not hyper-specific. Each entry should have 5–10 tags. Do not create new tags without flagging them to the user first.

### Entry type
- `#scene` — a moment captured vividly (dialogue, interaction, setting, sensory detail)
- `#reflection` — thinking through something, processing, introspection
- `#fact` — what happened (neutral capture, events, logistics)
- `#dialogue` — interesting conversation or exchange worth remembering
- `#turning-point` — felt significant, might matter later
- `#character` — interesting person or interaction worth remembering

### Life domains
- `#work` — career, projects, job stuff
- `#travel` — movement, places, geography
- `#relationship` — people, conversations, connections
- `#health` — body, sleep, exercise, energy
- `#mental-health` — therapy sessions, mood patterns, clinical self-reflection
- `#learning` — new ideas, skills, insights
- `#rest` — downtime, leisure, recharge
- `#social` — friends, gatherings, community

### Emotional / thematic
- `#beauty` — moments of aesthetic or emotional beauty
- `#struggle` — hard things, frustration, confusion, difficulty
- `#joy` — happiness, lightness, fun, laughter
- `#grief` — loss, sadness, mourning
- `#wonder` — curiosity, amazement, discovery
- `#creative` — making something, artistic moments

### Meta
- `#planning` — thinking ahead, setting intentions
- `#review` — looking back, assessing
- `#note-to-self` — reminders, lessons, things to remember

---

## Process

1. Identify or confirm the date of the entry
2. Determine the correct `source_type:` value from the input method
3. Populate `source:` with freeform provenance if meaningful (imported doc name, dictation context, etc.). Omit otherwise.
4. Format the entry content — preserve the user's exact voice (see fidelity rules below)
5. Suggest 5–10 tags from the tag system above — user will approve or trim
6. Populate `people:` with anyone central to the entry. Leave blank if none.
7. Populate `place:` with the meaningful location. Leave blank if not present or incidental.
8. Write the entry to `entries/YYYY-MM-DD.md`. If the file already exists, append below a `---` divider.
9. Output the formatted entry to confirm what was saved.

---

## Fidelity rules

Preserve the user's voice. The goal is light cleanup, not rewriting.

**Acceptable:**
- Correcting grammar and punctuation
- Fixing clear transcription errors (e.g. "Down Hall" → "Town Hall")
- Splitting one long run-on paragraph into two where it aids readability — without changing any words
- Reordering sentences within a paragraph only when the original order was clearly scrambled — flag this to the user rather than doing it silently

**Not acceptable:**
- Rewriting sentences, even if the result is "better" writing
- Replacing the user's phrasing with cleaner alternatives
- Condensing or cutting content
- Smoothing out rawness, informality, or repetition — these are intentional
- Completing a sentence that trails off — leave it trailing
- Inferring emotions or motivations not explicitly stated

If a word or phrase from audio cannot be reliably transcribed, mark it `[unclear]`. The user can correct it before saving.

**Example — not acceptable:**

Original: *"I was feeling nervous because in the past I haven't had the best experiences at networking events. Always being dragged there by my ex-boss to talk about recruitment, which I really couldn't care less about."*

Over-edited: *"I'd been nervous about going. In the past, networking events had always been a drag — recruited by my ex-boss to talk about recruitment (which I couldn't care less about)."*

The second version is tighter, but it's no longer her voice.

---

## Rules

- Do not synthesise or analyse — this is capture, not review
- Do not create new tags without flagging to the user first
- If the date is uncertain, flag it: *[date autoselected — correct if needed]*
- If the input covers multiple distinct moments or topics, ask the user whether to split into separate files or keep as one
