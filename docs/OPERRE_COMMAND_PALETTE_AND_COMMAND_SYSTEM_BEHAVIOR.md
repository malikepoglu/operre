# Operre Command Palette and Command System Behavior

## Purpose

This document defines Operre's Command Palette, command registry, command identifiers, command metadata, search behavior, context handling, security restrictions, extension/AI command rules, touch/display ergonomics, and relationship with error/warning behavior.

This decision follows the display, DPI, scaling, and responsive ergonomics decision.

## Core principle

Command Palette is Operre's central command discovery and execution surface.

Menus, keyboard shortcuts, context menus, toolbar actions, Settings UI, extension commands, AI commands, and Command Palette must use the same command registry model.

Command Palette must not be only for keyboard users. It must also be usable with mouse, touch, tablet, on-screen keyboard, and responsive layouts.

## Command Palette access

Default access:

- Ctrl+Shift+P;
- menu entry;
- Settings UI links where relevant;
- touch/tablet toolbar button where practical;
- Command Palette command itself: `commandPalette.open`.

Rules:

- Command Palette must be discoverable;
- it must be reachable without memorizing a shortcut;
- it must work with keyboard, mouse, and touch;
- it must remain usable when on-screen keyboard is visible.

## Command identifier system

Every important action should have a stable command identifier.

Examples:

- `app.quit`
- `commandPalette.open`
- `file.newTextFile`
- `file.newMarkdownNote`
- `file.openFile`
- `file.openFolder`
- `file.save`
- `file.saveAs`
- `file.closeTab`
- `file.reopenClosedTab`
- `editor.find`
- `editor.replace`
- `search.findInProject`
- `compare.compareSelectedFiles`
- `explorer.showHiddenFiles`
- `settings.open`
- `keyboardShortcuts.open`
- `recent.openRecentFile`
- `recent.clearRecentFiles`
- `problems.open`
- `warnings.open`
- `notifications.openSettings`

Rules:

- command identifiers must be stable once public;
- core command IDs use clear namespaces;
- extension command IDs must be namespaced;
- AI command IDs must be clearly identifiable;
- command IDs may be visible to advanced users.

## Command metadata

Each command should carry metadata.

Required or expected metadata:

- id;
- title;
- category;
- description;
- default shortcut where applicable;
- context / when condition;
- enabled/disabled state;
- disabled reason;
- dangerous/risky flag;
- confirmation requirement;
- source: core/extension/AI/system;
- extension ID where applicable;
- workspace trust requirement;
- permission requirement;
- whether command is available in Command Palette;
- whether command is available in menus;
- whether command is available to keybindings;
- error/warning behavior if command can fail.

## Command categories

Suggested categories:

- App;
- File;
- Edit;
- View;
- Go;
- Explorer;
- Search;
- Replace;
- Compare;
- Recent;
- Settings;
- Keyboard Shortcuts;
- Extensions;
- AI Agents;
- Privacy & Security;
- Problems;
- Warnings;
- Diagnostics;
- Developer / Advanced.

## Search behavior

Command Palette search must support:

- fuzzy search;
- command title search;
- command ID search;
- category search;
- shortcut search;
- recent/frequently used command ranking;
- disabled command display where enabled;
- disabled reason display.

Search must be fast and responsive.

## Basic usage flow

Expected keyboard flow:

- open Command Palette;
- type command text;
- navigate with arrow keys;
- Enter runs command;
- Esc closes palette.

Expected mouse/touch flow:

- open Command Palette through UI;
- tap/click search field;
- select result;
- confirm risky command if needed.

## Context-aware behavior

Command Palette must respect command context.

Examples:

- Save disabled when no file is open;
- Save disabled or changed when file is read-only;
- Search in Project disabled when no workspace/project is open;
- Compare Selected Files disabled unless two files are selected;
- Replace disabled in read-only editor;
- risky extension/AI commands disabled or restricted in untrusted workspace;
- some commands may be limited in Large File Mode.

Disabled commands should explain why they are disabled.

## Dangerous commands

Dangerous commands require confirmation even from Command Palette.

Examples:

- Delete;
- Permanent Delete;
- Replace in Files;
- Clear Recent History;
- Clear Cache;
- Reset Settings;
- Extension uninstall;
- AI workspace permission grant;
- Git destructive actions later;
- shell/terminal commands later.

Rules:

- Command Palette must not bypass confirmation;
- shortcut execution must not bypass confirmation;
- extension commands must not bypass confirmation;
- AI commands must not bypass confirmation;
- confirmation should explain consequences.

## Error and warning relationship

Error, warning, notification, and problem reporting must be a dedicated follow-up topic.

Command Palette must integrate with this future system.

Required design direction:

- commands may fail safely;
- command errors should be visible and understandable;
- warnings should not be silent;
- command failure should not crash Operre;
- risky command warnings should be configurable through Settings;
- warning severity and display style should be configurable where safe;
- users should be able to open Problems / Warnings / Notifications from Command Palette;
- critical safety warnings must not be disabled silently.

Future dedicated specification should define:

- error severity levels;
- warning severity levels;
- notification behavior;
- Problems panel;
- Settings Problems panel relationship;
- toast/banner/dialog/status-bar warning rules;
- per-category warning settings;
- dangerous-action warning settings;
- quiet mode / focus mode limits;
- logging/audit rules for security-relevant warnings.

## Extension commands

Extensions may contribute commands.

Rules:

- extension command IDs must be namespaced;
- extension source must be visible where relevant;
- disabled extension means its commands are unavailable or disabled;
- extension commands cannot bypass permissions;
- extension commands cannot silently gain network, workspace, Git, AI, shell, or credential access;
- extension commands requiring permissions must show permission flow;
- extension commands may appear in Command Palette only when allowed by manifest/trust rules.

Example:

- `extensions.github.openPullRequest`
- `extensions.ideboard.openBoard`

## AI commands

AI commands must be safe by default.

Accepted behavior:

- AI commands default OFF or limited in first core;
- AI workspace access cannot be silently enabled through Command Palette;
- AI commands still require scoped permission;
- AI commands must be audit-logged according to AI audit rules;
- prompt/response logging cannot be silently changed by command;
- AI commands cannot bypass Workspace Trust.

## Recent and frequently used commands

Command Palette may show recent/frequently used commands.

Rules:

- command usage history is local-only by default;
- command usage telemetry is OFF;
- command history is not sent to AI by default;
- command history is not exposed to extensions by default;
- dangerous commands still require confirmation when repeated;
- sensitive command history needs careful handling.

## Touch and tablet ergonomics

Command Palette must be usable with touch.

Required behavior:

- touch-friendly row height where touch mode is active;
- large enough tap targets;
- no hover-only command discovery;
- on-screen keyboard must not cover the input field;
- tablet layout may use a larger command sheet;
- phone layout later may use full-screen command sheet.

## Display, DPI, and responsive behavior

Command Palette must respect display ergonomics.

Required behavior:

- UI scale compatible;
- high-DPI crisp rendering;
- responsive width/height;
- not too large on big monitors;
- not clipped on small screens;
- readable command text at configured font scale;
- safe layout with on-screen keyboard;
- compatible with compact mode.

## Command Palette modes

First version may use one normal command mode.

Architecture should not block future modes:

- command mode;
- file/symbol mode later;
- workspace search mode later;
- help mode later;
- recent commands mode;
- extension commands mode.

## Help and discoverability

Command Palette should help users discover Operre.

It should show where practical:

- command title;
- command category;
- command ID;
- assigned shortcut;
- source;
- disabled reason;
- risky/dangerous marker;
- Settings link for shortcut changes later.

## Security and Workspace Trust

Workspace Trust affects command availability.

Rules:

- untrusted workspace can restrict commands;
- workspace settings cannot silently enable risky commands;
- command execution cannot silently grant permissions;
- shell/network/Git/AI/credential commands need explicit permission;
- dangerous commands still require confirmation;
- extension and AI command execution must respect their own security models.

## Logging and audit

Normal command usage does not need heavy logging.

Security-relevant actions may be audit-logged.

Examples:

- permission changes;
- AI commands;
- extension security actions;
- destructive actions;
- credential/secret access;
- diagnostics export;
- future shell/Git destructive commands.

Command usage telemetry is OFF by default.

## Settings

Settings should include:

- Command Palette shortcut;
- show command IDs on/off;
- show disabled commands on/off;
- show recent commands on/off;
- max recent commands;
- fuzzy search behavior;
- command result density;
- touch-friendly palette mode;
- palette position: centered/top/fullscreen later;
- warning display preferences later;
- dangerous command confirmation preferences where safe;
- notification/error/warning behavior after dedicated warning specification.

Critical safety confirmations must not be disabled casually.

## First implementation recommendation

Operre v0.1 should include:

- Ctrl+Shift+P Command Palette;
- core command registry;
- stable command IDs;
- fuzzy search;
- shortcut display;
- disabled command display;
- disabled reason display;
- context/when integration;
- dangerous command confirmation;
- extension/AI command security compatibility;
- touch/DPI/responsive design hooks;
- Settings integration for basic palette behavior.

First version may defer:

- multiple palette modes;
- command usage ranking polish;
- advanced command history;
- full extension command UI;
- full warning/notification configuration.

## Accepted decision summary

Accepted decisions:

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
- warning/error behavior must be configurable through Settings where safe.

## Error, warning, notification, and Problems relationship

Accepted behavior:

- Command failures must be visible and understandable.
- Command Palette must expose Problems, Warnings, Notifications, Logs, and Diagnostics commands.
- Command Palette must not bypass warning/confirmation policy.
- Dangerous diagnostic export commands require confirmation.
- Disabled command reasons may appear as warnings or Problems where useful.

## Logs and diagnostics command relationship

Accepted behavior:

- Command Palette must expose Open Logs Folder.
- Command Palette must expose Clear Logs.
- Command Palette must expose Export Diagnostics.
- Command Palette must expose Diagnostics Settings.
- Diagnostics export commands require confirmation.
- Clearing logs requires confirmation where destructive.
- Command Palette must not bypass privacy warnings.

## Crash recovery command relationship

Accepted behavior:

- Command Palette should expose recovery.open.
- Command Palette should expose recovery.showRecoveredWork.
- Command Palette should expose recovery.clearRecoveredWork.
- Command Palette should expose recovery.openSafeMode.
- Command Palette should expose session.restorePrevious.
- Command Palette should expose session.clearRestoreState.
- Command Palette must not bypass destructive recovery confirmations.

## Auto Save and file saving command relationship

Accepted behavior:

- Command Palette must expose file.save.
- Command Palette must expose file.saveAs.
- Command Palette should expose file.saveAll.
- Command Palette may expose file.saveCopyAs later.
- Command Palette should expose file.compareWithDisk.
- Command Palette should expose file.showSaveConflict.
- Command Palette must not bypass save conflict, overwrite, or protected path confirmations.

## Symlink, hardlink, special file, and watcher command relationship

Accepted behavior:

- Command Palette should expose file.compareWithDisk.
- Command Palette should expose file.reloadFromDisk.
- Command Palette should expose file.revealSymlinkTarget.
- Command Palette should expose file.showFileInfo.
- Command Palette should expose workspace.rescan.
- Command Palette should expose watcher.restart and watcher.showStatus.
- Command Palette must not bypass dirty conflict handling, protected path policy, or watcher privacy rules.

## File Explorer, workspace tree, File Info, tabs, and navigation command relationship

Accepted behavior:

- Command Palette must expose explorer.focus, explorer.refresh, explorer.rescanWorkspace, and explorer.revealActiveFile.
- Command Palette must expose explorer.toggleHiddenFiles and explorer.openFileInfo.
- Command Palette must expose explorer.copyPath and explorer.copyRelativePath.
- Command Palette must expose explorer.newFile and explorer.newFolder.
- Command Palette must expose file.rename, file.delete, file.revealInOS, file.compareWithDisk, and file.reloadFromDisk.
- Command Palette must expose navigation.back, navigation.forward, tabs.close, tabs.closeOthers, and breadcrumbs.focus.
- Command Palette must not bypass dangerous operation confirmation.

## Workbench chrome command integration

Menus, toolbar actions, titlebar actions, status bar actions, chrome overflow actions, UI scale actions, compact mode actions, and touch mode actions must use the central command registry.

Required workbench chrome command IDs include workbench.action.focusMenuBar, workbench.action.toggleMenuBar, workbench.action.focusToolbar, workbench.action.toggleToolbar, workbench.action.focusStatusBar, workbench.action.toggleStatusBar, workbench.action.increaseUIScale, workbench.action.decreaseUIScale, workbench.action.resetUIScale, workbench.action.enableTouchMode, workbench.action.disableTouchMode, workbench.action.toggleCompactMode, and workbench.action.showChromeOverflow.
