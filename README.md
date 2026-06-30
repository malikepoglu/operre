# Operre

Operre is a lightweight, privacy-first, local-first project working environment.

It starts like a classic, fast, old Windows 10 Notepad-style editor: install it, open it, write `.txt`, save, and continue working without accounts, cloud dependency, GitHub, Ideboard, AI, or online services.

From that small core, Operre can grow through explicit, permission-scoped extensions into a broader project platform for text, Markdown, common source files, documentation, project workspaces, diagrams, future CAD, Git/GitHub integration, optional Ideboard integration, optional sync, and optional AI-agent workflows.

Operre is an independent project. It is not an Ideboard client shell. Ideboard is a separate application and project. Ideboard may later connect to Operre through an optional Connector Extension.

## Name and domain

- Project name: Operre
- Domain: operre.com

The domain was originally inspired by operation research. The name also carries useful product meaning around operation, organization, preparation, execution, repository, workspace, and the German word "Oper" as a stage/performance metaphor.

Internal positioning:

> Operre is a lightweight place where projects are prepared, organized, and performed.

## Source model

Operre is not planned as an open-source project.

Current source and distribution direction:

- development repository: normally private;
- current public visibility: temporary, only for inspection/setup;
- basic/core application: free to use;
- future extensions: may be free or paid;
- future public repository: possible later for distribution, public documentation, or user-facing material.

## Product principles

Operre must be:

- very lightweight;
- local-first;
- privacy-first;
- useful without an account;
- useful without Ideboard;
- useful without GitHub;
- useful without AI;
- useful without online sync;
- extension-driven;
- secure by default;
- documented in detail;
- TODO-driven after the specification phase;
- ergonomic on desktop first, tablet/mobile later.

Core philosophy:

> Core-first. Cloud-optional. Extension-driven. Privacy-first.

## Initial technology direction

Preferred stack:

- Desktop framework: Tauri
- Editor engine: Monaco Editor
- Frontend: TypeScript + Vite + Solid
- Package manager: pnpm
- Native side: Rust through Tauri

Fallbacks:

- Desktop fallback: Electron
- Frontend fallback: React
- Not first choice: Svelte

Initial platform order:

1. Linux Desktop
2. Windows Desktop
3. macOS Desktop
4. Tablet/mobile later

## Repository discipline

This repository is the project memory.

Every meaningful decision, feature, architectural rule, security rule, UX rule, path decision, implementation detail, and completed work item must be documented.

Current phase:

1. consolidate the full specification;
2. document every accepted decision;
3. keep implementation TODOs pending until the specification is stable;
4. then create the detailed TODO/work plan;
5. then start application implementation.

## Language rule

Repository documentation must be English-only.

## Main documents

- specifications.md
- TODO.md

## Structured documentation

Topic-focused project memory is stored under [`docs/`](./docs/):

- [`docs/OPERRE_PRODUCT_PRINCIPLES.md`](./docs/OPERRE_PRODUCT_PRINCIPLES.md)
- [`docs/OPERRE_REPOSITORY_DISCIPLINE.md`](./docs/OPERRE_REPOSITORY_DISCIPLINE.md)
- [`docs/OPERRE_TECHNOLOGY_DECISIONS.md`](./docs/OPERRE_TECHNOLOGY_DECISIONS.md)
- [`docs/OPERRE_EXTENSION_SECURITY_MODEL.md`](./docs/OPERRE_EXTENSION_SECURITY_MODEL.md)
- [`docs/OPERRE_AI_AGENT_SECURITY.md`](./docs/OPERRE_AI_AGENT_SECURITY.md)
- [`docs/OPERRE_UI_UX_SPECIFICATION.md`](./docs/OPERRE_UI_UX_SPECIFICATION.md)
- [`docs/OPERRE_STORAGE_PRIVACY_SYNC.md`](./docs/OPERRE_STORAGE_PRIVACY_SYNC.md)
- [`docs/OPERRE_MARKDOWN_AND_EDITOR_BEHAVIOR.md`](./docs/OPERRE_MARKDOWN_AND_EDITOR_BEHAVIOR.md)
- [`docs/OPERRE_FUTURE_FEATURES_AND_RESTRAINTS.md`](./docs/OPERRE_FUTURE_FEATURES_AND_RESTRAINTS.md)
- [`docs/OPERRE_DECISION_LOG.md`](./docs/OPERRE_DECISION_LOG.md)
- [`docs/OPERRE_CONVERSATION_IMPORT_AND_SOURCE_PROCESSING.md`](./docs/OPERRE_CONVERSATION_IMPORT_AND_SOURCE_PROCESSING.md)
- [`docs/OPERRE_FILE_VISIBILITY_AND_PROTECTED_PATHS.md`](./docs/OPERRE_FILE_VISIBILITY_AND_PROTECTED_PATHS.md)
- [`docs/OPERRE_SEARCH_AND_FILE_COMPARE_BEHAVIOR.md`](./docs/OPERRE_SEARCH_AND_FILE_COMPARE_BEHAVIOR.md)
- [`docs/OPERRE_LARGE_FILE_MEMORY_AND_CACHE_BEHAVIOR.md`](./docs/OPERRE_LARGE_FILE_MEMORY_AND_CACHE_BEHAVIOR.md)
- [`docs/OPERRE_RECENT_FILES_PROJECTS_BEHAVIOR.md`](./docs/OPERRE_RECENT_FILES_PROJECTS_BEHAVIOR.md)
- [`docs/OPERRE_SETTINGS_UI_AND_SCHEMA_BEHAVIOR.md`](./docs/OPERRE_SETTINGS_UI_AND_SCHEMA_BEHAVIOR.md)
- [`docs/OPERRE_KEYBOARD_KEYBINDINGS_AND_INPUT_ERGONOMICS.md`](./docs/OPERRE_KEYBOARD_KEYBINDINGS_AND_INPUT_ERGONOMICS.md)
- [`docs/OPERRE_DISPLAY_DPI_SCALING_AND_RESPONSIVE_ERGONOMICS.md`](./docs/OPERRE_DISPLAY_DPI_SCALING_AND_RESPONSIVE_ERGONOMICS.md)
- [`docs/OPERRE_COMMAND_PALETTE_AND_COMMAND_SYSTEM_BEHAVIOR.md`](./docs/OPERRE_COMMAND_PALETTE_AND_COMMAND_SYSTEM_BEHAVIOR.md)
- [`docs/OPERRE_ERROR_WARNING_NOTIFICATION_AND_PROBLEM_REPORTING_BEHAVIOR.md`](./docs/OPERRE_ERROR_WARNING_NOTIFICATION_AND_PROBLEM_REPORTING_BEHAVIOR.md)
- [`docs/OPERRE_LOGS_AND_DIAGNOSTICS_EXPORT_BEHAVIOR.md`](./docs/OPERRE_LOGS_AND_DIAGNOSTICS_EXPORT_BEHAVIOR.md)

## Source review documents

- [`docs/source-reviews/OPERRE_SOURCE_REVIEW_1_ODT.md`](./docs/source-reviews/OPERRE_SOURCE_REVIEW_1_ODT.md)
- [`docs/source-reviews/OPERRE_SOURCE_REVIEW_2_ODT.md`](./docs/source-reviews/OPERRE_SOURCE_REVIEW_2_ODT.md)
- [`docs/source-reviews/OPERRE_SOURCE_REVIEW_3_ODT.md`](./docs/source-reviews/OPERRE_SOURCE_REVIEW_3_ODT.md)
- [`docs/source-reviews/OPERRE_SOURCE_REVIEW_4_ODT.md`](./docs/source-reviews/OPERRE_SOURCE_REVIEW_4_ODT.md)
- [`docs/source-reviews/OPERRE_SOURCE_REVIEW_5_ODT.md`](./docs/source-reviews/OPERRE_SOURCE_REVIEW_5_ODT.md)
