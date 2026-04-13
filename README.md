# Anchor
*Last updated: 13 April 2026*

A personal journaling and life-archive system. Built on one idea: a life worth living is worth recording — and records are only useful if you can get back inside them.

---

## What it does

Anchor solves three problems: capture, storage, and review.

**Capture** — it meets you where you are. You put the content in; the system handles formatting and tagging.

**Storage** — every entry is a plain Markdown file, owned by you, living in a folder you control. No proprietary format, no lock-in. Your archive goes wherever you go.

**Review** — because entries are structured, the system can synthesise them. Monthly reflections surface concrete moments, emotional arc, and threads worth carrying forward. Those feed into a yearly synthesis — the chapter of that year of your life.

For the full story of why Anchor works the way it does, see [VISION.md](VISION.md).

---

## How it works

You put the content in. Anchor formats it, tags it, and saves it to the right file. You don't manage files or frontmatter.

At the end of each month, Anchor reads all your entries and writes a monthly synthesis — concrete moments, the shape of the month, threads to carry forward. Those monthlies feed into a yearly synthesis, which becomes the raw material for a printed record of that year.

---

## Capture methods

- **Type** — paste typed notes directly
- **Voice transcript** — paste a transcript from a voice note recorded elsewhere
- **Upload a photo of notes** — handwritten entries, physical journal pages (untested in plugin)
- **Upload a file** — typed notes or documents

In-app audio recording is planned for the standalone app — see [VISION.md](VISION.md).

---

## Your data

All entries are stored as plain Markdown files. They live in a folder you control — not locked inside a proprietary format, not dependent on Anchor to read. If you ever want to leave, your files leave with you.

---

## Current state

Anchor is currently a set of Claude skills running through Cowork. There's no standalone app yet — that comes once the workflows are proven through use.

### Skills available now

| Skill | What it does | Trigger phrases |
|-------|-------------|----------------|
| Daily capture | Formats and files a journal entry | "add entry", "log this", "daily capture", "new entry" |
| Monthly reflection | Synthesises all entries in a calendar month | "monthly review", "monthly synthesis", "end of month" |

### How entries are stored

Each entry is its own file, named by date. Files live flat in an `entries/` folder — no nesting by month or year.

```
entries/
├── 2026-04-13.md
├── 2026-04-12.md
└── ...

monthlies/
├── 2026-04_monthly.md
└── ...
```

---

## Future direction

See [VISION.md](VISION.md).

---

## Repo structure

```
anchor/
├── plugin/                  # The plugin bundle
│   ├── skills/              # Skill definitions
│   └── system-guide.md      # File structures, tags, and formatting rules
├── product/                 # Product development (not part of the plugin)
│   ├── knowledge-base/      # Decisions and working principles
│   ├── user-flows/          # User flow documentation
│   ├── designs/             # Figma exports and wireframes
│   ├── research/            # User research
│   └── testing/             # Prototype feedback
├── decisions-system.md      # System design decision log
├── VISION.md                # Product vision — the why and where it's going
└── README.md                # This file
```
