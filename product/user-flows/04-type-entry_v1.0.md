# User flow: Type an entry

---

## 1. Core outcome

User types a journal entry directly and saves it as a clean, readable entry.

For cleanup and fidelity rules, see: [`../knowledge-base/rendering-rules.md`](rendering-rules.md)

> **Pipeline note**: The type entry flow does not generate a separate transcript — the typed text IS the source of truth. There is no OCR or audio transcription step. Rendering applies only light formatting (punctuation, paragraph breaks) with no filler-word removal or inference. See open question in section 7.

---

## 2. User persona

Someone who prefers to write, or is in a context where speaking isn't possible (meeting, public space, late at night). May also be used as a fallback from a failed voice or upload attempt.

---

## 3. Entry point

Home screen → taps "Type it out"

Also reachable as fallback from:
- "Type instead" button in record voice note error states
- "Type instead" button in upload note error states

---

## 4. Steps

**Action**: User taps "Type it out"
→ **Screen**: Text editor opens
→ Keyboard appears automatically
→ Placeholder text visible: "What's on your mind?"

**Input**: User types entry
→ **System**: Captures text in real time
→ No processing step — typed text is stored directly as the entry

  **Decision**: Does rendering apply to typed entries?
  * See open question in section 7. For now, treat typed text as the rendered entry — no additional processing step.

  **Decision**: AI tagging ships in MVP?
  * **Yes** → After user taps "Save entry", AI-suggested tags are generated and presented for confirmation before final save
  * **No** → Skip tag step entirely

**Action**: User taps "Save entry"
→ **System**:
  * Stores typed text as source of truth (functions as both transcript and entry)
  * Saves entry in plain markdown
  * Records input type as "typed"

  **If AI tagging ships:**
  → **Screen**: Tags presented ("Here are some suggested tags — confirm or skip")
  → **Input**: User confirms or deselects tags (optional)
  → **Action**: User taps "Save" to finalise
  → **System**: Saves entry with confirmed tags

**Screen**: Confirmation message ("Entry saved.")
→ **Redirect**: Home screen

---

## 5. Exit / end point

Journal entry is saved and accessible in the system. User returns to the home screen ready for the next capture.

---

## 6. Alternative paths

**User arrives from a failed voice or upload attempt**
→ Text editor opens with blank state (no pre-population from failed transcript)
→ Flow proceeds identically to standard typed entry

**User pastes text from clipboard**
→ Permitted — pasted content treated as typed input
→ No processing applied beyond light formatting at save

**User leaves editor with unsaved text**
→ Show confirmation prompt: "Leave without saving? Your entry will be lost."
→ Confirm → discard, return to home screen
→ Cancel → return to editor, text preserved

**User saves an empty entry**
→ Prevent save: "Your entry is empty. Add something before saving."
→ Return focus to text editor

---

## 7. Open question — does rendering apply to typed entries?

The rendering pipeline was designed for converting speech or handwriting into clean prose. For typed entries, users are already writing deliberately — there are no filler words, transcription errors, or OCR mistakes to clean up.

**Options:**

**A. No rendering step** — typed text is saved exactly as written. Simple, predictable, and respects user intent. Risk: inconsistent experience if some entry types go through rendering and others don't.

**B. Light rendering only** — apply only formatting normalisation (consistent paragraph breaks, punctuation) with no content changes. Keeps the pipeline consistent across input types without risk of altering meaning.

**C. Full rendering pipeline** — same process as voice/OCR entries. Risk: unnecessary and could alter meaning for users who wrote deliberately.

Recommendation: **Option B**. Apply light formatting only. This maintains pipeline consistency, is lowest-risk on fidelity, and requires minimal implementation work. Avoids the sharp asymmetry of Option A while steering clear of the over-reach of Option C.

> **Status: open — needs decision before build.** Current flow assumes Option B as a working default.

---

## 8. Edge cases / errors

**Empty entry on save**
→ Block save
→ Show message: "Your entry is empty. Add something before saving."
→ Return focus to text editor

**Very long entry**
→ No hard limit enforced in MVP — accept as-is
→ Consider: character count indicator near save button if UX warrants it (deferred)

**User pastes from clipboard — unexpected format**
→ Treat as plain text, strip any rich formatting (bold, links, etc.)
→ Do not show an error; normalise silently

**Connection error on save**
→ Show error: "Your entry couldn't be saved. Check your connection and try again."
→ Text preserved in editor — do not discard on error
→ Button: "Try again"

**App closed before saving**
→ Best effort: auto-save draft to local storage if possible (deferred — depends on storage architecture decision)
→ If not possible: note that unsaved entries are lost on close — this should be surfaced in the confirmation prompt flow

---

## 9. UX copy

**Entry point (home screen)**
| Element | Copy |
|---|---|
| CTA | "Type it out" |

**Text editor**
| Element | Copy |
|---|---|
| Placeholder | "What's on your mind?" |
| Save CTA | "Save entry" |
| Discard | "Discard" |

**Tag step (if AI tagging ships)**
| Element | Copy |
|---|---|
| Tag prompt | "Here are some suggested tags — confirm or skip." |
| Confirm tags and save | "Save" |
| Skip tags | "Skip" |

**Error messages**
| Trigger | Copy |
|---|---|
| Empty entry on save | "Your entry is empty. Add something before saving." |
| Save failed (connection) | "Your entry couldn't be saved. Check your connection and try again." |

**Action buttons (errors)**
| Context | Button |
|---|---|
| Save failed | "Try again" |

**Confirmation prompts (discard / abandon)**
| Trigger | Copy |
|---|---|
| Leave editor with unsaved text | "Leave without saving? Your entry will be lost." |

**Success**
| Element | Copy |
|---|---|
| Save confirmation | "Entry saved." |
