# Operre Decision Log

## Accepted decisions through current planning

- Project name is Operre.
- Domain is operre.com.
- Operre is independent.
- Operre is not an Ideboard shell.
- Ideboard is a separate application/project.
- Ideboard may later be an optional Connector Extension.
- Operre is not planned as open source.
- Basic/core application may be free.
- Future extensions may be free or paid.
- Development repository should normally be private.
- Future public repo may be created for user-facing distribution/docs.
- GitHub repository is the project memory.
- Repository docs must be English-only.
- Chat discussion may remain Turkish.
- Current phase is specification consolidation.
- TODO implementation planning comes after specifications stabilize.
- Initial product should feel like old Windows 10 Notepad: very light and immediately writable.
- Windows 11 Notepad is not the reference.
- Core must stay small.
- Features grow through extensions/connectors.
- Preferred stack is Tauri + Rust + Monaco + TypeScript + Vite + Solid + pnpm.
- Electron is desktop fallback.
- React is frontend fallback.
- Svelte is not first choice.
- Platform order is Linux Desktop, Windows Desktop, macOS Desktop, tablet/mobile later.
- Monaco weight is not considered the main mobile problem; ergonomics are.
- Default workspace is `~/Operre/Works/`.
- Diagrams and Cad folders are separate.
- Installed extension code is separated from user work data.
- Default privacy mode is Strict Privacy.
- Crash upload, telemetry, diagnostics upload are OFF by default.
- Local safe logs are ON.
- Extension telemetry is denied by default.
- Product categories are Core, Built-in Features, Extensions, Connectors, Services.
- Do not use "module" as main product category.
- Git is optional Extension.
- GitHub is optional Connector Extension.
- Ideboard is optional Connector Extension.
- Extension system is VS Code-like but stricter.
- Default extension permission is deny all.
- Workspace Trust and Publisher Trust are required concepts.
- AI agents are optional Connector Extensions.
- AI cannot read full workspace, edit, run commands, access Git, access secrets, or send data by default.
- AI edits require diff before apply.
- AI actions must be logged one by one.
- Prompt/response logging is OFF by default and optional per project/per agent.
- `.operre/` is ignored by default.
- `.operre/shared/` may be tracked if explicitly chosen.
- `.operre/audit/`, `.operre/secrets/`, `.operre/cache/`, `.operre/local-state/`, `.operre/snapshots/` are always ignored.
- Startup screen includes recent files/projects, restore previous session, new text file, new Markdown note, open file, open folder/project, Operre Works shortcut.
- Session restore is ON by default.
- Autosave is OFF by default.
- Dirty files show `*`.
- Close warning offers Save / Don't Save / Cancel.
- Crash recovery is ON, local-only, never silently overwrites files.
- Crash recovery retention default is 7 days.
- Default encoding is UTF-8 without BOM.
- UTF-8 with BOM option exists.
- Existing BOM is preserved.
- New files default to LF on all platforms.
- Existing line endings are preserved.
- Indentation is language-aware, spaces by default, existing indentation preserved.
- Default theme follows system.
- Default editor font is system monospace.
- Multiple tabs are supported.
- Vertical split editor is first; horizontal later.
- Markdown opens in edit mode by default.
- Markdown preview can be preview only, side-by-side, or live preview.
- Markdown preview blocks scripts and remote resources by default.
- Markdown security warning is a web-browser-like yellow top bar.
- Minimap is ON by default on the right.
- Status Bar exists.
- Command Palette exists with Ctrl+Shift+P.
- Keyboard shortcuts are configurable through keybindings.json.
- Classic menu: File, Edit, View, Go, Tools, Extensions, Help.
- Activity Bar: Explorer, Search, Recent, Extensions, Settings.
- Explorer scope defaults to user-opened folder/project only.
- Delete moves to OS Trash/Recycle Bin by default.
- Permanent delete is separate.
- Every delete requires confirmation.
- Folder delete requires extra warning.

## Current continuation point

Continue product decisions after delete behavior.

Next decisions should cover:

- detailed permanent delete behavior;
- OS Trash/Recycle Bin implementation;
- Search behavior;
- Recent files/projects behavior;
- Settings UI/schema.

## Source review processing

### 1.odt processed

Accepted memory extracted from `1.odt`:

- VS Code is an architecture/usability reference, not a clone target.
- Cursor is an AI-first reference, not a product model.
- Monaco Editor is the preferred editor engine candidate.
- Monaco is not the full VS Code workbench.
- Operre must design its own workbench, extension model, permissions, and security model.
- AI must be optional, permission-scoped, auditable, and diff-before-apply.
- Monaco and all wrappers/dependencies require license audit before implementation.
- Ideboard remains separate.
- Diagrams/CAD remain future direction and must not bloat first core.

### 2.odt processed

Accepted memory extracted from `2.odt`:

- Operre / operre.com product identity confirmed.
- Operre starts as old Windows 10 Notepad-like lightweight editor/workspace.
- Core must stay small and immediately useful for `.txt`.
- GitHub and Ideboard are not core; they are future extensions/connectors.
- Frontend primary stack is TypeScript + Vite + Solid.
- React is fallback; Svelte is not first choice.
- Package manager is pnpm.
- Desktop primary framework is Tauri; Electron is fallback.
- Platform order is Linux Desktop, Windows Desktop, macOS Desktop, tablet/mobile later.
- Monaco performance is not the main mobile concern; ergonomics are.
- Sync should be local-first, privacy-first, optional, and user-owned when possible.

### 3.odt processed

Accepted memory extracted from `3.odt`:

- Default privacy mode is Strict Privacy.
- Crash upload, telemetry, diagnostics upload are OFF by default.
- Local safe logs are ON.
- Extension telemetry is denied by default.
- Product categories are Core, Built-in Features, Extensions, Connectors, Services.
- Extension system is VS Code-like but stricter.
- Default extension permission is deny all.
- Extensions must declare manifest, activation events, contributions, capabilities, permissions, language scopes, and extension type.
- Workspace Trust and Publisher Trust are required concepts.
- Webviews must be sandboxed and CSP controlled.
- Secret Vault is required.
- AI agents are optional Connector Extensions.
- AI access must be selected/scope-based only.
- AI edits require diff before apply.
- Every AI action must be logged.
- Prompt/response logging is OFF by default and optional per project/per agent.
- `.operre/` uses hybrid Git model with audit/secrets/cache/local-state/snapshots always ignored.

### 4.odt processed

Accepted memory extracted from `4.odt`:

- Tab system accepted.
- Vertical split editor accepted.
- Markdown edit/preview behavior accepted.
- Markdown preview security accepted.
- Browser-like yellow warning bar accepted for blocked Markdown preview content.
- Minimap accepted and default ON.
- Status Bar accepted.
- Command Palette accepted with Ctrl+Shift+P.
- Keyboard shortcuts are configurable through keybindings.json.
- Classic menu accepted.
- Activity Bar/Sidebar accepted.
- Ideboard remains separate and later optional Connector Extension.
- Explorer/folder tree first version accepted.
- Delete behavior baseline accepted: OS Trash/Recycle Bin by default, Permanent Delete separate, confirmations required.
- Initial GitHub documentation/memory direction accepted.
