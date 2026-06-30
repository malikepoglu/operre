# Operre Source Review: 2.odt

This document records decisions and useful planning extracted from `2.odt`.

Source position:

- file: `2.odt`
- processing order: 2 / 5
- topic range: Operre naming/product identity, repository discipline, frontend choice, package manager choice, Tauri/Electron comparison, platform order, ergonomics, local-first sync direction.

## 1. Product identity confirmed

Accepted:

- product name: Operre;
- domain: operre.com;
- product type: very lightweight project platform;
- independent project;
- not an Ideboard shell;
- Ideboard integration optional later;
- CAD later;
- LogisticSearch can continue in parallel.

Meaning layers:

- operation research origin;
- operate / operation feeling;
- organize / project execution feeling;
- repository / workspace association;
- German "Oper" as stage/performance metaphor.

Internal meaning:

> Operre is a lightweight place where projects are prepared, organized, and performed.

Branding caution:

- do not overuse the poetic stage metaphor;
- keep product technical, clean, and lightweight.

## 2. Notepad-like core confirmed

Accepted core direction:

- old Windows 10 Notepad-like lightweight start;
- Windows 11 Notepad is not the preferred reference;
- install/open/write `.txt` immediately;
- basic/core application free;
- open source is not planned;
- core must stay small;
- features grow through extensions.

Core v0.1 spirit:

- open quickly;
- create/open/edit/save `.txt`;
- low memory target;
- simple user control;
- no forced account;
- no forced cloud;
- no forced GitHub;
- no forced Ideboard;
- no forced AI.

## 3. Extension-first direction confirmed

Accepted:

- GitHub support is an extension/connector, not core.
- Ideboard integration is an extension/connector, not core.
- Diagrams, CAD, TODO list, work plan, service plan, AI, export tools, and theme packs are future extensions or built-in/future features.
- Operre must remain useful without extensions.

Important product rule:

> Operre core = lightweight text/project workspace foundation.  
> Operre extensions = additional project-platform capabilities.

## 4. Repository and development discipline

Accepted:

- Operre can be developed in parallel with LogisticSearch.
- LogisticSearch remains long-running and must not be disrupted.
- Operre should use similar audit/commit/TODO/documentation discipline.
- Operre repository documentation must be English-only.
- Chat discussion may remain Turkish.
- GitHub repository is the project memory.

Workflow direction:

1. audit first;
2. document decisions;
3. update TODO;
4. implement only after decisions are clear;
5. verify;
6. commit;
7. push;
8. post-push audit.

Initial repository path decision:

- `/home/mak/operre/repo`

Repository visibility decision:

- temporarily public for inspection/setup;
- normally should be private;
- future public repo may exist for public docs/distribution.

## 5. Initial repo audit plan from 2.odt

Initial read-only audit targets:

- Ubuntu Desktop environment;
- Git version;
- GitHub SSH access;
- git global config;
- pull.ff behavior;
- local repo existence;
- Operre remote state;
- LogisticSearch remote/local comparison;
- branch/HEAD status;
- clean/dirty worktree state;
- docs/TODO presence.

Accepted comparison principle:

- Operre does not need to copy LogisticSearch structure exactly.
- Operre should adopt the same seriousness and discipline.

## 6. Frontend framework decision

Options discussed:

- TypeScript + Vite + React;
- TypeScript + Vite + Solid;
- TypeScript + Vite + Svelte.

Accepted primary frontend:

- TypeScript + Vite + Solid.

Fallback:

- TypeScript + Vite + React.

Not first choice:

- TypeScript + Vite + Svelte.

Reasoning:

- Solid is lightweight and suitable for fast UI.
- Solid is a good fit for Operre core.
- React has a stronger ecosystem, useful fallback.
- Svelte is good but not the preferred direction.

## 7. Package manager decision

Options discussed:

- npm;
- pnpm.

Accepted package manager:

- pnpm.

Reasoning:

- better fit for monorepo/workspace structure;
- better disk efficiency;
- strict dependency discipline;
- better fit for apps/packages/extensions structure;
- better for future extension package architecture;
- good fit for Tauri + Solid + Vite + Monaco + extension architecture.

Rules:

- use pnpm only;
- commit `pnpm-lock.yaml` when implementation begins;
- use `pnpm-workspace.yaml` when workspace structure begins;
- pin pnpm through `packageManager` later;
- do not commit `package-lock.json`;
- do not commit `yarn.lock`;
- do not commit `bun.lockb`.

Future CI rule:

- `pnpm install --frozen-lockfile`

## 8. Tauri vs Electron decision

Accepted primary desktop framework:

- Tauri.

Fallback:

- Electron.

Reasoning for Tauri:

- lightweight product goal;
- smaller package direction;
- lower RAM target;
- Rust-native command layer;
- permission/capability model fits Operre security;
- future Android/iOS path remains open;
- better fit for privacy-first/local-first architecture.

Reasoning for Electron fallback:

- mature desktop ecosystem;
- predictable bundled Chromium;
- strong Node.js ecosystem;
- easier VS Code-like extension/tooling patterns;
- useful fallback if Tauri + Monaco + platform WebView creates unacceptable limitations.

Important caution:

- Tauri mobile support does not automatically make a good mobile UX.
- Operre needs adaptive ergonomics per platform.

## 9. Monaco and platform ergonomics decision

Accepted:

- Monaco performance/weight is not considered the primary mobile/tablet concern.
- Platform ergonomics are the main concern.

Design rule:

> Same core. Adaptive ergonomics.

Desktop ergonomics:

- keyboard;
- mouse;
- multiple panels;
- broad workspace;
- folder tree;
- split editor;
- minimap.

Tablet ergonomics:

- touch;
- optional external keyboard;
- simplified panel switching;
- adaptive minimap behavior;
- larger hit targets.

Phone ergonomics:

- single-file focus;
- fast notes;
- small edits;
- preview-oriented workflows.

## 10. Platform order decision

Accepted platform order:

1. Linux Desktop
2. Windows Desktop
3. macOS Desktop
4. Tablet/mobile later

Earlier platform wording included Android/iOS future because Tauri can keep that path open, but current product order remains desktop-first.

## 11. Sync strategy from 2.odt

Accepted direction:

- local-first;
- privacy-first;
- no mandatory Operre cloud for user-created work data;
- optional user-owned sync later;
- extension/data-domain level sync.

User-created work data examples:

- TODO lists;
- work plans;
- service plans;
- notes;
- project docs;
- personal boards;
- local project metadata.

Possible sync ownership:

- user devices;
- user storage;
- self-hosted storage;
- user's chosen ecosystem.

Important distinction:

- Operre may need servers for app/extension/update/license/marketplace services.
- User-created work data should remain local-first and sync only by explicit user choice.

## 12. 2.odt accepted decisions summary

Accepted decisions extracted from `2.odt`:

- Operre / operre.com confirmed.
- Operre is independent and lightweight.
- Operre starts like old Windows 10 Notepad.
- Operre is not open source.
- Basic/core may be free.
- Future extensions may be paid.
- GitHub and Ideboard are not core.
- Repo normally should be private.
- Repository documentation is English-only.
- Development is audit/TODO/documentation driven.
- Frontend primary: TypeScript + Vite + Solid.
- Frontend fallback: React.
- Svelte is not first choice.
- Package manager: pnpm.
- Desktop primary: Tauri.
- Desktop fallback: Electron.
- Editor engine: Monaco.
- Platform order: Linux, Windows, macOS, tablet/mobile later.
- Monaco weight is not the main mobile concern; ergonomics are.
- Sync is local-first and optional.
- User-owned sync is important.
