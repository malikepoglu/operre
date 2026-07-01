# Operre UI/UX Specification

## UI reference

Operre should learn from VS Code usability but remain smaller and lighter.

Operre is not a VS Code clone.

## Startup screen

Startup screen should show:

- recent files/projects;
- restore previous session / reopen open files;
- new text file;
- new Markdown note;
- open file;
- open folder/project;
- Operre Works shortcut.

## Session restore

Session restore:

- default: ON;
- user can disable it.

Saved:

- open files;
- open folder/project;
- active tab;
- cursor position;
- scroll position;
- split/panel layout.

Not saved:

- file contents;
- clipboard;
- secrets/tokens;
- prompt/AI content.

## Autosave

Autosave:

- default: OFF.

Possible later options:

- OFF;
- after delay;
- on focus lost;
- prompt on window close.

Default behavior:

- user controls saving;
- Operre does not silently overwrite user files.

## Dirty/unsaved behavior

Rules:

- dirty tab indicator: `*`;
- close warning;
- choices: Save / Don't Save / Cancel;
- local recovery snapshot may exist for crash recovery.

## Crash recovery

Crash recovery:

- default: ON;
- local-only;
- cloud-disabled;
- user-configurable.

Opening order:

1. If crash recovery exists, show recovery screen.
2. User chooses Recover / Discard / Compare if possible.
3. After recovery decision, normal session restore may run.
4. If no recovery exists, normal startup flow runs.

Crash recovery must never silently overwrite files.

Retention:

- default: 7 days;
- options: 1 day, 7 days, 30 days, manual only.

## Tabs

Tab system:

- multiple tabs supported;
- dirty tab indicator: `*`;
- close tab button;
- reopen closed tab;
- pin tab later;
- tab restore through session restore.

## Split editor

Split editor:

- first version: side-by-side vertical split;
- horizontal split later;
- session restore remembers split layout.

## Minimap

Minimap:

- default: ON;
- position: right.

Settings:

- on/off;
- left/right;
- width small/medium/large;
- adaptive tablet/phone/small-screen behavior.

## Status Bar

Status Bar:

- bottom bar;
- file type;
- encoding;
- BOM yes/no;
- LF/CRLF;
- Spaces/Tabs;
- cursor position: Ln, Col;
- dirty/saved state;
- workspace trust status;
- extension warnings.

## Command Palette

Command Palette shortcut:

- Ctrl+Shift+P

Initial commands:

- New Text File;
- New Markdown Note;
- Open File;
- Open Folder;
- Save;
- Save As;
- Toggle Markdown Preview;
- Toggle Minimap;
- Change Theme;
- Convert Line Endings;
- Convert Indentation;
- Manage Extensions.

## Keyboard shortcuts

Keyboard shortcuts must be configurable.

Defaults:

- Ctrl+N: New File;
- Ctrl+O: Open File;
- Ctrl+S: Save;
- Ctrl+Shift+S: Save As;
- Ctrl+W: Close Tab;
- Ctrl+Shift+T: Reopen Closed Tab;
- Ctrl+F: Find;
- Ctrl+H: Replace;
- Ctrl+Shift+P: Command Palette.

Users can customize through:

- keybindings.json.

macOS should later use platform-native Cmd conventions where appropriate.

## Menu system

Initial classic desktop menu:

- File;
- Edit;
- View;
- Go;
- Tools;
- Extensions;
- Help.

## Activity Bar / Sidebar

Left Activity Bar / Sidebar:

- Explorer;
- Search;
- Recent;
- Extensions;
- Settings.

Later icons appear only through installed/enabled extensions/connectors:

- Git;
- GitHub;
- Ideboard.

## Explorer / folder tree

Explorer first version:

- opened folder/project;
- files and folders;
- create file;
- create folder;
- rename;
- delete with confirmation;
- reveal in file manager;
- refresh.

Security:

- default scope = only user-opened folder/project.

## Delete behavior

Delete behavior baseline:

- default delete moves item to OS Trash/Recycle Bin;
- permanent delete is a separate command;
- every delete operation requires confirmation;
- folder delete requires extra warning.

Detailed permanent delete UI and OS Trash/Recycle Bin implementation remain open for further discussion.

## Search and Recent

Accepted Activity Bar entries include Search and Recent.

Details still open:

- search in current file;
- search in opened folder/project;
- replace in files;
- ignore patterns;
- hidden files;
- binary file handling;
- recent files;
- recent folders;
- recent projects;
- privacy-safe recent history.

## Source 4 UI baseline

The `4.odt` review confirms the initial UI/workbench baseline.

Accepted UI features:

- tabs;
- dirty tab indicator;
- reopen closed tab;
- vertical split editor;
- minimap default ON;
- Status Bar;
- Command Palette;
- configurable keyboard shortcuts;
- classic menu;
- Left Activity Bar / Sidebar;
- Explorer;
- Search;
- Recent;
- Extensions;
- Settings.

Accepted Explorer behavior:

- opened folder/project;
- files and folders;
- create file;
- create folder;
- rename;
- delete with confirmation;
- reveal in file manager;
- refresh;
- scope limited to user-opened folder/project.

Accepted delete baseline:

- Delete moves to OS Trash/Recycle Bin by default.
- Permanent Delete is a separate command.
- Every delete requires confirmation.
- Folder delete requires extra warning.

## Hidden files / dotfiles UI baseline

Accepted UI behavior:

- Explorer hides hidden files and dotfiles by default.
- Explorer provides a Show Hidden Files toggle.
- `.operre/` and `.git/` become visible only when hidden files are shown.
- `.operre/` and `.git/` must display protected metadata indicators when visible.
- Sensitive dotfiles such as `.env` should display warnings before open/preview where practical.
- Protected metadata paths should not look like normal user folders.

## Search and file compare UI baseline

Accepted UI behavior:

- Ctrl+F opens current file search.
- Ctrl+Shift+F opens opened folder/project search.
- Ctrl+H opens replace in current file.
- Replace in files requires preview and confirmation.
- File compare is required.
- Two-file side-by-side compare is required.
- Two-file stacked compare is required.
- Multi-file compare must be supported by design.
- Differences may use red background-color.
- Same/identical content may optionally use green background-color.
- Compare settings must allow detailed user control.
- Compare must provide accessibility-friendly indicators in addition to color where practical.

## Large file UI baseline

Accepted UI behavior:

- Large files show a warning before expensive operations where practical.
- Large File Mode badge/status indicator is required.
- Read-only fallback is visible to the user.
- Feature-limited state must be visible.
- User can choose Open in Large File Mode, Open Read-only, Open normally anyway, or Cancel where practical.
- Settings must expose large file thresholds and behavior.

## Recent files/projects UI baseline

Accepted UI behavior:

- Startup screen shows Continue Last Session, Recent Projects, Recent Files, Pinned, Open File, Open Folder/Project, New Text File, New Markdown Note, and Operre Works.
- File > Open Recent is required.
- Command Palette access to recent items is allowed.
- Missing items are shown as missing without noisy startup errors.
- Recent item actions include Open, Reveal in File Manager, Remove from Recent, Pin/Unpin, Clear Missing Entries, Clear All Recents, Copy Path, and Show Details.
- Clear recent history does not remove pinned items by default.

## Settings UI baseline

Accepted UI behavior:

- Settings UI is required.
- Settings UI must be searchable.
- Settings UI must be category-based.
- Modified settings must be visibly marked.
- Reset to Default is required.
- Restart-required settings must be visibly marked.
- Settings Problems panel is required by design.
- Settings UI must support privacy/security warnings for risky settings.

## Keyboard, touch, and input ergonomics UI baseline

Accepted UI behavior:

- Keyboard shortcuts are required.
- Command Palette, menus, Settings UI, context menus, and keybindings use the same command system.
- Settings UI must support shortcut editing and conflict detection.
- Menus should show shortcut labels where practical.
- On-screen keyboard users must be able to use core workflows efficiently.
- Touchscreen users must not depend on hover-only actions.
- Tablet and phone ergonomics must be supported by design.
- PC touchpads and MacBook trackpads must be comfortable and precise.
- Dangerous shortcut-triggered commands still require confirmation.

## Display, DPI, scaling, and responsive ergonomics UI baseline

Accepted UI behavior:

- UI scale and editor font size are separate concepts.
- Responsive/collapsible layout is required by design.
- Sidebar, panels, split editor, search UI, settings UI, and compare UI must adapt to available screen space.
- Compare view should support side-by-side on wide screens and stacked layout on narrow screens.
- Touch mode and mouse mode may use different spacing and hit targets.
- On-screen keyboard must not cover active editor/input areas where practical.
- High contrast, focus visibility, and non-color indicators must remain compatible with scaling.
- This topic needs a later detailed UI implementation pass.

## Command Palette UI baseline

Accepted UI behavior:

- Command Palette is required.
- Ctrl+Shift+P is the default shortcut.
- Command Palette must support fuzzy command search.
- Command title, category, shortcut, source, and disabled reason should be visible where practical.
- Command Palette must be usable with keyboard, mouse, touch, and on-screen keyboard.
- Command Palette must respect UI scale, high-DPI rendering, and responsive layouts.
- Dangerous commands launched from Command Palette still require confirmation.
- Problems, warnings, and notifications must be reachable through commands when the warning system is defined.

## Error, warning, notification, and Problems UI baseline

Accepted UI behavior:

- Severity levels are required.
- Problems panel is required.
- Settings Problems relationship must be clear.
- Toast, status bar, inline warning, banner, modal, Problems panel, and Settings Problems have distinct roles.
- Critical safety warnings must not be disabled casually.
- Critical safety warnings must not be disabled silently.
- Warning/error behavior must be configurable through Settings where safe.
- Warning UI must be keyboard, touch, high-DPI, high contrast, and on-screen-keyboard compatible.

## Logs and diagnostics export UI baseline

Accepted UI behavior:

- Diagnostics export must be user-initiated.
- Diagnostics export should show preview/summary before creation.
- Export dialogs must be keyboard, touch, high-DPI, and high-contrast compatible.
- Redaction warnings must not rely only on color.
- Open Logs Folder, Clear Logs, and Export Diagnostics must be reachable from Command Palette.
- Diagnostics upload is OFF by default.
- Crash upload is OFF by default.

## Crash recovery and unsaved work UI baseline

Accepted UI behavior:

- Recovery UI/panel is required after crash when recoverable work exists.
- Recovery UI must expose Recover, Compare, Save As, Keep Both, and Discard actions where practical.
- Disk conflict handling must be understandable.
- Destructive recovery actions require confirmation.
- Safe Mode is required by design.
- Recovery UI must be keyboard, touch, high-DPI, high-contrast, and on-screen-keyboard compatible.

## Auto Save and file saving UI baseline

Accepted UI behavior:

- Auto Save is OFF by default.
- Auto Save can be enabled by user preference.
- Save state must be visible where practical.
- Save failed state must preserve dirty buffer and show recovery actions.
- Save conflicts must be understandable and actionable.
- Protected/large/secret-like save warnings must be visible where useful.
- Status bar, Problems panel, editor tabs, and Command Palette should reflect save state where practical.

## Symlink, hardlink, special file, and watcher UI baseline

Accepted UI behavior:

- Symlink badge, broken symlink badge, hardlink warning badge, special file badge, read-only badge, binary badge, sparse badge, external changed badge, deleted-on-disk badge, watcher-limited badge, and protected target warning should exist where useful.
- File Info should expose link path, target path, file identity, hardlink count, type, permissions, and watcher status where safe.
- Dirty buffers must never be silently overwritten by external reload.
- Watcher overflow and watcher limited states must be visible.

## File Explorer, workspace tree, File Info, tabs, and navigation UI baseline

Accepted UI behavior:

- File Explorer tree, workspace root, File Info, tabs, breadcrumbs, and Back/Forward navigation are required by design.
- Tabs must show dirty/read-only/external-changed/deleted/conflict states.
- File Info is a first-class surface for file identity, symlink, hardlink, special-file, watcher, encoding, and protected-path metadata.
- Dangerous Explorer actions require confirmation.
- Large workspace lazy loading and tree virtualization are required by design.
- AI and extensions cannot access Explorer tree or navigation history by default.

## Workbench layout and view management

Operre should use a simple workbench layout model: Activity Bar, primary sidebar, editor area, and bottom panel. The design should keep the useful parts of VS Code's workbench model while reducing complexity, default noise, hidden state, and unclear ownership.

Required UI principles:

- Activity Bar entries map to view containers.
- View containers own views and panels through stable IDs.
- Major view actions use the central command registry.
- Sidebar and panel collapse/resize behavior must be predictable.
- Reset Layout and Restore Default Layout must be available.
- Layout state is machine-local by default.
- Touch, high-DPI, keyboard focus, and narrow layouts must be considered from the start.
- Terminal, Debug, Git, AI, and language runtime surfaces are not v0.1 core surfaces.

## Responsive workbench chrome ergonomics

Operre must not repeat legacy editor failures where toolbar icons and menu text become microscopic on high-DPI monitors. Menus, toolbar buttons, titlebar controls, status bar items, badges, and overflow controls must scale with UI scale and remain usable across desktop, laptop, MacBook, tablet, phone, external display, high-DPI, fractional scaling, and mixed-DPI setups.

The UI must provide compact, comfortable, and touch-oriented density modes. Toolbar and status bar surfaces must overflow gracefully instead of shrinking controls into unreadable or untouchable sizes.

## Operational panel ergonomics

Problems, Search Results, Output, Logs, and Diagnostics panels must remain usable across desktop, high-DPI displays, tablets, phones, MacBooks, external monitors, and mixed-DPI environments. Desktop can use richer tables and channels. Tablet should prefer drawers or stacked views with safe summaries. Phone should prefer cards, full-screen sheets, and restricted summaries.

Panels must avoid microscopic toolbar buttons, clipped filter inputs, hover-only actions on touch, dense desktop tables on phone, and unbounded rendering of large result sets.

## Extension ergonomics and device limits

Extension UI contributions must not damage Operre ergonomics. Extensions cannot make menus, toolbar items, status bar items, panels, views, buttons, icons, or labels microscopic, clipped, overlapping, unreachable, or unusable. Phone and tablet extension support is intentionally limited to safe summaries, themes, syntax, snippets, and lightweight helpers by default.

## Extension permission risk bars

Extension permission warnings must appear below the toolbar and above the editor or working surface. Info bars, warning bars, and critical alert bars must use severity label, icon, readable text, accessible label, keyboard focus support, and status bar fallback. Warning bars must not auto-dismiss. Critical alert bars require acknowledgement before dangerous continuation. Colors are customizable but must not be the only meaning carrier.

## Workspace Trust UI behavior

Workspace Trust warnings can use red critical, yellow warning, and light-blue info bars below the toolbar and above the editor or working surface. Bars must include text, severity label, icon, action buttons, accessibility labels, keyboard focus support, and status bar fallback. Dismissing a bar does not grant trust.

## Terminal UI safety behavior

Terminal UI must show command preview, risk, trust state, log ID,
clickable log path, clickable working directory path, stop action,
kill action, exit code, and output routing. Full terminal mode must
remain guarded and must not look like an uncontrolled shell.

## Per-project Toolchains dashboard

Operre should provide a per-project Toolchains dashboard showing profile
states, missing tools, setup guidance, last run, current status, logs,
diagnostics, outputs, artifacts, risk levels, Resource Governor state,
production guard state, blocked profiles, review-needed profiles, and
safe reset actions.

## Project Dashboard relationship

Project Dashboard is a central project control surface. It should show
overview, files, recent activity, Toolchains, Tasks, Outputs, Logs,
Diagnostics, Problems, Artifacts, Security, Workspace Trust,
Permissions, Production Guard, Resource Usage, and Safe Reset using
readable cards, progressive disclosure, safe actions, and responsive
phone and tablet layouts.

## Diagnostics Dashboard visual relationship

Diagnostics Dashboard should combine health summaries, cards, tables,
detail panels, filters, grouping, lifecycle views, related evidence, and
safe next actions. The UI must remain readable, accessible, responsive,
and useful on desktop, tablet, and phone without exposing restricted
data.

## Marketplace UI relationship

Marketplace UI should show extension name, extension ID, publisher,
verified state, version, install time, last updated time, permission
summary, risk summary, device support, changelog, license, privacy notes,
signature state, source registry, install, update, remove, rollback, and
quarantine actions while remaining simple and accessible.

## Device profile UI relationship

Device profiles are required for desktop, laptop, tablet, phone,
high-DPI monitor, touch-first, keyboard-mouse, low-power, and
remote-view-only experiences. Device profiles affect UI scale, layout,
dashboard density, sidebar behavior, panel behavior, touch mode, command
availability, diagnostics detail level, and safe summary mode.
