# Anchor — MVP Roadmap

## Source: MVP-scope_overview.md

**Title:** anchor-overview  
**Source:** https://zorentia.com/tools/what-to-build-first  
**Created:** 2026-04-24  
**Description:** What's inside: A "Now/Next/Later" roadmap and a build sequence based on technical dependencies.

### Get your MVP Scope

Mission Control / Get your MVP Scope

### Build This First

**Three-Step Workflow**

This is the core architectural pattern that enables all input processing and user control features. Every input type (voice, text, audio, handwritten notes) must flow through this workflow to become a journal entry. Without this workflow structure, there's no way to connect input capture to processing to user approval, and no framework for the review/edit/regenerate functionality that preserves user agency. All processing features (transcription, OCR, formatting) are meaningless without this workflow to coordinate them. Monthly reviews and other advanced features depend on entries that can only exist through t...

### Summary

| Item | Value |
|---|---|
| Total Features | 28 |
| Phases | 3 |
| Roadmap | Now → Next → Later |
| Dependencies | 14 |

---

## Source: mvp_roadmap.md

**Title:** anchor-app_roadmap  
**Source:** https://zorentia.com/tools/what-to-build-first  
**Created:** 2026-04-24  
**Description:** What's inside: A "Now/Next/Later" roadmap and a build sequence based on technical dependencies.

### Get your MVP Scope

Mission Control / Get your MVP Scope

### 1. Build Phase: Now

**Foundation**

**Three-Step Workflow**

This is the core architectural pattern that enables all input processing and user control features. Every input type must flow through this workflow to become a journal entry. Without this structure, there's no way to connect input capture to processing to user approval.

**Delivers:** Users can capture typed entries through a consistent workflow that processes, reviews, and saves their memories in a structured format. This solves the core pain point of scattered memory fragments by providing one reliable system.

### 2. Build Phase: Next

**Input Processing**

**Voice Note Input**

Voice is a primary input method that requires the workflow foundation but no other dependencies. Users can immediately capture thoughts without typing.

**Audio Upload Input**

Extends voice capabilities to handle pre-recorded audio files using the same transcription pipeline as voice notes.

**Handwritten Note Photo Input**

OCR processing follows the same pattern as voice transcription - capture, process, review, save. Requires only the workflow foundation.

**Entry Review System**

The review interface must be fully built to handle all input types consistently. This is step 2 of the workflow.

**Source Text Preservation**

Essential for maintaining fidelity and enabling regeneration. Must be built with the workflow to ensure all inputs preserve originals.

**Automatic Storage Management**

Required to save entries from the workflow. Must handle both source and processed content with proper organization.

**Delivers:** Users can capture memories through voice, audio uploads, photos of handwritten notes, and typing - all processed through one consistent experience. This completes the core capture system and enables daily journaling across all input methods.

### 3. Build Phase: Later

**Archive Intelligence**

**Search Functionality**

Search requires a substantial archive of properly structured entries from the input processing phase. Without multiple entries across different input types, search provides minimal value.

**Monthly Reviews Generation**

Monthly reviews need structured entries as source material and sufficient entry volume to identify patterns and themes. This is the synthesis feature that creates higher-order value.

**Yearly Summaries**

Yearly summaries depend on monthly reviews as their source material. Cannot be built until monthly review generation is complete.

**Printed Life Record**

Printing requires the full archive structure with both individual entries and synthesized reviews to create a meaningful physical record.

**Delivers:** Transforms the captured archive into an intelligent memory system. Users can find any detail through search and receive automated insights about their life patterns through monthly and yearly reviews. The archive becomes a living record that grows more valuable over time.

---

## Source: MVP-scope_foundation-feature.md

**Title:** anchor-app_foundations  
**Source:** https://zorentia.com/tools/what-to-build-first  
**Created:** 2026-04-24  
**Description:** What's inside: A "Now/Next/Later" roadmap and a build sequence based on technical dependencies.

### Get your MVP Scope

Mission Control / Get your MVP Scope

### Foundation Feature

**Three-Step Workflow**

This is the core architectural pattern that enables all input processing and user control features. Every input type (voice, text, audio, handwritten notes) must flow through this workflow to become a journal entry. Without this workflow structure, there's no way to connect input capture to processing to user approval, and no framework for the review/edit/regenerate functionality that preserves user agency. All processing features (transcription, OCR, formatting) are meaningless without this workflow to coordinate them. Monthly reviews and other advanced features depend on entries that can only exist through t...

### Dependency Mapping

| Feature | Requires | Note |
|---|---|---|
| Voice Note Input | Three-Step Workflow | Voice notes need the workflow to move from capture to processing to user approval |
| Typed Entry Input | Three-Step Workflow | Typed entries follow the same capture-review-save pattern |
| Audio Upload Input | Three-Step Workflow | Audio uploads require the workflow to handle transcription and user review |
| Handwritten Note Photo Input | Three-Step Workflow | Photos need the workflow to process OCR and allow user review of extracted text |
| Automatic Voice Transcription | Three-Step Workflow | Transcription happens during the processing step and results must be reviewable |
| Entry Review System | Three-Step Workflow | Review is the second step of the three-step workflow |
| Entry Editing | Three-Step Workflow, Entry Review System | Editing happens during the review step before saving |
| Entry Regeneration | Three-Step Workflow, Entry Review System | Regeneration occurs during the review step after editing source text |
| Source Text Preservation | Three-Step Workflow | Source text is captured in step 1 and preserved through the workflow |
| Entry Approval System | Three-Step Workflow | Approval is the final step in the three-step workflow |
| Consistent Review Interface | Three-Step Workflow | The consistent interface is the review step that all input types flow through |
| Monthly Reviews Generation | Three-Step Workflow, Structured Entry Format | Monthly reviews need entries that have been processed through the workflow to ensure quality and structure |
| Search Functionality | Three-Step Workflow, Automatic Storage Management | Search needs entries that have been properly processed and stored through the workflow |
| Automatic Storage Management | Three-Step Workflow | Storage happens at the end of the workflow after user approval |

---

## Source: MVP-scope_feature-list.md

**Title:** anchor-app_features-list  
**Source:** https://zorentia.com/tools/what-to-build-first  
**Created:** 2026-04-24  
**Description:** What's inside: A "Now/Next/Later" roadmap and a build sequence based on technical dependencies.

### Get your MVP Scope

Mission Control / Get your MVP Scope

Saved on Apr 24, 2026

### Anchor Life Archive

| Feature | Description |
|---|---|
| Voice Note Input | Accept voice notes as input for journal entries |
| Typed Entry Input | Accept typed text entries as input for journal entries |
| Audio Upload Input | Accept uploaded audio files as input for journal entries |
| Handwritten Note Photo Input | Accept photos of handwritten notes as input for journal entries |
| Automatic Voice Transcription | Automatically transcribe voice notes and uploaded audio into text |
| OCR Processing | Perform OCR on photos of handwritten notes to extract text |
| Automatic Formatting | Automatically handle formatting of processed entries |
| Automatic Metadata Generation | Automatically generate metadata for entries |
| Automatic Tagging | Automatically tag entries without user intervention |
| Search Functionality | Make all entries searchable |
| Source Text Preservation | Keep original source text accessible for each entry |
| Entry Review System | Allow users to review processed entries before saving |
| Entry Editing | Allow users to edit source text and entries before saving |
| Entry Regeneration | Allow users to regenerate final entries from edited source text |
| Structured Entry Format | Format entries to capture who was present, what happened, what was said, and specific details |
| Monthly Reviews Generation | Generate monthly summaries including concrete moments, emotional themes, threads to carry forward, and dominant tags |
| Yearly Summaries | Create yearly summaries based on monthly reviews |
| Printed Life Record | Support generating a printed life record from archived entries |
| Three-Step Workflow | Implement capture, review, save workflow for all input types |
| Content Fidelity Rules | Process content without adding ideas, interpretation, or changing meaning |
| User-Controlled Storage | Store entries in user's own cloud account where possible, not on Anchor's servers |
| Consistent Review Interface | Provide same review screen experience for all capture methods |
| Minimal UI Design | Keep UI minimal so users don't need to understand technical processes |
| Automatic Organization | Organize entries automatically without user intervention |
| Memory Reconstruction Focus | Help users reconstruct what life felt like with enough detail to return to moments later |
| Entry Approval System | Require user approval before entries are saved |
| Automated Monthly Processing | Automatically generate monthly reflections on the first day of the next month |
