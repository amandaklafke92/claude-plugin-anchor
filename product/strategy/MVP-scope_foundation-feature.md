---
title: "anchor-app_foundations"
source: "https://zorentia.com/tools/what-to-build-first"
author:
published:
created: 2026-04-24
description: "What's inside: A \"Now/Next/Later\" roadmap and a build sequence based on technical dependencies."
tags:
---
## Get your MVP Scope

Mission Control / Get your MVP Scope

Foundation Feature

Three-Step Workflow

This is the core architectural pattern that enables all input processing and user control features. Every input type (voice, text, audio, handwritten notes) must flow through this workflow to become a journal entry. Without this workflow structure, there's no way to connect input capture to processing to user approval, and no framework for the review/edit/regenerate functionality that preserves user agency. All processing features (transcription, OCR, formatting) are meaningless without this workflow to coordinate them. Monthly reviews and other advanced features depend on entries that can only exist through t...

Dependency Mapping

Voice Note Input

Requires:Three-Step Workflow

Voice notes need the workflow to move from capture to processing to user approval

Typed Entry Input

Requires:Three-Step Workflow

Typed entries follow the same capture-review-save pattern

Audio Upload Input

Requires:Three-Step Workflow

Audio uploads require the workflow to handle transcription and user review

Handwritten Note Photo Input

Requires:Three-Step Workflow

Photos need the workflow to process OCR and allow user review of extracted text

Automatic Voice Transcription

Requires:Three-Step Workflow

Transcription happens during the processing step and results must be reviewable

Entry Review System

Requires:Three-Step Workflow

Review is the second step of the three-step workflow

Entry Editing

Requires:Three-Step Workflow, Entry Review System

Editing happens during the review step before saving

Entry Regeneration

Requires:Three-Step Workflow, Entry Review System

Regeneration occurs during the review step after editing source text

Source Text Preservation

Requires:Three-Step Workflow

Source text is captured in step 1 and preserved through the workflow

Entry Approval System

Requires:Three-Step Workflow

Approval is the final step in the three-step workflow

Consistent Review Interface

Requires:Three-Step Workflow

The consistent interface is the review step that all input types flow through

Monthly Reviews Generation

Requires:Three-Step Workflow, Structured Entry Format

Monthly reviews need entries that have been processed through the workflow to ensure quality and structure

Search Functionality

Requires:Three-Step Workflow, Automatic Storage Management

Search needs entries that have been properly processed and stored through the workflow

Automatic Storage Management

Requires:Three-Step Workflow

Storage happens at the end of the workflow after user approval