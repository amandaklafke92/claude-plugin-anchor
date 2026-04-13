# User flow: Upload voice note

---

## 1. Core outcome

User uploads an existing voice note and saves it as a clean, editable journal entry.

For cleanup and fidelity rules, see: [`../knowledge-base/rendering-rules.md`](rendering-rules.md)

---

## 2. User persona

Someone capturing a thought via an existing voice recording (low-friction, in-the-moment capture). The note already exists — they just need a way to get it into the system.

---

## 3. Entry point

Home screen → taps "Upload a voice note"

---

## 4. Steps

**Action**: User taps "Upload a voice note"
→ **Screen**: File picker opens
→ Accepted formats: MP3, M4A, WAV, and similar audio formats

**Input**: User selects audio file
→ **System**: Accepts file and begins processing
→ **Screen**: Processing state ("Transcribing…")

  **Decision**: Transcription successful?
  * **Yes** → System renders journal entry from transcript → show review screen
  * **No** → Error state (see edge cases)

---

**Screen**: Review screen — two-panel view
→ Rendered journal entry displayed (editable)
→ "View transcript" option available (hidden by default per rendering rules)

**Input**: User reviews rendered entry (optional edit)
→ **System**: Updates entry in real time

**Optional action**: User taps "View transcript"
→ **Screen**: Transcript expands or overlays
→ **Input**: User edits transcript
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
  * Records input type as "voice — uploaded"
  * Source audio file is not stored (see decisions.md — audio preservation deferred)

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

**User cancels the file picker without selecting a file**
→ File picker closes, user returns to home screen
→ No error shown — this is an intentional exit

---

## 7. Edge cases / errors

**Unsupported file format**
→ File picker rejects file before upload
→ Show message: "That file type isn't supported. Please upload an MP3, M4A, WAV, or similar audio file."
→ File picker remains open so user can select a different file

**File too large**
→ Show message: "That file is too large. Try a shorter recording or a compressed audio file."
→ File picker remains open

**Upload fails**
→ File selected but upload does not complete
→ Show error: "Something went wrong uploading your file. Try again."
→ Buttons: "Try again" / "Cancel"
→ "Cancel" returns user to home screen

**Transcription fails**
→ Show error: "We couldn't transcribe that. Try uploading the file again, or type your note instead."
→ Buttons: "Try again" / "Type instead"
→ "Try again" → reopens file picker
→ "Type instead" → opens type entry flow with blank state
→ Note: saving audio-only without a transcript is out of MVP scope — see decisions.md

**Unclear audio segments**
→ Transcription marks unclear words as `[unclear]`
→ Review screen shows `[unclear]` inline so user can correct before saving
→ See rendering-rules.md for full handling rules

**User exits before saving**
→ Show confirmation prompt: "Leave without saving? Your entry will be lost."
→ Confirm → discard and return to home
→ Cancel → return to review screen

**Long processing time**
→ Maintain visible loading state: "Transcribing…"
→ If processing exceeds threshold: "This is taking longer than expected. Hang tight…"

---

## 8. UX copy

**Entry point (home screen)**
| Element | Copy |
|---|---|
| CTA | "Upload a voice note" |

**Processing**
| Element | Copy |
|---|---|
| Loading state | "Transcribing…" |
| Extended wait | "This is taking longer than expected. Hang tight…" |

**Review screen**
| Element | Copy |
|---|---|
| Transcript toggle (collapsed) | "View transcript" |
| Transcript toggle (expanded) | "Hide transcript" |
| Regenerate button | "Regenerate entry" |
| Save CTA | "Save entry" |
| Discard | "Discard" |

**Error messages**
| Trigger | Copy |
|---|---|
| Unsupported file format | "That file type isn't supported. Please upload an MP3, M4A, WAV, or similar audio file." |
| File too large | "That file is too large. Try a shorter recording or a compressed audio file." |
| Upload failed | "Something went wrong uploading your file. Try again." |
| Transcription failed | "We couldn't transcribe that. Try uploading the file again, or type your note instead." |

**Action buttons (errors)**
| Context | Buttons |
|---|---|
| Upload failed | "Try again" / "Cancel" |
| Transcription failed | "Try again" / "Type instead" |

**Confirmation prompts (discard / abandon)**
| Trigger | Copy |
|---|---|
| Leave review screen without saving | "Leave without saving? Your entry will be lost." |

**Success**
| Element | Copy |
|---|---|
| Save confirmation | "Entry saved." |
