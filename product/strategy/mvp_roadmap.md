---
title: "anchor-app_roadmap"
source: "https://zorentia.com/tools/what-to-build-first"
author:
published:
created: 2026-04-24
description: "What's inside: A \"Now/Next/Later\" roadmap and a build sequence based on technical dependencies."
tags:
---
## Get your MVP Scope

Mission Control / Get your MVP Scope

1

Build Phase: Now

Foundation

Three-Step Workflow

This is the core architectural pattern that enables all input processing and user control features. Every input type must flow through this workflow to become a journal entry. Without this structure, there's no way to connect input capture to processing to user approval.

Delivers: Users can capture typed entries through a consistent workflow that processes, reviews, and saves their memories in a structured format. This solves the core pain point of scattered memory fragments by providing one reliable system.

2

Build Phase: Next

Input Processing

Voice Note Input

Voice is a primary input method that requires the workflow foundation but no other dependencies. Users can immediately capture thoughts without typing.

Audio Upload Input

Extends voice capabilities to handle pre-recorded audio files using the same transcription pipeline as voice notes.

Handwritten Note Photo Input

OCR processing follows the same pattern as voice transcription - capture, process, review, save. Requires only the workflow foundation.

Entry Review System

The review interface must be fully built to handle all input types consistently. This is step 2 of the workflow.

Source Text Preservation

Essential for maintaining fidelity and enabling regeneration. Must be built with the workflow to ensure all inputs preserve originals.

Automatic Storage Management

Required to save entries from the workflow. Must handle both source and processed content with proper organization.

Delivers: Users can capture memories through voice, audio uploads, photos of handwritten notes, and typing - all processed through one consistent experience. This completes the core capture system and enables daily journaling across all input methods.

3

Build Phase: Later

Archive Intelligence

Search Functionality

Search requires a substantial archive of properly structured entries from the input processing phase. Without multiple entries across different input types, search provides minimal value.

Monthly Reviews Generation

Monthly reviews need structured entries as source material and sufficient entry volume to identify patterns and themes. This is the synthesis feature that creates higher-order value.

Yearly Summaries

Yearly summaries depend on monthly reviews as their source material. Cannot be built until monthly review generation is complete.

Printed Life Record

Printing requires the full archive structure with both individual entries and synthesized reviews to create a meaningful physical record.

Delivers: Transforms the captured archive into an intelligent memory system. Users can find any detail through search and receive automated insights about their life patterns through monthly and yearly reviews. The archive becomes a living record that grows more valuable over time.