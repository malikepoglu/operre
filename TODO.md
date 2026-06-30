# Operre TODO

This file is the planning queue for Operre.

Current project phase:

- specification consolidation first;
- implementation TODO after specifications are stable;
- no application implementation before accepted specification baseline.

## Rules

- Every task must be documented.
- Every completed detail must update specifications.md or another relevant document.
- Repository language is English-only.
- No implementation should proceed without a clear TODO item.
- No security-sensitive behavior should be added without documented security rules.
- Operre is not open source.
- Basic/core functionality is planned to be free.
- Future extensions may be free or paid.

## Status labels

- QUEUED
- IN_PROGRESS
- DONE
- BLOCKED
- DEFERRED
- SEALED

## Specification-phase queue

| ID | Status | Task |
|---|---|---|
| OPR-SPEC-0001 | DONE | Create initial README, specifications, TODO, and repository hygiene baseline. |
| OPR-SPEC-0002 | DONE | Expand specifications from full planning transcript through delete behavior. |
| OPR-SPEC-0002B | DONE | Add gap patch from uploaded ODT transcript: VS Code/Cursor/Monaco research baseline, detailed technology notes, earlier diagram/project-board ideas, future doc split, and implementation restraint rules. |
| OPR-SPEC-0003 | QUEUED | Continue product decisions after delete behavior. |
| OPR-SPEC-0004 | QUEUED | Decide detailed permanent delete and OS Trash/Recycle Bin behavior. |
| OPR-SPEC-0005 | QUEUED | Define search behavior. |
| OPR-SPEC-0006 | QUEUED | Define recent files/projects behavior. |
| OPR-SPEC-0007 | QUEUED | Define settings UI and settings storage schema. |
| OPR-SPEC-0008 | QUEUED | Define exact extension manifest schema. |
| OPR-SPEC-0009 | QUEUED | Define extension permission UI and approval flow. |
| OPR-SPEC-0010 | QUEUED | Define workspace trust model and restricted mode UI. |
| OPR-SPEC-0011 | QUEUED | Define Markdown preview security implementation details. |
| OPR-SPEC-0012 | QUEUED | Define AI connector audit log schema. |
| OPR-SPEC-0013 | QUEUED | Define installer/update/security model. |
| OPR-SPEC-0014 | QUEUED | Define non-open-source/free-core legal/license strategy. |
| OPR-SPEC-0015 | QUEUED | Define first application implementation phase after specifications stabilize. |
| OPR-SPEC-0016 | DONE | Split consolidated specification into focused docs after specification baseline stabilizes. |
| OPR-SPEC-0017 | DONE | Write accepted decisions from uploaded five-part ODT transcript into structured repository memory files. |
| OPR-SOURCE-0001 | DONE | Process 1.odt into dedicated source review memory document. |
| OPR-SOURCE-0002 | DONE | Process 2.odt into dedicated source review memory document. |
| OPR-SOURCE-0003 | DONE | Process 3.odt into dedicated source review memory document. |
| OPR-SOURCE-0004 | DONE | Process 4.odt into dedicated source review memory document. |
| OPR-SOURCE-0005 | DONE | Process 5.odt into dedicated source review memory document. |
| OPR-SPEC-0018 | DONE | Complete ordered source review pass for 1.odt through 5.odt. |
| OPR-SPEC-0019 | DONE | Resume product decisions after delete behavior. |
| OPR-SPEC-0020 | DONE | Define hidden files, dotfiles, and protected path visibility behavior. |
| OPR-SPEC-0021 | DONE | Define detailed search, replace, and file compare behavior. |
| OPR-SPEC-0022 | DONE | Define Recent files/projects/folders behavior. |
| OPR-SPEC-0023 | DONE | Define large file memory and cache behavior. |
| OPR-SPEC-0024 | DONE | Define Settings UI and settings schema behavior. |
| OPR-SPEC-0025 | DONE | Define keyboard shortcut, keybinding, and input ergonomics behavior. |
| OPR-SPEC-0026 | DONE | Define detailed Command Palette and command system behavior. |
| OPR-SPEC-0027 | DONE | Define display, DPI, scaling, and responsive ergonomics behavior. |
| OPR-SPEC-0028 | QUEUED | Revisit display/DPI/scaling/responsive ergonomics during detailed UI implementation. |
| OPR-SPEC-0029 | DONE | Define error, warning, notification, and problem reporting behavior. |
| OPR-SPEC-0030 | DONE | Define detailed logs and diagnostics export behavior. |
| OPR-SPEC-0031 | DONE | Define crash recovery and unsaved work recovery behavior. |
| OPR-SPEC-0032 | DONE | Define Auto Save, file saving, atomic write, and backup behavior. |
| OPR-SPEC-0033 | DONE | Define symlink, hardlink, special file, and file watcher behavior. |
| OPR-SPEC-0034 | DONE | Define File Explorer, workspace tree, File Info, tabs, and navigation behavior. |
| OPR-SPEC-0035 | DONE | Define panels, sidebars, activity bar, layout persistence, and view management behavior. |
| OPR-SPEC-0036 | QUEUED | Define menus, toolbar, titlebar, status bar, and workbench chrome behavior. |

## Implementation queue

Implementation queue is intentionally not expanded yet.

Implementation starts only after:

1. specifications.md is stable enough;
2. core scope is frozen for the first milestone;
3. repository discipline is accepted;
4. first implementation TODO list is generated.


## Future extension track

- Future programming language toolchain/runtime extension track:
  after the standard/core Operre functions become usable, Operre may support optional extensions for compilers, interpreters, simulators, emulators, linkers, executable/package builders, live runtime/REPL surfaces, language servers, debuggers, build/test runners, problem matchers, formatters, linters, and language-specific project templates. These capabilities must remain extension-driven, permission-scoped, Workspace-Trust-aware, audited, and never required by Operre core.


## Current next topic

NEXT_TOPIC: Menus, toolbar, titlebar, status bar, and workbench chrome behavior

## Meta discipline queue

| ID | Status | Item |
| --- | --- | --- |
| OPR-META-0001 | DONE | Document the rule that every 20 completed meaningful repository workflow steps require a detailed terminal-based GitHub repository audit before continuing. |
