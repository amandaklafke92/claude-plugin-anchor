# User flow: Record voice note

---

## 1. Core outcome

User records a voice note live in the app and saves it as a clean, editable journal entry.

For cleanup and fidelity rules, see: [`../knowledge-base/rendering-rules.md`](../knowledge-base/rendering-rules.md)

---

## 2. User persona

Someone capturing a thought in the moment — no prep, no existing file. They want to speak and come back to a clean entry.

---

## 3. Entry point

Home screen → taps "Record a voice note"

---

## 4. Steps

**System**: Check microphone permission

  **Decision**: Permission granted?
  * **Yes** → Proceed to recording screen
  * **No — first time ask** → Show system permission prompt
    * User grants → Proceed to recording screen
    * User denies → Show in-app error (see edge cases)
  * **No — previously denied** → Show in-app error with link to Settings (see edge cases)

---

**Screen**: Recording interface appears
→ Large record button, timer at 00:00, "Tap to start recording"

**Action**: User taps record button
→ **System**: Recording begins
→ **Screen**: Timer starts, button becomes active stop state, "Recording…" indicator visible

  **Optional action**: User taps Pause
  → **System**: Recording pauses
  → **Screen**: Timer freezes, button becomes resume state, "Paused" indicator visible
  → **Optional action**: User taps Resume → recording continues

**Action**: User taps Stop
→ **System**: Recording ends, audio captured
→ **Screen**: Transition to processing state ("Transcribing…")

  **Decision**: Transcription successful?
  * **Yes** → Show review screen
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
  * Records input type as "voice — recorded"

**Screen**: Confirmation message ("Entry saved.")
→ **Redirect**: Home screen

---

## 5. Exit / end point

Journal entry is saved and accessible in the system. User returns to the home screen ready for the next capture.

---

## 6. Alternative paths

**User discards during recording**
→ User taps "Discard" or navigates away mid-recording
→ Show confirmation prompt: "Discard this recording? It won't be saved."
→ Confirm → Recording deleted, user returns to home screen
→ Cancel → Return to recording screen, recording resumes or remains paused

**User discards from review screen**
→ User taps "Discard" or navigates away before saving
→ Show confirmation prompt: "Leave without saving? Your entry will be lost."
→ Confirm → Entry and transcript discarded, user returns to home screen
→ Cancel → Return to review screen

**User edits entry directly without viewing transcript**
→ Permitted — direct edits to the rendered entry are saved as-is
→ No transcript regeneration triggered by this path

---

## 7. Edge cases / errors

**Microphone permission denied (first time)**
→ System prompt declined
→ Show in-app message: "Microphone access is needed to record. You can allow it in your device settings."
→ Button: "Open Settings" / "Not now"
→ "Not now" returns user to home screen

**Microphone permission previously denied**
→ Show in-app message immediately: "To record, allow microphone access in Settings > [App name] > Microphone."
→ Button: "Open Settings" / "Cancel"

**Recording cut short — very short audio (< 2 seconds)**
→ After Stop: show message "That was a very short recording. Transcription may be limited."
→ Continue through transcription pipeline as normal

**No speech detected**
→ Transcription returns empty or near-empty
→ Show message: "We didn't catch any speech. Try recording again, or type your note instead."
→ Buttons: "Try again" / "Type instead"
→ "Try again" → returns to recording screen
→ "Type instead" → opens type entry flow with blank state

**Transcription fails**
→ Show error: "We couldn't transcribe that. Try recording again, or type your note instead."
→ Buttons: "Try again" / "Type instead"
→ Note: saving audio-only without transcript is out of scope for MVP — see decisions.md

**Long processing time**
→ Maintain visible loading state throughout: "Transcribing…"
→ Do not leave user in an unresponsive state; if processing exceeds threshold, show: "This is taking longer than expected. Hang tight…"

**App interruption during recording** (e.g. phone call, notification)
→ Recording pauses automatically if OS requires
→ On return: show prompt "Your recording was paused. Resume or discard?"
→ "Resume" → recording continues
→ "Discard" → confirm prompt before discarding

**Unclear audio segments**
→ Transcription marks unclear words as `[unclear]`
→ Review screen shows `[unclear]` inline so user can correct before saving
→ See rendering-rules.md for full handling rules

---

## 8. UX copy

**Entry point (home screen)**
| Element | Copy |
|---|---|
| CTA | "Record a voice note" |

**Recording screen**
| Element | Copy |
|---|---|
| Prompt (pre-record) | "Tap to start recording" |
| Recording indicator | "Recording…" |
| Pause button | "Pause" |
| Paused indicator | "Paused" |
| Resume button | "Resume" |
| Stop button | "Stop" |
| Discard | "Discard" |

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
| Mic permission denied (first time) | "Microphone access is needed to record. You can allow it in your device settings." |
| Mic permission previously denied | "To record, allow microphone access in Settings > [App name] > Microphone." |
| Very short recording | "That was a very short recording. Transcription may be limited." |
| No speech detected | "We didn't catch any speech. Try recording again, or type your note instead." |
| Transcription failed | "We couldn't transcribe that. Try recording again, or type your note instead." |

**Action buttons (errors)**
| Context | Buttons |
|---|---|
| Mic denied | "Open Settings" / "Not now" |
| No speech / transcription failed | "Try again" / "Type instead" |
| App interruption on return | "Resume" / "Discard" |

**Confirmation prompts (discard / abandon)**
| Trigger | Copy |
|---|---|
| Discard during recording | "Discard this recording? It won't be saved." |
| Leave review screen without saving | "Leave without saving? Your entry will be lost." |

**Success**
| Element | Copy |
|---|---|
| Save confirmation | "Entry saved." |
