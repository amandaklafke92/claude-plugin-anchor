# Anchor — Plugin Development Context

Anchor is a Cowork plugin that gives Claude three journaling skills: daily capture, weekly synthesis, and monthly reflection. Entries are stored as plain markdown files in a user-specified folder.

**Core design principle:** text records should reconstruct lived experience, not summarise it.

---

## Repo structure

```
anchor/
├── plugin/              # The plugin bundle — what users install
│   ├── skills/
│   │   ├── daily/SKILL.md
│   │   ├── weekly/SKILL.md
│   │   └── monthly/SKILL.md
│   └── references/
│       └── anchor-context.md
├── product/             # Product development work (not part of the plugin)
│   ├── knowledge-base/  # Specs, decisions, and working principles
│   ├── user-flows/      # User flow documentation and prototype screenshots
│   ├── designs/         # Figma exports and wireframes
│   ├── research/        # User research and competitive notes
│   └── testing/         # Prototype feedback and test records
├── VISION.md
└── README.md
```

---

## The canonical reference

`plugin/system-guide.md` is the single source of truth for all plugin behaviour: file naming convention, file structures, tag system, formatting rules, and core operating principles. Any skill work should be consistent with this document. If there's a conflict between a skill file and anchor-context.md, anchor-context.md wins — update the skill, not the reference.

---

## Decision log

`product/knowledge-base/decisions.md` is the live record of product decisions — made, deferred, and open. At the end of any product work session, check whether any decisions were made or surfaced and prompt Amanda to log them if they aren't already captured. Log decisions in real-time during sessions where possible rather than waiting.

---

## Skill development conventions

Each skill lives in its own folder with a single `SKILL.md` file. Skills are written as plain instructions Claude reads at the start of a task.

When writing or modifying skills:
- Read `anchor-context.md` in full before making changes — the rules there are load-bearing
- Skills should be minimal: orient Claude, then defer to anchor-context.md for the detail
- Do not duplicate rules across skills and anchor-context.md; keep the reference canonical
- Preserve the user's voice in all entry handling — do not paraphrase or smooth out content

---

## File naming convention

```
YYYY-MM_mmm_[type]-[DD].md
```

Examples: `2026-03_mar_week-16.md`, `2026-03_mar_monthly.md`

Full details in `plugin/system-guide.md`.
