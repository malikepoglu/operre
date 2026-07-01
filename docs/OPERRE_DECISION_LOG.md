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

### Auto Save, file saving, atomic write, and backup behavior decided

Accepted memory:

- Auto Save, file saving, atomic write, and backup behavior must have a dedicated specification.
- Auto Save is OFF by default.
- Auto Save can be enabled by user preference.
- The project owner may not personally use Auto Save, but Operre must support user-controlled opt-in Auto Save.
- Auto Save, Manual Save, Save As, Hot Exit, Crash Recovery, Session Restore, Atomic Write, and Backup are separate concepts.
- Manual Save and Save As must be safe and conflict-aware.
- Save failure must preserve dirty buffer.
- External changes must never silently overwrite dirty buffers.
- Settings and keybindings require atomic write.
- Settings and keybindings require last-known-good backup.
- User files may use atomic write where safe and practical, but symlink/network/metadata risks must be respected.
- Normal user file backups should not be aggressive by default.
- Large/protected/secret-like files require save warnings and strict privacy boundaries.
- File contents, dirty buffer contents, backup content, and recovery content are not logged.
- Backup/recovery content is not included in diagnostics export by default.

Next continuation point:

- define symlink, hardlink, special file, and file watcher behavior.

### Symlink, hardlink, special file, and file watcher behavior decided

Accepted memory:

- Symlink, hardlink, special file, and file watcher behavior must have a dedicated specification.
- Operre must not silently change filesystem semantics.
- Operre must distinguish path, canonical path, symlink path, target path, and file identity where practical.
- lstat/stat distinction is required by design.
- Symlink files may be opened, but link/target distinction must be visible where useful.
- Saving through symlink must not silently replace the symlink itself with a regular file.
- Broken symlink warning is required.
- Symlink loop detection is required.
- Hardlink count greater than 1 should trigger warning where supported.
- Atomic write must not silently break hardlink semantics for user files.
- Special files must not be treated as normal text files.
- Sparse and binary files require cautious handling.
- File watcher must detect external changes and workspace tree changes where practical.
- Dirty buffers must never be silently overwritten by external reload.
- Watcher debounce, deduplication, overflow handling, and rescan are required by design.
- Internal save events must be distinguished from external changes where practical.
- Watcher limits and network/removable filesystem unreliability must be visible.
- Protected paths must remain privacy-first in watcher behavior.
- AI and extensions cannot access watcher event history by default.

Next continuation point:

- define File Explorer, workspace tree, File Info, tabs, and navigation behavior.

### File Explorer, workspace tree, File Info, tabs, and navigation behavior decided

Accepted memory:

- File Explorer, workspace tree, File Info, tabs, and navigation behavior must have a dedicated specification.
- Users must always understand where they are in the filesystem and workspace.
- Explorer, tabs, breadcrumbs, recent files, search results, Problems, and Command Palette must share the same file identity model.
- v0.1 supports single file and single folder/workspace; multi-root workspace remains a future-compatible design target.
- Workspace root must be explicit.
- Hidden file visibility is separate from protected path access.
- Protected path policy applies inside Explorer.
- File Info is a first-class surface.
- Tabs must show dirty/read-only/external-changed/deleted/conflict states.
- Tab identity must not be only a path string.
- Same target opened through different symlink paths must not be silently merged.
- Dirty buffers must never be silently discarded by Explorer, tab, reload, or navigation actions.
- Dangerous Explorer actions require confirmation.
- Large workspace lazy loading and tree virtualization are required by design.
- Watcher events must update Explorer through debounce/rescan behavior.
- AI and extensions cannot access Explorer tree or navigation history by default.

Next continuation point:

- define panels, sidebars, activity bar, layout persistence, and view management behavior.

## OPR-SPEC-0035 - Panels, Sidebars, Activity Bar, Layout Persistence, and View Management

Decision: Accepted.

Operre will define a workbench model using Activity Bar entries, view containers, sidebars, panels, editor area, command IDs, persisted machine-local layout state, and permission-scoped view ownership.

Key decisions:

- VS Code is a useful reference for proven workbench patterns, not a complexity target.
- Operre should keep useful patterns such as activity-driven navigation, view containers, command-driven focus, resettable layout, Problems/Logs/Diagnostics surfaces, and keyboard-first flow.
- Operre should improve the model through fewer default surfaces, clearer labels, stricter privacy, explicit extension boundaries, and local-only layout state by default.
- v0.1 includes Activity Bar, primary sidebar, Explorer, Search, Recent, Problems, Extensions shell, Settings, basic bottom panel, Problems, Logs, Diagnostics, Search Results, collapse/resize behavior, layout reset, keyboard navigation, and touch/high-DPI baseline.
- Terminal, Debug, Git, AI, secondary sidebar, and language toolchain/runtime features remain later optional extension or connector surfaces.
- Layout state is machine-local by default and not synced by default.
- AI and extensions cannot read layout state, Recent history, Explorer state, Problems, Logs, or Diagnostics by default.
- The later programming language toolchain/runtime extension track may include compilers, interpreters, simulators, emulators, linkers, executable builders, package builders, live runtime/REPL surfaces, language servers, debuggers, build/test runners, problem matchers, formatters, linters, and language-specific project templates.
- These language toolchain/runtime capabilities must remain extension-driven, Workspace-Trust-aware, permission-scoped, audited, and never required by Operre core.

Next topic: Menus, toolbar, titlebar, status bar, and workbench chrome behavior.

## OPR-META-0001 - Periodic repository audit cadence

Decision: Accepted.

Operre must run a detailed terminal-based GitHub repository audit after every 20 completed meaningful repository workflow steps. This rule exists to prevent repeated planning loops, contradictory specifications, stale TODO state, missing next-topic markers, local/remote drift, and hidden documentation inconsistencies.

The audit may be run earlier after failed audits, failed pushes, unexpected dirty worktrees, new conversation handoffs, major scope changes, overlapping topics, or before implementation begins.

After the audit, work should continue only after a done/queued/risk/next-action summary is produced.

## OPR-SPEC-0036 - Menus, Toolbar, Titlebar, Status Bar, and Workbench Chrome

Decision: Accepted.

Operre will define a responsive workbench chrome model for menus, toolbar, titlebar, status bar, command surfaces, high-DPI displays, tablets, phones, laptops, MacBooks, external displays, and mixed-DPI environments.

Key decisions:

- VS Code is a useful reference for command-driven chrome, but Operre must be calmer and less crowded.
- The Notepad++ on a 4K 27-inch monitor failure mode is an explicit anti-pattern.
- Menus, toolbar buttons, titlebar controls, status bar items, badges, and overflow controls must remain readable, reachable, scalable, and ergonomic.
- UI scale and editor font size are separate.
- Workbench chrome must not rely on hard-coded pixel-only sizing.
- Toolbar and status bar must use overflow behavior instead of shrinking controls into unusable sizes.
- Phone and tablet layouts must not depend on desktop menubar assumptions.
- Native titlebar behavior is preferred for v0.1 where practical.
- Run, Debug, Terminal, Git, AI, compiler, interpreter, simulator, emulator, linker, executable builder, and runtime chrome remain later optional extension or connector surfaces.
- Security and privacy indicators must be visible but calm.
- Extension-contributed chrome must be declared, permission-scoped, user-hideable, and unable to bypass Workspace Trust.

Next topic: Problems, search results, output, logs, and diagnostics panel detailed behavior.

## OPR-SPEC-0037 - Problems, Search Results, Output, Logs, and Diagnostics Panel Behavior

Decision: Accepted.

Operre will define structured Problems, Search Results, Output, Logs, and Diagnostics panels with privacy-first defaults, redaction, command integration, large-list ergonomics, high-DPI behavior, device-specific capability limits, and future desktop/workstation diagnostic depth.

Key decisions:

- Output and Diagnostics may eventually approach Visual Studio-like depth on desktop/workstation platforms.
- v0.1 Output remains a safe basic shell.
- Build output, runtime output, compiler diagnostics, test output, terminal output, and debug console are later extension or process-execution topics.
- Diagnostics are local-first, user-initiated, previewed before export, and redacted by default.
- Diagnostics upload, crash upload, and telemetry are OFF by default.
- Logs are local-only by default and inaccessible to AI/extensions without scoped permission.
- Phone and tablet modes are limited to safe summaries, syntax-like checks, restricted Problems, restricted Search Results, and local app health summaries.
- Phone and tablet modes must not expose full Output, terminal output, build/run/debug output, runtime sessions, unbounded logs, or dense diagnostic tables by default.
- AI and extensions cannot read Problems, Search Results, Output, Logs, or Diagnostics by default.
- Open UI does not imply data access.

Next topic: Extension contribution points and manifest schema.

## OPR-SPEC-0038 - Extension Contribution Points and Manifest Schema

Decision: Accepted.

Operre will use a manifest-driven extension architecture with TypeScript/JavaScript as the core extension control plane, sandboxed extension hosts, default-deny permissions, explicit contribution points, local install support, private registry planning, profile-aware sync planning, and later brokered desktop/workstation external toolchain integration.

Key decisions:

- TypeScript/JavaScript is the core extension control plane.
- C, C++, Python, JavaScript runtimes, database tools, web tools, compilers, interpreters, simulators, emulators, linkers, executable builders, package managers, and live runtime tools are later external toolchain/runtime integrations, not core in-process plugin runtimes.
- Operre should coordinate license-compatible external tools through brokers instead of embedding unsafe native runtimes into the core.
- A public marketplace is not required for early use; local unpacked folders, local packages, development paths, and a private registry are enough for early extension testing and distribution.
- A single VPS can support the first private registry.
- Package trust must rely on signatures, hashes, publisher identity, compatibility metadata, revocation metadata, and client-side verification; client-side verification is required.
- Sync must be profile-aware and device-aware.
- Phone and tablet extension capability is intentionally limited.
- Workspace Trust gates risky capabilities.
- Open UI does not imply data access.

Next topic: Extension permission UI and approval flow.

## OPR-SPEC-0039 - Extension Permission UI and Approval Flow

Decision: Accepted.

Operre will use install-time permission summaries, runtime critical permission prompts, scoped grants, duration choices, visible risk bars, status bar persistence, update permission policy, Developer Mode for local extensions, phone/tablet disabled capability display, revocation controls, Safe Mode, and audit logging.

Key decisions:

- Install-time summary plus runtime critical prompts is the permission timing model.
- Permission duration supports deny, allow once, session, workspace, machine, until extension update, and until revoked.
- Permission scope supports file, folder, workspace, glob, domain, URL pattern, command, panel, output channel, diagnostics session, problem source, search session, executable path, toolchain profile, and AI session.
- Risk levels are Low, Medium, High, Very High, and Critical.
- Permission risk bars appear below the toolbar and above the editor or working surface.
- Warning bars do not auto-dismiss and critical alert bars require acknowledgement.
- Dismissed warnings leave status bar summaries.
- Colors are customizable but cannot be the only meaning carrier.
- Extension update policy B is the default and recommended reset behavior.
- Users may choose update policies A, B, C, or D.
- Permission grants do not sync silently.
- Local and unpacked extensions require Developer Mode.
- Phone and tablet show unsupported risky capabilities as disabled with desktop required.
- Revocation dashboard, revoke all, Safe Mode, suspicious request handling, and audit logging are required.
- Technical permission ID and user-friendly explanation must be shown together.
- Open UI does not imply data access.

Next topic: Workspace Trust deep behavior.

## OPR-SPEC-0040 - Workspace Trust Deep Behavior

Decision: Accepted.

Operre will use a scoped, revocable, device-local Workspace Trust model with opening-time trust bars, runtime prompts for dangerous actions, restricted mode, granular trust scopes, per-root multi-root behavior, extension-aware trust, toolchain-aware trust, trust review needed, status bar state, and strict no-sync defaults.

Key decisions:

- Workspace Trust uses both opening-time bars and runtime prompts.
- Global trust is unavailable by default or strongly discouraged.
- Trust decisions do not sync by default.
- Untrusted workspaces keep basic editing available.
- Code execution, data exfiltration, AI workspace access, protected paths, secrets, extension scans, and external toolchain actions remain locked.
- Workspace identity uses path, roots, optional repo remote, local workspace ID, and safety metadata.
- Multi-root trust is tracked per root.
- Trust review needed appears after meaningful risk changes.
- Trust bars can be red critical, yellow warning, or light-blue info.
- Dismissed trust bars leave status bar state where relevant.
- Extension trust requires package verification, workspace trust, permissions, and device capability.
- External toolchain and live runtime require the full trust and approval chain.
- Phone and tablet show unsupported risky actions as disabled with desktop required.
- Open UI does not imply data access.

Next topic: Safe terminal and process execution model.

## OPR-SPEC-0041 - Safe Terminal and Process Execution Model

Decision: Accepted.

Operre will support a powerful but brokered terminal and process execution
model. The default remains safe, but advanced users can enable stronger
terminal modes, including full guarded terminal mode, through settings.

Key decisions:

- Terminal modes A, B, C, and D are supported.
- The recommended default is A plus B.
- Terminal mode D is full guarded terminal with per-action approval.
- Execution is brokered through Permission Broker, Workspace Trust Broker,
  Process Execution Broker, and Toolchain Broker where applicable.
- Silent shell launch is forbidden.
- Command preview is required for risky commands.
- Log ID and log file path must be visible.
- Working directory path and log file path should be clickable.
- Environment variables are sanitized by default.
- Secrets are not injected automatically.
- Sudo, administrator, and root are disabled by default but may be enabled
  by advanced users with critical warnings and per-operation approval.
- Package managers are high-risk or very-high-risk.
- Build, run, debug, test, live runtime, and REPL are separate categories.
- AI cannot directly execute commands by default.
- Phone and tablet do not get full local terminal by default.
- Open UI does not imply data access.

Next topic: External toolchain and live runtime broker model.

## OPR-SPEC-0042 - External Toolchain and Live Runtime Broker Model

Decision: Accepted.

Operre will use a brokered external toolchain and live runtime model.
Toolchains are profile-based, permission-gated, trust-aware,
resource-governed, audited, and dashboard-visible.

Key decisions:

- Toolchain Broker is a separate security and coordination layer.
- Every external tool uses a toolchain profile.
- Profile states include discovered, pending review, approved, blocked,
  quarantined, review needed, deprecated, and missing.
- Toolchain install modes are A, B, C, and D with A plus B as default.
- Auto discovery suggests profiles but does not approve them.
- operre.worksRoot defines the managed Works root.
- External workspaces are not modified by default.

- External workspaces must not be modified with outputs, logs, or artifacts folders by default.
- Python prefers project-local venv.
- C and C++ build, run, debug, linker, and artifact profiles are
  separated.
- Node and package managers are supply-chain-sensitive.
- MongoDB and NoSQL database tools are in scope.
- Database tools are secret-aware and migration-risk-aware.
- Web development servers are live runtime sessions.
- Resource Governor is required.
- Sandbox planning is layered.
- Toolchain installation is detect-and-guide by default.
- Extensions may contribute templates but cannot force execution.
- AI is advisory by default.
- Phone and tablet use safe summaries and desktop-required disabled
  actions.
- Production system guard is required.
- Remote toolchains are later and disabled by default.
- Profile templates may sync, but executable approvals, paths, secrets,
  and production approvals must not sync silently.

- Profile templates may sync, but executable approvals, paths, secrets, and production approvals must not sync silently.
- Per-project Toolchains dashboard is required.
- Safe reset is mandatory.

Next topic: Managed Works projects templates and project dashboard behavior.

## OPR-SPEC-0043 - Managed Works Projects Templates and Dashboard

Decision: Accepted.

Operre will support managed Works projects and external workspaces as
separate modes. Managed projects use a predictable Works root, templates,
dashboards, outputs, logs, artifacts, and safe reset. External workspaces
remain non-invasive by default.

Key decisions:

- Managed projects and external workspaces are separate modes.
- Managed projects are required.
- operre.worksRoot defines the managed Works root.
- Folder creation uses C plus B by default.
- The `.operre` protected local shared boundaries are required.
- External workspaces are not modified by default.
- Templates are declarative and do not execute commands.
- Project Dashboard is a central project control surface.
- Dashboard default behavior is C plus B.
- Dashboard includes security summary.
- Project Dashboard links to Toolchains Dashboard.
- Outputs, logs, and artifacts are visible and manageable.
- Cleanup and retention policy is required.
- Special project names stay out of public specification.
- Project-level safe reset is mandatory.
- Phone and tablet show safe project summaries.
- First implementation starts with skeleton and ergonomic guidance.

Next topic: Diagnostics dashboard deep behavior.

## OPR-SPEC-0044 - Diagnostics Dashboard Deep Behavior

Decision: Accepted.

Diagnostics Dashboard is required as a deep project health surface.
Diagnostics remains separate from Problems, Output, Logs, and Project
Dashboard.

Key decisions:

- Diagnostics Dashboard is required.
- Diagnostics is an interpreted project health surface, not only an error
  list.
- Diagnostics items must carry severity and confidence.
- Every diagnostics item must show its source.
- AI cannot read Diagnostics by default.
- Extensions may contribute diagnostics only through declared providers
  and permissions.
- Fix actions must not run hidden commands.
- Noise control is required.
- Retention, privacy, redaction, and export controls are required.
- Production diagnostics require production guard.
- Remote diagnostics are planned, disabled by default, and must not be
  forgotten.
- Phone and tablet show safe diagnostics summaries.
- First implementation starts with diagnostics schema and dashboard
  skeleton.

Next topic: Extension marketplace package signing and update distribution behavior.
