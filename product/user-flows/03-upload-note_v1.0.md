# User flow: Upload a note

---

## 1. Core outcome

User uploads an image of a handwritten or typed note (photo, scan, or digital document), which is converted to an editable transcript via OCR and saved as a clean journal entry.

For cleanup and fidelity rules, see: [`../knowledge-base/rendering-rules.md`](../knowledge-base/rendering-rules.md)

> **Scope note**: "Upload a note" covers images as source material — text to be converted and stored. This is distinct from "photo integration" (photos as embedded content within an entry), which is explicitly out of MVP scope. The output of this flow is always a text entry, not a stored image.

---

## 2. User persona

Someone who writes by hand — in a notebook, on a whiteboard, on loose paper — and wants their handwritten notes captured in the system without retyping.

---

## 3. Entry point

Home screen → taps "Upload a note"

---

## 4. Steps

**Action**: User taps "Upload a note"
→ **Screen**: File picker opens
→ Accepted formats: JPG, PNG, HEIC, PDF (single page)

**Input**: User selects file
→ **System**: Accepts file, begins processing
→ **Screen**: Processing state ("Reading your note…")

  **Decision**: OCR successful?
  * **Yes** → Show review screen
  * **Partially successful** → Show review screen with `[unclear]` markers where text could not be read
  * **No** → Error state (see edge cases)

---

**Screen**: Review screen — two-panel view
→ Rendered journal entry displayed (editable)
→ "View transcript" option available (hidden by default per rendering rules)

**Input**: User reviews rendered entry (optional edit)
→ **System**: Updates entry in real time

**Optional action**: User taps "View transcript"
→ **Screen**: Transcript expands or overlays
→ **Input**: User edits transcript (e.g. corrects OCR errors, fills in `[unclear]` sections)
→ **Action**: User taps "Regenerate entry"
→ **System**: Rerenders entry from updated transcript

  **Decision**: AI tagging ships in MVP?
  * **Yes** → AI-suggested tags appear below entry
    * User confirms or deselects tags (optional, not required to save)
  * **No** → Skip tag step entirely

**Action**: User taps "Save entry"
→ **System**:
  * Stores transcript as source of truth
  * Saves rendered journal entry in plain markdown
  * Records input type as "note — uploaded"
  * Source image file is not stored (see decisions.md — storage deferred)

**Screen**: Confirmation message ("Entry saved.")
→ **Redirect**: Home screen

---

## 5. Exit / end point

Journal entry is saved and accessible in the system. User returns to the home screen ready for the next capture.

---

## 6. Alternative paths

**User discards from review screen**
→ User taps "Discard" or navigates away before saving
→ Show confirmation prompt: "Leave without saving? Your entry will be lost."
→ Confirm → Entry and transcript discarded, user returns to home screen
→ Cancel → Return to review screen

**User edits entry directly without viewing transcript**
→ Permitted — direct edits to the rendered entry are saved as-is
→ No transcript regeneration triggered by this path

**User uploads a PDF**
→ Single-page PDFs accepted
→ Treated identically to image upload: OCR → transcript → review
→ Multi-page PDFs: see edge cases

---

## 7. Edge cases / errors

**Unsupported file format**
→ File picker rejects file before upload
→ Show message: "That file type isn't supported. Please upload a JPG, PNG, HEIC, or single-page PDF."
→ File picker remains open so user can select a different file

**File too large**
→ Show message: "That file is too large. Try a compressed image or photo at lower resolution."
→ File picker remains open

**Upload fails**
→ File selected but upload does not complete
→ Show error: "Something went wrong uploading your file. Try again."
→ Buttons: "Try again" / "Cancel"
→ "Cancel" returns user to home screen

**OCR fails completely**
→ Image processed but no text extracted (e.g. blank page, unsupported script, severe image quality issue)
→ Show error: "We couldn't read that note. Try a clearer photo, or type your note instead."
→ Buttons: "Try again" / "Type instead"
→ "Try again" → reopens file picker
→ "Type instead" → opens type entry flow with blank state

**OCR partially successful**
→ Some text extracted, some words or sections unreadable
→ Proceed to review screen with `[unclear]` markers inline
→ Do not block saving — user can correct or leave `[unclear]` as-is
→ Show advisory: "Some parts of your note couldn't be read. Check the sections marked [unclear] before saving."

**Poor image quality (e.g. low light, blurry)**
→ Treat as partial OCR failure — proceed with `[unclear]` markers
→ Do not fail silently; surface all unreadable sections explicitly

**Multi-page PDF uploaded**
→ If only first page is processed: show message "Only the first page of your PDF was captured. To include more pages, upload them separately."
→ Note: decision on multi-page support is deferred — this is the MVP-safe fallback

**User exits before saving**
→ Show confirmation prompt: "Leave without saving? Your entry will be lost."
→ Confirm → discard and return to home
→ Cancel → return to review screen

**Long processing time**
→ Maintain visible loading state: "Reading your note…"
→ If processing exceeds threshold: "This is taking longer than expected. Hang tight…"

---

## 8. UX copy

**Entry point (home screen)**
| Element | Copy |
|---|---|
| CTA | "Upload a note" |

**Processing**
| Element | Copy |
|---|---|
| Loading state | "Reading your note…" |
| Extended wait | "This is taking longer than expected. Hang tight…" |

**Review screen**
| Element | Copy |
|---|---|
| Partial OCR advisory | "Some parts of your note couldn't be read. Check the sections marked [unclear] before saving." |
| Transcript toggle (collapsed) | "View transcript" |
| Transcript toggle (expanded) | "Hide transcript" |
| Regenerate button | "Regenerate entry" |
| Save CTA | "Save entry" |
| Discard | "Discard" |

**Error messages**
| Trigger | Copy |
|---|---|
| Unsupported file format | "That file type isn't supported. Please upload a JPG, PNG, HEIC, or single-page PDF." |
| File too large | "That file is too large. Try a compressed image or photo at lower resolution." |
| Upload failed | "Something went wrong uploading your file. Try again." |
| OCR failed completely | "We couldn't read that note. Try a clearer photo, or type your note instead." |
| Multi-page PDF (MVP fallback) | "Only the first page of your PDF was captured. To include more pages, upload them separately." |

**Action buttons (errors)**
| Context | Buttons |
|---|---|
| Upload failed | "Try again" / "Cancel" |
| OCR failed | "Try again" / "Type instead" |

**Confirmation prompts (discard / abandon)**
| Trigger | Copy |
|---|---|
| Leave review screen without saving | "Leave without saving? Your entry will be lost." |

**Success**
| Element | Copy |
|---|---|
| Save confirmation | "Entry saved." |
