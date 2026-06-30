# Operre Conversation Import and Source Processing

## Purpose

This document defines how imported conversation/source files are handled during Operre planning.

## Local import area

Local-only import path:

- `/home/mak/operre/conversation_import/`

Expected full chat export path:

- `/home/mak/operre/conversation_import/operre_chat_full_export.txt`

## Security

Raw full conversation transcripts are not committed by default.

Reason:

- they may contain private planning details;
- they may contain sensitive project context;
- they may contain unrelated conversation material;
- repository should store accepted decisions, not raw chat dumps.

## Source processing order

Accepted order:

1. `1.odt`
2. `2.odt`
3. `3.odt`
4. `4.odt`
5. `5.odt`

Rules:

- process one source at a time;
- create a dedicated source review document for each source;
- update README/docs index;
- update TODO status;
- update specifications processing status;
- update decision log;
- commit and push;
- verify with post-push audit.

## Terminal reliability

Terminal blocks must be:

- Bash-compatible;
- self-contained;
- fail-fast;
- explicit about paths;
- protected against dirty worktrees;
- checked with `git diff --check`;
- committed only after diff review;
- pushed only after successful commit.

Every block should end with:

- `PROMPT_RETURNED=TRUE`

## UI error handling

If a ChatGPT UI/rendering error appears, verify real state through:

- terminal output;
- `git status --short`;
- `git log --oneline`;
- `git ls-remote --heads origin`;
- pushed commit hash.

Do not treat UI rendering errors as repository failure if terminal/git audit proves success.

## Current source review status

- `1.odt`: processed.
- `2.odt`: processed.
- `3.odt`: processed.
- `4.odt`: processed.
- `5.odt`: processed.

Next continuation point:

- continue product decisions after delete behavior.
