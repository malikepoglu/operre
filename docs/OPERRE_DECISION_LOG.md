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

### 5.odt processed

Accepted memory extracted from `5.odt`:

- Initial repository documentation baseline succeeded.
- Operre repo path is `/home/mak/operre/repo`.
- GitHub SSH workflow works.
- Post-push audit is mandatory.
- Conversation import area is local-only.
- Raw full transcript must not be committed by default.
- Documentation should preserve accepted decisions, not raw chat dumps.
- Source files must be processed in order from 1.odt to 5.odt.
- Terminal code blocks must be Bash-compatible and prompt-safe.
- UI rendering errors must be verified against terminal/git audit.
- Ordered source review pass is complete through 5.odt.

Next continuation point:

- continue product decisions after delete behavior.

### Hidden files and protected paths decided

Accepted memory:

- Hidden files and dotfiles are hidden by default.
- Explorer requires a Show Hidden Files toggle.
- `.operre/` is hidden by default and protected when visible.
- `.git/` is hidden by default and protected when visible.
- `.operre/audit/`, `.operre/secrets/`, `.operre/cache/`, `.operre/local-state/`, and `.operre/snapshots/` are always protected.
- `.operre/shared/` is the only optional shared/tracked `.operre` subtree.
- Sensitive dotfiles such as `.env` are hidden and excluded from search/recent by default where practical.
- Search excludes hidden/protected paths by default.
- Recent history excludes protected paths by default.
- AI and extensions cannot access hidden/protected paths without explicit scoped permission.

Next continuation point:

- define detailed search behavior.

### Search, replace, and file compare decided

Accepted memory:

- Current file search is required.
- Opened folder/project search is required.
- Replace in current file is required.
- Replace in files requires preview and confirmation.
- Search excludes hidden/protected/generated/binary paths by default.
- Include Hidden Files may include hidden files but not protected paths by default.
- File compare is required.
- Two-file side-by-side compare is required.
- Two-file stacked compare is required.
- Multi-file compare must be supported by design.
- Differences may use red background-color.
- Same/identical content may optionally use green background-color.
- Compare UI details must be user-configurable.
- Compare follows hidden/protected path safety rules.
- AI and extensions cannot access search/compare contents without explicit scoped permission.

Next continuation point:

- define Recent files/projects behavior.

### Large file memory and cache behavior decided

Accepted memory:

- Large file support must be part of architecture from the beginning.
- Very large files must not be loaded fully into RAM blindly.
- Large File Mode is required.
- Very Large File Mode / streaming mode is required as a design target.
- Read-only fallback is required.
- Streaming/chunked reading is required as a design target.
- Lazy syntax highlighting is required for large files.
- Minimap and semantic tooling may be disabled above thresholds.
- Large file search should be streaming-capable.
- Large file compare should be line/chunk first.
- Word/character diff may be disabled automatically for large files.
- Cache must be bounded, cleanable, local-only, and protected.
- Memory budget settings are required.
- User must be able to configure thresholds and behavior.
- AI and extensions cannot access large file content without explicit scoped permission.

Next continuation point:

- define Recent files/projects behavior.

### Recent files/projects behavior decided

Accepted memory:

- Recent Files is required.
- Recent Projects/Folders is required.
- Pinned recent items are required.
- Startup screen must show Recent Projects and Recent Files.
- Recent history and Session Restore are separate concepts.
- Recent history is local-only by default.
- Sensitive/protected files are excluded by default.
- User can clear recent history.
- Missing files/projects are shown as missing, not noisy errors.
- Search history is separate from Recent Files.
- Recent Comparisons may be added later and must be separate.
- Large files can appear in Recent Files with a Large File marker.
- AI and extensions cannot access recent history by default.
- Sync/export of recent history is OFF by default and requires explicit user consent if added later.

Next continuation point:

- define Settings UI and settings schema behavior.

### Settings UI and settings schema behavior decided

Accepted memory:

- Settings UI is required.
- `settings.jsonc` is required.
- JSONC comments are accepted.
- JSON schema validation is required.
- Invalid settings must not crash Operre.
- Settings Problems panel is required by design.
- User settings and Workspace/Project settings are separate.
- Machine-local settings are separate and not synced by default.
- Secret/token/password values must not be stored in settings files.
- Secret Vault / OS keyring is separate from settings.
- Privacy/security defaults are OFF/safe by default.
- Settings search, Reset to Default, and modified indicators are required.
- Settings import/export may come later but must be designed safely.
- Settings schema version and migration are required by design.
- Workspace Trust can restrict workspace settings.
- Extension and AI settings cannot bypass permission systems.

Next continuation point:

- define keyboard shortcut and keybinding behavior.

### Keyboard, keybindings, and input ergonomics decided

Accepted memory:

- Keyboard shortcuts are required.
- Command identifier system is required.
- Command Palette, menus, Settings UI, context menus, and keybindings use the same command system.
- `keybindings.jsonc` is required.
- JSONC comments are accepted.
- Schema validation is required.
- Conflict detection is required.
- Shortcut editing through Settings UI is required.
- Reset shortcut and Reset all shortcuts are required.
- User keybindings and workspace keybindings are separate.
- Workspace Trust can restrict workspace keybindings.
- Extension and AI shortcuts cannot bypass permission systems.
- Dangerous commands still require confirmation.
- Linux/Windows/macOS shortcut differences must be supported.
- Turkish/German/English keyboard layout differences must be considered.
- Chord shortcuts must not be blocked by architecture.
- On-screen keyboard support is required by design.
- Touchscreen, tablet, phone, PC touchpad, and MacBook trackpad ergonomics must be supported by design.
- Touch and on-screen keyboard users must be able to use core workflows efficiently.

Next continuation point:

- define detailed Command Palette and command system behavior.

### Display, DPI, scaling, and responsive ergonomics decided

Accepted memory:

- Display, DPI, scaling, and responsive ergonomics must have a dedicated specification.
- UI scale and editor font size are separate concepts.
- High-DPI and fractional scaling must be supported by design.
- Multi-monitor different-DPI behavior must be considered.
- Responsive/collapsible layout is required by design.
- Compare view should adapt between side-by-side and stacked layouts.
- Touch mode and mouse mode may use different ergonomics.
- On-screen keyboard must not cover active editor/input areas where practical.
- MacBook screens, high-DPI, trackpads, and safe area/notch behavior must be considered.
- Window size and position are machine-local state and must not sync by default.
- Display/scale/font/touch/window behavior must be configurable.
- Accessibility and high contrast must remain compatible with scaling.
- This topic must be revisited later for a deeper detailed UI implementation pass.

Next continuation point:

- define detailed Command Palette and command system behavior.

### Command Palette and command system behavior decided

Accepted memory:

- Command Palette is required.
- Ctrl+Shift+P is the default shortcut.
- Core command registry is required.
- Every important action should have a command ID.
- Menus, keyboard shortcuts, context menus, Settings UI, extension commands, AI commands, and Command Palette use the same command system.
- Fuzzy command search is required.
- Command ID, title, category, shortcut, source, and disabled reason should be visible where practical.
- Dangerous commands require confirmation.
- Extension and AI commands cannot bypass permission systems.
- Workspace Trust can restrict command availability and execution.
- Command usage history is local-only by default.
- Command usage telemetry is OFF by default.
- Command Palette must support touch, on-screen keyboard, DPI scaling, and responsive layouts by design.
- Error, warning, notification, and problem reporting behavior must be a dedicated follow-up topic.
- Warning/error behavior must be configurable through Settings where safe.

Next continuation point:

- define error, warning, notification, and problem reporting behavior.

### Error, warning, notification, and problem reporting behavior decided

Accepted memory:

- Error, warning, notification, and problem reporting behavior must have a dedicated specification.
- Severity levels are required.
- Problems panel is required.
- Settings Problems relationship must be defined.
- Warning/error behavior must be configurable through Settings where safe.
- Critical safety warnings must not be disabled casually.
- Critical safety warnings must not be disabled silently.
- Toast, status bar, inline warning, banner, modal, Problems panel, Settings Problems, logs, and diagnostics export have distinct roles.
- Command Palette must provide access to Problems, Warnings, Notifications, Logs, and Diagnostics commands.
- Privacy-first diagnostics behavior is required.
- Diagnostics upload is OFF by default.
- File contents, secrets, and AI prompt/response content are not included automatically.
- File operation, large file, search/replace/compare, extension, AI, and Workspace Trust warnings must be considered.
- Accessibility, touch, DPI, and on-screen keyboard compatibility must be considered.

Next continuation point:

- define detailed logs and diagnostics export behavior.

### Logs and diagnostics export behavior decided

Accepted memory:

- Logs and diagnostics export behavior must have a dedicated specification.
- Logs are local-only by default.
- Diagnostics upload is OFF by default.
- Crash upload is OFF by default.
- Automatic diagnostics upload is forbidden by default.
- Diagnostics export is user-initiated only.
- Diagnostics export should show preview/summary before creation.
- Secret redaction is required.
- File contents are not included by default.
- AI prompts/responses are not included by default.
- Paths may be redacted in diagnostics export.
- Protected paths are redacted/excluded by default.
- Log rotation and retention are required by design.
- Settings must expose log level, retention, clear logs, export diagnostics, path redaction, diagnostics upload OFF, and crash upload OFF.
- Command Palette must expose Open Logs Folder, Clear Logs, Export Diagnostics, and related diagnostics commands.
- Extension/AI/security events may be included as summaries where safe.

Next continuation point:

- define detailed crash recovery and unsaved work recovery behavior.

### Crash recovery and unsaved work recovery behavior decided

Accepted memory:

- Crash Recovery and Unsaved Work Recovery behavior must have a dedicated specification.
- User-created unsaved work should not be lost easily.
- Crash Recovery, Auto Save, Hot Exit, and Session Restore are separate concepts.
- Crash Recovery is ON by default.
- Hot Exit is ON by default.
- Auto Save remains separate and configurable.
- Recovery data is local-only and machine-local by default.
- Recovery content is not included in diagnostics export by default.
- AI and extensions cannot access recovery content by default.
- Recovery UI/panel is required after crash when recoverable work exists.
- Recover, Compare, Save As, Keep Both, and Discard actions should be supported.
- Disk conflict handling is required.
- Untitled documents must be recoverable.
- Atomic write is required for settings and keybindings.
- Large file recovery must respect memory/cache limits.
- Protected/secret-like file recovery requires strict privacy boundaries.
- Safe Mode is required by design.
- Destructive recovery actions require confirmation.

Next continuation point:

- define Auto Save, file saving, atomic write, and backup behavior.
