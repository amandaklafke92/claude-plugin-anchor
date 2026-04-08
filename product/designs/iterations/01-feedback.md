---

## date: 2026-04-05
prototype: Lovable v1
status: feedback captured — not yet actioned

## Iteration 1 — Anchor Prototype (Lovable v1)

**Date:** 2026-04-05  
**Status:** Feedback captured — not yet actioned  

---

### What’s working

- Overall design direction is right: simple, calm, good font, easy to read  
- Capture methods are logically grouped (voice vs writing; record vs upload)  
- Voice note upload auto-opens file picker on click — good friction reduction  
- After saving, returns to home screen — correct behaviour  
- Date auto-selects to current date on all input screens

---

### Key issues identified

#### 1. Unnecessary two-step capture flow

Current flow requires two steps to begin journal entry capture.  
Violates core intent: user opens app to capture immediately.

##### Change

- Display capture options directly on home screen  
- Remove “Capture a moment” intermediary step  
- Replace app name with a personal greeting (e.g. "Hey [name], what's on your mind?")

##### Design constraints (for new home screen)

- Use clear and specific labels (e.g. "Upload a note" instead of "Upload handwriting")  
- Remove low-signal UI (emojis, unnecessary subtext)  
- Keep interaction minimal — avoid introducing new friction

##### Notes

- Grid layout logic still valid, but needs re-evaluation in home context  
- Circle vs square buttons to be explored (label character length may constrain this)  
- Dictation intentionally excluded (overlaps with voice recording, adds complexity without clear benefit)

---

#### 2. Transcription missing after upload

User uploads voice or written note but never sees the transcript, thus unable to verify accuracy or make changes.

##### Change

- Display transcription toggle/button for user to optinally access transcript in a scrollable, editable text box after upload  
- Ensure user can review and correct before saving

---

#### 3. No way to change or reset uploaded files

Once a file is selected, there is no way to remove or replace it.

##### Change

- Add clear/remove (✕) action to reset file selection  
- Restore original “Choose a file” state after removal

---

#### 4. Tags introduced before content exists (misaligned flow)

Tags are shown before any content is created, which conflicts with intended AI-driven tagging flow.

##### Change

- Remove manual tag selection from input screens  
- Introduce tags after content creation via AI suggestion

---

### Screenshot reference


| File                            | Screen                   |
| ------------------------------- | ------------------------ |
| 01-lovable-questions.png        | Lovable setup Q&A        |
| 02-home-screen.png              | Home screen              |
| 03-capture-method-selection.png | Capture method picker    |
| 04-record-voice.png             | Record voice input       |
| 05-upload-voice-note.png        | Upload voice note input  |
| 06-type-it-out.png              | Type it out input        |
| 07-upload-handwriting.png       | Upload handwriting input |


