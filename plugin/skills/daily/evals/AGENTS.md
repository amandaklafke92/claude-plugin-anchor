# Anchor Daily Skill — Evals

These evals test whether `SKILL.md` produces good enough instructions for a fresh Claude instance to process raw journal entries correctly. They are not output test suites — they're a scorecard for observing how a naive Claude (with only the skill loaded) handles real input.

---

## How it works

1. **Claude B** (a fresh session with the `anchor-daily` skill loaded, no other context) processes a raw entry. It never sees the eval criteria.
2. **You** observe Claude B's output and score it against the `expected_behavior` checklist.
3. If it fails, bring findings back to **Claude A** (the session where you refine SKILL.md) and iterate.
4. Log the result in `runs/` so you can track whether SKILL.md changes improve things.

---

## Eval spec format

```json
{
  "skill": "anchor-daily",
  "input_file": "anchor-data/raw/YYYY-MM-DD.md",
  "query": "Add this entry",
  "expected_behavior": [
    "Criterion targeting a known failure mode",
    "Criterion targeting a known failure mode"
  ]
}
```

`input_file` paths are relative to the `projects/` root. Raw files live in the private `anchor-data/` repo.

Criteria should focus on **known failure modes** — things Claude gets wrong without proper skill instructions — not comprehensive coverage of every possible output field.

---

## Scoring

For each criterion: pass / fail / partial.

**Priority failures** (skill is broken):
- Content rewritten (voice not preserved)
- Wrong date
- Tags invented outside the tag system

**Quality failures** (skill needs tuning):
- Missing a central person in `people:`
- Tags too sparse or over-tagged
- Key moment dropped or flattened
- Name misspelling not corrected (or corrected wrong)

---

## Run log format

Save each run to `runs/YYYY-MM-DD_eval-name.md`:

```markdown
# Eval run: [eval file] — [date]

**Skill version:** [version from SKILL.md frontmatter]
**Model:** [which Claude model was used]

## Results

| # | Criterion | Result | Notes |
|---|-----------|--------|-------|
| 1 | ... | pass/fail/partial | ... |

## Summary

[What worked, what failed, what to change in SKILL.md]
```

---

## Test cases

| File | Date | Entry summary |
|------|------|---------------|
| [2026-05-01.json](2026-05-01.json) | 1 May | Dinner with Tanja; Menno collab; Codex voice hack |
| [2026-05-02.json](2026-05-02.json) | 2 May | UTS uni girls reunion; voice thermostat; missing uni memories |
| [2026-06-08.json](2026-06-08.json) | 8 Jun | Coffee with Camilla; Robin's Anthropic feedback; bragging ≠ speaking to experience |
