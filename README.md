# Operre

Operre is a lightweight, privacy-first, local-first project working environment.

It starts as a very fast Notepad-like text and Markdown editor, then grows step by step into a modular project platform for text, Markdown, common source files, documentation, project workspaces, diagrams, future CAD, Git/GitHub integration, optional Ideboard integration, and optional AI-agent workflows.

Operre is an independent project. It is not an Ideboard client shell. It must be useful on its own. Ideboard may later connect to Operre through an optional connector extension.

## Name and domain

- Project name: Operre
- Domain: operre.com

The name was originally inspired by operation research. It also carries useful product meaning around operation, organization, preparation, execution, workspace, and the German word "Oper" as a stage/performance metaphor.

Internal positioning:

Operre is a lightweight place where projects are prepared, organized, and performed.

## Source model

Operre is not planned as an open-source project.

Current source and distribution direction:

- development repository: private after initial inspection/setup;
- basic/core application: free to use;
- future extensions: may be free or paid;
- future public repository: possible later for distribution, public documentation, or user-facing materials.

## Product principles

Operre must be:

- very lightweight;
- local-first;
- privacy-first;
- useful without an account;
- useful without Ideboard;
- useful without GitHub;
- extension-driven;
- secure by default;
- documented in detail;
- TODO-driven in development;
- ergonomic on desktop first, tablet/mobile later.

Core philosophy:

Core-first. Cloud-optional. Extension-driven. Privacy-first.

## Initial technology direction

Preferred stack:

- Desktop framework: Tauri
- Editor engine: Monaco Editor
- Frontend: TypeScript + Vite + Solid
- Package manager: pnpm

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

Every meaningful decision, feature, architectural rule, security rule, UX rule, path decision, and implementation detail must be documented.

Development must be TODO-driven:

1. choose a TODO item;
2. audit current state;
3. implement;
4. verify;
5. document;
6. update TODO;
7. inspect git diff;
8. commit;
9. push;
10. audit after push.

## Language rule

Repository documentation must be English-only.

## Main documents

- specifications.md
- TODO.md
