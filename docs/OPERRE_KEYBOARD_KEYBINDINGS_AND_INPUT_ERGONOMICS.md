# Operre Keyboard, Keybindings, and Input Ergonomics

## Purpose

This document defines Operre keyboard shortcuts, keybindings, command identifiers, conflict handling, touch input, on-screen keyboards, touchpads, MacBook ergonomics, tablet/phone ergonomics, and accessibility expectations.

This decision follows the Settings UI and settings schema behavior decision.

## Core principle

Operre must be efficient with keyboard, mouse, touchpad, touchscreen, on-screen keyboard, tablet, phone, and MacBook-style trackpad input.

Operre must not assume that the user only uses a physical keyboard and mouse.

Operre must remain ergonomic across:

- Linux desktops;
- Windows desktops;
- macOS desktops and MacBooks;
- touch-enabled PCs;
- tablets;
- phones later;
- devices using on-screen keyboards;
- devices using precision touchpads;
- devices using external keyboards.

## Keyboard-first but not keyboard-only

Keyboard shortcuts are required.

However:

- every important action must also be reachable through UI;
- every important action should be reachable through Command Palette;
- keyboard shortcuts are accelerators, not the only access path;
- touch and on-screen keyboard users must not be blocked.

## Command system baseline

Every important action should have a command identifier.

Examples:

- `file.newTextFile`
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
- `commandPalette.open`
- `keyboardShortcuts.open`

Rules:

- Menu, Command Palette, Settings UI, keybindings, context menus, and extensions should use the same command system.
- Command identifiers must be stable once public.
- Extension command identifiers must be namespaced.
- Dangerous commands must not bypass confirmations through shortcuts.

## Default shortcuts

Operre should start with familiar default shortcuts.

### File shortcuts

Suggested defaults:

- Ctrl+N: New Text File
- Ctrl+O: Open File
- Ctrl+Shift+O: Open Folder / Project
- Ctrl+S: Save
- Ctrl+Shift+S: Save As
- Ctrl+W: Close Tab
- Ctrl+Shift+T: Reopen Closed Tab
- Ctrl+Q: Quit, with careful confirmation where needed on Linux/Windows

### Editor shortcuts

Suggested defaults:

- Ctrl+F: Find in Current File
- Ctrl+H: Replace in Current File
- Ctrl+Shift+F: Search in Folder/Project
- Ctrl+G: Go to Line
- Ctrl+Z: Undo
- Ctrl+Y or Ctrl+Shift+Z: Redo depending on platform convention
- Ctrl+A: Select All
- Ctrl+C: Copy
- Ctrl+X: Cut
- Ctrl+V: Paste
- Ctrl+Slash: Toggle Line Comment where language supports it

### UI shortcuts

Suggested defaults:

- Ctrl+Shift+P: Command Palette
- Ctrl+Comma: Settings
- F11: Fullscreen
- Ctrl+B: Toggle Sidebar, optional
- Ctrl+Shift+E: Focus Explorer, optional

Terminal shortcut note:

- Ctrl+Backtick may be reserved for a future terminal feature.
- If the first core has no terminal, the shortcut can remain unassigned or reserved.

### Tab/navigation shortcuts

Suggested defaults:

- Ctrl+Tab: Next Tab
- Ctrl+Shift+Tab: Previous Tab
- Alt+Left: Back navigation
- Alt+Right: Forward navigation

### Compare shortcuts

File compare should be reachable through:

- Explorer context menu;
- Command Palette;
- Settings-configurable shortcut.

A default compare shortcut is optional because conflicts are likely.

## keybindings.jsonc

Operre must support user-editable keybindings.

User keybindings file:

- `keybindings.jsonc`

JSONC comments are accepted.

Validation is required.

Invalid keybindings must not crash Operre.

Invalid keybindings should appear in Settings Problems.

Example structure as plain text:

[
  {
    "key": "Ctrl+Shift+F",
    "command": "search.findInProject",
    "when": "workspaceOpen"
  },
  {
    "key": "Ctrl+Alt+C",
    "command": "compare.compareSelectedFiles",
    "when": "explorerTwoFilesSelected"
  }
]

## Keybinding storage paths

User keybindings:

Linux:

- `~/.config/operre/keybindings.jsonc`

Windows:

- `%APPDATA%\Operre\config\keybindings.jsonc`

macOS:

- `~/Library/Application Support/Operre/config/keybindings.jsonc`

Workspace shared keybindings:

- `.operre/shared/keybindings.jsonc`

Machine-local keybinding overrides, if needed:

- `~/.local/state/operre/keybindings-local.jsonc`

Machine-local keybindings should not sync by default.

## Settings UI keybinding editor

Settings UI must support shortcut editing.

Required behavior:

- search by command name;
- search by command identifier;
- search by shortcut;
- category filter;
- modified indicator;
- reset one shortcut;
- reset all shortcuts;
- conflict warning;
- invalid shortcut warning;
- platform-specific shortcut display;
- keyboard capture UI for assigning shortcuts.

## Conflict detection

Conflict detection is required.

Rules:

- same shortcut in same context/scope must show conflict;
- user must see conflicting command IDs;
- user can remove old binding;
- user can cancel new binding;
- user may intentionally keep conflict only if the scope/context makes it safe;
- OS-level shortcut conflicts should show a warning;
- shortcuts captured by the OS may show "may not work" warning.

## Context / when system

Keybindings must support context conditions.

Examples:

- `editorFocus`
- `explorerFocus`
- `searchPanelFocus`
- `settingsFocus`
- `markdownPreviewFocus`
- `compareViewFocus`
- `workspaceOpen`
- `fileDirty`
- `filesSelected`
- `explorerTwoFilesSelected`
- `largeFileMode`
- `readOnlyEditor`
- `trustedWorkspace`
- `extensionEnabled`
- `touchMode`
- `onScreenKeyboardVisible`

A shortcut should only run when its context matches.

## Keybinding priority

Baseline priority order:

- Default keybindings
- User keybindings
- Workspace keybindings
- Language-specific keybindings
- Temporary/session override

Security rule:

- workspace keybindings cannot silently enable risky actions;
- Workspace Trust can block or restrict workspace keybindings;
- AI, extension, network, shell, terminal, Git, and credential-related commands need permission/confirmation where appropriate.

## User vs workspace keybindings

User keybindings are global.

Workspace keybindings are project-specific.

Workspace keybindings:

- may be shared through `.operre/shared/keybindings.jsonc`;
- must obey Workspace Trust;
- must not silently trigger risky commands;
- must not silently grant permissions;
- must not bypass confirmation dialogs.

## Platform differences

Operre must support platform-specific bindings.

Baseline:

- Linux/Windows use Ctrl-heavy shortcuts;
- macOS uses Cmd-heavy shortcuts;
- Alt/Option behavior differs by platform;
- OS-reserved shortcuts should not be overridden silently;
- same command may have platform-specific default bindings.

## Keyboard layout handling

Operre must be usable with Turkish, German, English, and other keyboard layouts.

Risks:

- some symbols differ by layout;
- Ctrl+Slash may be difficult on some layouts;
- Ctrl+Backtick may not be convenient on some layouts;
- physical key and logical character can differ.

Accepted behavior:

- shortcut capture UI should record what the user actually presses;
- Settings UI should show the shortcut as the user understands it;
- keybinding model should consider physical key and logical key tradeoffs;
- user must be able to rebind problematic shortcuts.

## Chord shortcuts

Chord shortcuts may be supported later.

Examples:

- Ctrl+K Ctrl+S: Keyboard Shortcuts
- Ctrl+K Ctrl+W: Close All Tabs

First version may start with single-step shortcuts.

Architecture must not block chord shortcuts.

## Disable / unbind

Users must be able to disable a shortcut.

Accepted design direction:

- support explicit disabled bindings;
- avoid ambiguous destructive syntax where possible;
- Settings UI should provide Disable Shortcut.

Possible JSONC model:

[
  {
    "key": "Ctrl+Q",
    "command": "app.quit",
    "disabled": true
  }
]

## Dangerous commands

Dangerous commands must require confirmation even when triggered by shortcut.

Examples:

- Delete
- Permanent Delete
- Replace in Files
- Clear Recent History
- Clear Cache
- Reset Settings
- Extension uninstall
- AI workspace permission grant
- Git destructive actions later
- Shell/terminal commands later

Shortcuts must not bypass confirmations.

## Extension shortcuts

Extensions may contribute shortcuts.

Rules:

- extension shortcuts must be namespaced;
- extensions must not silently override core shortcuts;
- risky extension shortcuts require permission/trust;
- disabled extension means its shortcuts are inactive;
- removing an extension may ask whether to remove its keybindings/settings;
- extension shortcuts cannot bypass extension permission model.

## AI shortcuts

AI shortcuts must be safe by default.

Accepted behavior:

- AI commands should not receive broad default shortcuts in first core;
- AI shortcut execution still requires permission/scoped access;
- AI workspace access cannot be silently enabled by shortcut;
- prompt/response logging cannot be silently changed by shortcut;
- AI shortcuts must respect audit logging.

## On-screen keyboard support

Operre must support devices using on-screen keyboards.

Required behavior:

- editor remains usable when on-screen keyboard is visible;
- cursor/caret should not be hidden behind the on-screen keyboard;
- input fields should scroll or resize into view;
- command UI should remain reachable;
- touch mode should increase important hit targets;
- virtual keyboard appearance should not break layout;
- floating/popup panels should avoid being covered by keyboard where practical;
- on-screen keyboard users must be able to save, search, navigate, and close safely.

Settings may include:

- touch mode auto/on/off;
- on-screen keyboard avoidance on/off;
- larger touch targets on/off;
- compact toolbar on/off;
- bottom toolbar on/off later.

## Touchscreen support

Operre must be usable on touch-enabled screens.

Required behavior:

- tap to focus;
- long press context menu where appropriate;
- touch selection handles where practical;
- scroll with touch;
- pinch zoom where practical;
- drag gestures must not conflict with text selection;
- context actions must not require hover;
- important buttons must have touch-friendly sizes;
- destructive touch actions require confirmation.

Touch must not reduce desktop precision.

## Tablet ergonomics

Tablet ergonomics must be considered by design even if full tablet support comes later.

Required design direction:

- adaptive layout;
- touch-friendly command access;
- optional larger spacing;
- keyboard-aware viewport;
- bottom or floating action surfaces later;
- easy access to Save, Search, Recent, Settings, Command Palette;
- no hover-only critical actions;
- safe handling of split views on smaller screens.

## Phone ergonomics

Phone support may come later, but architecture must not block it.

Design direction:

- same core, adaptive ergonomics;
- single-pane default on small screens;
- responsive editor controls;
- mobile-friendly command access;
- on-screen keyboard awareness;
- safe file picker/open recent flows;
- limited split/compare view on small screens;
- compare may use stacked layout by default on phones.

## Touchpad and trackpad support

Operre must be comfortable with PC precision touchpads and MacBook trackpads.

Required behavior:

- smooth scrolling;
- horizontal scrolling where useful;
- pinch zoom where platform supports it;
- two-finger scroll;
- trackpad-friendly tab/editor navigation;
- avoid accidental destructive gestures;
- support high-DPI displays;
- preserve text selection precision;
- context menu access must be easy.

## MacBook ergonomics

Operre must be efficient on MacBook screens and trackpads.

Design direction:

- macOS Cmd-based shortcuts;
- trackpad-friendly gestures;
- high-DPI rendering;
- safe area/notch awareness where relevant;
- good behavior on smaller laptop screens;
- efficient split editor layouts;
- no dependency on Touch Bar;
- Touch Bar support is optional and not required.

## External keyboard support

External keyboards must work with desktops, laptops, tablets, and phones where platform allows.

Behavior:

- same command/keybinding model;
- platform-specific modifier mapping;
- remappable shortcuts;
- keyboard capture UI;
- layout-aware display.

## Accessibility

Keyboard and input behavior must support accessibility.

Accepted behavior:

- full keyboard navigation target;
- visible focus indicators;
- screen-reader-friendly UI later;
- no color-only feedback;
- shortcut labels visible in menus where practical;
- Command Palette available for actions without shortcuts;
- touch targets large enough in touch mode;
- user can disable problematic shortcuts.

## Import/export

Keybinding import/export may be supported later.

Rules:

- explicit user action;
- validation before import;
- conflict preview before import;
- platform mismatch warnings;
- no secrets;
- no hidden permission grants;
- no bypass of Workspace Trust.

## Profiles / presets

Shortcut presets may come later.

Possible presets:

- Operre Default
- VS Code-like
- Notepad-like simple
- JetBrains-like later
- Vim/Emacs through extension rather than core where practical

First implementation may use Operre Default only.

## Documentation

Operre must document default shortcuts.

Documentation should include:

- shortcut list;
- command IDs for advanced users;
- platform differences;
- how to reset shortcuts;
- how to fix conflicts;
- how to use touch/on-screen keyboard mode.

## First implementation recommendation

Operre v0.1 should include:

- keyboard shortcuts;
- command identifiers;
- Command Palette integration;
- Settings UI shortcut editing;
- `keybindings.jsonc`;
- JSON schema validation;
- conflict detection;
- reset one shortcut;
- reset all shortcuts;
- user keybindings;
- workspace keybindings design;
- Workspace Trust restrictions;
- platform-aware shortcuts;
- touch/on-screen keyboard design hooks;
- basic touch-friendly UI rules;
- dangerous command confirmations.

First implementation may defer:

- full chord shortcut UI;
- import/export;
- shortcut presets;
- advanced gestures;
- full phone/tablet optimized UI;
- Touch Bar support.

## Accepted decision summary

Accepted decisions:

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
- Detailed Command Palette and command system behavior should be decided next.

## Display and input ergonomics relationship

Accepted behavior:

- Keyboard, touch, on-screen keyboard, touchpad, and trackpad ergonomics must account for screen size and DPI.
- Touch mode may use larger hit targets than mouse mode.
- On-screen keyboard visibility must influence viewport/input positioning where practical.
- MacBook trackpad and high-DPI screen ergonomics must be considered together.
- Keyboard shortcut labels must remain readable under UI scaling.

## Command Palette relationship

Accepted behavior:

- Ctrl+Shift+P opens Command Palette by default.
- Command Palette and keybindings use the same command registry.
- Keyboard shortcuts must not bypass command confirmations.
- Command Palette must show shortcut labels where practical.
- Command Palette must remain usable with on-screen keyboards and touch input.
