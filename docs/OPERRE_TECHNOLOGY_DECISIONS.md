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

## Source 2 detailed technology baseline

The `2.odt` review confirms the current baseline:

- Desktop framework: Tauri primary.
- Desktop fallback: Electron.
- Editor engine: Monaco Editor.
- Frontend: TypeScript + Vite + Solid.
- Frontend fallback: TypeScript + Vite + React.
- Svelte is not first choice.
- Package manager: pnpm.

Decision rationale:

- Tauri better matches the lightweight, privacy-first, local-first direction.
- Electron remains useful as fallback because it is mature and Chromium behavior is predictable.
- Solid better matches lightweight UI goals.
- React remains fallback because ecosystem strength may matter later.
- pnpm better matches future monorepo and extension package structure.

Future implementation tests required:

- Tauri + Solid + Monaco on Linux Desktop;
- startup time;
- memory use;
- large `.txt` behavior;
- Markdown editing and preview;
- syntax highlighting for default file types;
- WebView behavior differences;
- packaging size;
- security permission model fit.

## Large file architecture baseline

Accepted technology direction:

- Operre must not require full-file memory loading for very large files.
- File access should support streaming/chunked readers.
- Editor state should support Large File Mode flags.
- Long-running indexing/search/compare operations must be cancellable.
- Very large file search should be streaming-capable.
- Very large file compare should be line/chunk first.
- Cache and memory budgets must be configurable.
- UI must remain responsive during large file operations.

## Settings schema and migration baseline

Accepted technology direction:

- Settings must have schema validation.
- Settings schema version is required by design.
- Invalid settings must not crash Operre.
- Deprecated and unknown settings should be reported safely.
- Settings migration is required by design.
- JSONC support is required for user-editable settings.

## Command and keybinding architecture baseline

Accepted technology direction:

- Commands must have stable command identifiers.
- Keybindings must resolve through the command system.
- Keybindings must support context conditions.
- Keybindings must support platform-specific bindings.
- Keybindings must support validation and conflict detection.
- Architecture must not block chord shortcuts.
- Architecture must support on-screen keyboard, touch, and touchpad ergonomics.

## Display, DPI, and responsive architecture baseline

Accepted technology direction:

- Operre must be high-DPI aware.
- Fractional scaling must be supported by design where platform allows.
- Per-monitor DPI changes must not break layout.
- Responsive layout system is required by design.
- Safe window restore is required by design.
- On-screen keyboard avoidance must be supported by design.
- Window geometry is machine-local state and must not sync by default.
- Detailed breakpoint and scaling rules need a later implementation pass.

## Command system architecture baseline

Accepted technology direction:

- Operre requires a core command registry.
- Menus, keybindings, context menus, Settings UI, extensions, AI commands, and Command Palette must use the same command system.
- Commands must have stable IDs and metadata.
- Commands must support context/when conditions.
- Commands must support disabled reasons.
- Commands must support dangerous/confirmation metadata.
- Command execution must integrate with future error/warning/problem reporting.

## Error, warning, notification, and Problems architecture baseline

Accepted technology direction:

- Operre needs a structured severity model.
- Operre needs a Problems model.
- Command execution must integrate with visible error reporting.
- Settings validation must integrate with Settings Problems.
- Diagnostics export must be privacy-safe by design.
- Structured error codes should not be blocked by architecture.

## Logs and diagnostics architecture baseline

Accepted technology direction:

- Logs are local-only by default.
- Diagnostics export is user-initiated only.
- Automatic diagnostics upload is forbidden by default.
- Redaction is required before diagnostics export.
- Log rotation and retention are required by design.
- Structured diagnostics manifest should be supported by design.
- Crash recovery data is a separate behavior area.

## Crash recovery architecture baseline

Accepted technology direction:

- Crash Recovery, Auto Save, Hot Exit, and Session Restore are separate concepts.
- Recovery data is local-only and machine-local by default.
- Atomic write is required for settings and keybindings.
- Safe Mode is required by design.
- Recovery conflict detection is required by design.
- AI and extensions cannot access recovery content by default.
