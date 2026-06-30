# Operre Technology Decisions

## Primary stack

Accepted primary stack:

- Tauri;
- Rust native side through Tauri;
- Monaco Editor;
- TypeScript;
- Vite;
- Solid;
- pnpm.

## Fallbacks

Fallbacks:

- Electron as desktop fallback;
- React as frontend fallback;
- Svelte not first choice.

## Frontend decision

Accepted:

- TypeScript + Vite + Solid.

Reasoning:

- lightweight UI target;
- fine-grained reactivity;
- suitable for a fast Tauri desktop UI;
- good fit for Operre's lightweight core goal.

Fallback:

- TypeScript + Vite + React.

Reasoning:

- large ecosystem;
- useful fallback if Solid creates unacceptable limitations.

Not first choice:

- Svelte.

## Package manager decision

Accepted:

- pnpm.

Reasoning:

- better fit for future monorepo/workspaces;
- better disk efficiency;
- stricter dependency discipline;
- good fit for apps/packages/extensions layout;
- good fit for extension-based architecture.

## Desktop framework decision

Accepted primary framework:

- Tauri.

Fallback:

- Electron.

Reasoning for Tauri:

- lightweight product goal;
- smaller package direction;
- lower RAM target;
- Rust-native command layer;
- stronger fit with explicit permissions/capabilities;
- future Android/iOS path remains open;
- better match for privacy-first/local-first architecture.

Reasoning for Electron fallback:

- proven desktop maturity;
- predictable Chromium runtime;
- strong Node.js ecosystem;
- easier VS Code-like extension/tooling patterns;
- fallback if Tauri + Monaco + platform WebView behavior creates unacceptable limitations.

## Monaco decision

Monaco Editor is the preferred editor engine.

Important distinction:

- Monaco is the editor engine.
- Monaco is not the full VS Code workbench.
- Monaco does not provide the complete VS Code extension system.
- Explorer, Activity Bar, command palette, settings, extension host, permissions, Git UI, AI security, and workbench behavior must be designed by Operre.

Implementation rules:

- verify official Monaco license before dependency addition;
- preserve required license notices;
- audit wrapper packages separately;
- do not use VS Code or Microsoft branding.

## VS Code reference

VS Code is an architectural reference for usability, not a product clone target.

Useful ideas:

- Monaco Editor;
- Activity Bar;
- Sidebar;
- Explorer;
- tabs;
- split editor;
- status bar;
- command palette;
- extension manifest;
- activation events;
- contribution points;
- extension host separation;
- language-scoped activation;
- Workspace Trust;
- webviews;
- secret storage.

Operre must be smaller and stricter.

## Cursor reference

Cursor is an AI-first reference, not Operre's product model.

Cursor-like ideas must be handled cautiously:

- AI chat/composer;
- inline AI editing;
- codebase indexing;
- cloud/local agent workflows.

Operre must not copy cloud-first AI assumptions.

## Platform order

Initial target order:

1. Linux Desktop
2. Windows Desktop
3. macOS Desktop
4. Tablet/mobile later

## Ergonomics rule

Monaco Editor weight is not considered the primary mobile problem.

The primary problem is ergonomics.

Rule:

> Same core. Adaptive ergonomics.

Desktop:

- keyboard;
- mouse;
- multi-panel layout;
- split editor;
- folder tree;
- minimap.

Tablet:

- touch;
- optional keyboard;
- simplified panel switching;
- adaptive minimap behavior;
- larger hit targets.

Phone:

- fast notes;
- small edits;
- preview;
- focused single-file workflows.
