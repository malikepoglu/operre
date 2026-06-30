# Operre Panels, Sidebars, Activity Bar, Layout Persistence, and View Management Behavior

Status: Accepted specification
Topic ID: OPR-SPEC-0035
Scope: Panels, sidebars, activity bar, layout persistence, view containers, view management, and workbench navigation.

## 1. Purpose

Operre needs a clear workbench model before implementation begins. This document defines how Activity Bar entries, sidebars, panels, view containers, layout persistence, commands, accessibility, privacy, and extension surfaces should behave.

The goal is not to copy VS Code. VS Code is a useful reference for proven interaction patterns, not a complexity target. Operre should keep the useful parts: stable workbench zones, activity-driven navigation, discoverable commands, keyboard-first flow, predictable view containers, resettable layouts, Problems and Output style surfaces, extension contribution discipline, and responsive sidebars. Operre should improve the experience by using fewer default surfaces, clearer names, stricter privacy, safer extension permissions, machine-local layout state, and less surprising automation.

## 2. Product direction

Operre should feel simple at first launch:

- open a file quickly;
- edit text quickly;
- understand where the user is;
- show only the surfaces that matter;
- keep advanced surfaces discoverable but not noisy;
- avoid turning the first milestone into a full IDE clone.

The long-term design can support powerful extension-driven workflows, but the core must stay small. Compiler, interpreter, simulator, emulator, linker, executable builder, terminal, debugger, language runtime, AI, Git, and cloud integrations must not become core dependencies.

## 3. Workbench hierarchy

The workbench model should follow this hierarchy:

    Activity Bar
      -> View Container
          -> View
          -> Panel
          -> Command IDs
          -> Persisted state
          -> Permission scope
      -> Editor Area

Important rules:

- Activity items must not open random untyped UI.
- Every major view should have a stable view ID.
- Every important user action should have a command ID.
- Extension-contributed views must be permission-scoped.
- AI-contributed or AI-readable views must be explicitly authorized.
- Layout persistence must not become a hidden channel for sensitive user activity.

## 4. Activity Bar

The Activity Bar is the primary workbench navigation surface.

### 4.1 Core Activity Bar entries for v0.1

Required entries:

- Explorer
- Search
- Recent
- Problems
- Extensions
- Settings

Later or optional entries:

- Source Control, as an optional Git extension
- AI, as an optional connector or extension
- Terminal, only after the safe process execution model is specified
- Debug, only after runtime and debugger permissions are specified
- Language Tools, only through extension contribution points

### 4.2 Activity Bar behavior

The Activity Bar should:

- be keyboard focusable;
- expose tooltips and accessible labels;
- use badges for meaningful counts, not decoration;
- avoid color-only state communication;
- support high-DPI icons;
- collapse or adapt in narrow layouts;
- expose commands through the Command Palette;
- preserve the active activity item as machine-local layout state by default.

### 4.3 Useful VS Code patterns to keep

Operre should keep these proven patterns in a simpler form:

- one stable left navigation rail;
- activity entries mapped to view containers;
- command-driven focus and toggle behavior;
- visible problem counts;
- predictable Explorer and Search access;
- simple extension entry point;
- ability to reset a broken layout.

### 4.4 Complexity to avoid

Operre should avoid:

- too many default icons;
- silent extension UI injection;
- unclear view ownership;
- hidden telemetry or usage tracking;
- layout state synced by default;
- AI reading view state or navigation history by default;
- Terminal, Debug, Git, and AI becoming mandatory surfaces.

## 5. Sidebars

### 5.1 Primary sidebar

v0.1 should include a primary sidebar.

Required behavior:

- collapsible;
- resizable;
- keyboard focusable;
- state persisted machine-locally;
- usable with mouse, touchpad, keyboard, and touch;
- protected path indicators respected;
- hidden file visibility kept separate from protected path access.

### 5.2 Secondary sidebar

A secondary sidebar should be future-compatible but not required for v0.1.

Potential future use cases:

- outline;
- preview;
- AI audit view;
- documentation side view;
- secondary search or symbol views;
- extension-contributed auxiliary views.

### 5.3 Sidebar states

The sidebar state machine should distinguish:

- visible;
- collapsed;
- hidden;
- resizing;
- temporarily revealed;
- restored from layout state;
- restricted by Workspace Trust;
- restricted by extension permission policy.

Collapsed and hidden are not the same. Collapsed means the surface is intentionally minimized. Hidden means it should not occupy workbench space.

### 5.4 Sidebar position

Left sidebar should be the default. Right sidebar support can be a later setting, but the model must not make left-only assumptions that prevent future right-side placement.

## 6. Bottom Panel

### 6.1 Purpose

The bottom panel should collect transient, diagnostic, and result-oriented views without polluting the editor area.

### 6.2 v0.1 panel entries

Required or basic entries:

- Problems
- Search Results
- Logs
- Diagnostics
- Settings Problems relationship

Later entries:

- Output
- Extension Problems
- AI Audit
- Terminal
- Debug Console
- Test Results
- Build Results
- Runtime Output

### 6.3 Terminal caution

Terminal must remain later and risky until a safe process execution model is specified.

Terminal support requires:

- Workspace Trust;
- explicit permission;
- command audit logging;
- environment handling;
- secrets protection;
- resource limits;
- process termination rules;
- path redaction;
- extension and AI restrictions;
- user confirmation for dangerous operations.

## 7. View Containers and Views

### 7.1 View container identity

Each view container should have:

- stable ID;
- human-readable title;
- source owner, such as core or extension;
- permission scope;
- default location;
- visibility state;
- command IDs;
- persisted layout state key;
- reset behavior.

### 7.2 View identity

Each view should have:

- stable ID;
- title;
- parent container;
- focus command;
- optional badge;
- optional empty state;
- optional restricted state;
- optional unavailable state;
- clear privacy boundary.

### 7.3 Extension-contributed views

Extension views must not be allowed to appear without a declared contribution point. Extension views must not access Explorer, Search, Recent, Problems, layout state, file contents, logs, diagnostics, or protected paths unless the permission model allows that exact scope.

## 8. Layout Persistence

### 8.1 Default policy

Layout persistence is machine-local by default.

It must not be synced by default. It must not be stored in ordinary workspace settings by default. It must not be included in diagnostics export as full UI history.

### 8.2 Persistable layout state

Allowed machine-local state:

- window size;
- window position;
- active activity item;
- active sidebar container;
- sidebar visible or collapsed state;
- sidebar width;
- active bottom panel;
- bottom panel visible or collapsed state;
- bottom panel height;
- compact mode state when user-controlled;
- touch mode state when user-controlled;
- last selected view inside a container.

### 8.3 State that belongs elsewhere

Layout persistence must not absorb unrelated concerns:

- open editor tabs belong to Session Restore policy;
- dirty buffers belong to Hot Exit and Crash Recovery;
- Recent files and projects belong to Recent policy;
- settings belong to settings files;
- secrets belong to Secret Vault or OS keyring;
- diagnostics belong to logs and diagnostics export policy.

### 8.4 Recovery from bad state

Operre must provide a safe way back from broken layout state:

- reset layout command;
- restore default layout command;
- safe mode behavior;
- ignored invalid layout entries;
- fallback to default if layout state is corrupt;
- no crash on invalid layout state.

## 9. View Management

Required commands:

- workbench.action.focusActivityBar
- workbench.action.focusSideBar
- workbench.action.toggleSideBar
- workbench.action.togglePanel
- workbench.action.focusEditor
- workbench.action.focusProblems
- workbench.action.focusLogs
- workbench.action.focusDiagnostics
- workbench.action.resetLayout
- workbench.action.restoreDefaultLayout
- views.explorer.focus
- views.search.focus
- views.recent.focus
- views.problems.focus
- views.extensions.focus
- views.settings.focus

All commands must use the central command registry. Menus, shortcuts, context menus, Settings UI, extension contributions, and Command Palette must not implement separate private action paths.

## 10. Settings

Recommended settings and state split:

User settings:

- activityBar.visible
- activityBar.showBadges
- sidebar.defaultPosition
- workbench.restoreLayoutOnStartup
- workbench.rememberLastActivity
- workbench.compactMode
- workbench.touchMode
- workbench.reduceAnimations
- workbench.showViewBadges

Machine-local layout state:

- sidebar.width
- sidebar.visibleState
- panel.height
- panel.visibleState
- activeActivity
- activePanel
- activeViewByContainer
- window geometry

Commands, not settings:

- reset layout
- restore default layout
- focus activity bar
- focus sidebar
- toggle panel

## 11. Problems, Logs, Diagnostics, and Search relationship

The panel system must respect already accepted rules:

- Problems must not expose secrets unnecessarily.
- Logs must be local-only by default.
- Diagnostics export must be user-initiated.
- Diagnostics upload must be OFF by default.
- File contents must not be exported automatically.
- AI prompts and responses must not be exported automatically.
- Protected paths must be redacted or excluded by default.
- Search results must respect hidden and protected path policy.

## 12. Accessibility and input ergonomics

The workbench must support:

- keyboard traversal between Activity Bar, sidebar, editor, and panel;
- visible focus indicators;
- screen-reader-friendly labels where practical;
- touch-friendly hit targets;
- high-DPI icons;
- non-color-only badges;
- reduced animation setting;
- on-screen keyboard safety;
- narrow layout adaptation;
- mouse, touchpad, keyboard, and touch input.

## 13. Responsive behavior

Wide layout:

- Activity Bar on the side;
- primary sidebar visible or collapsible;
- editor area central;
- bottom panel optional.

Narrow layout:

- sidebar can become overlay or drawer-like;
- bottom panel can become stacked or tab-like;
- editor must remain reachable;
- active input must not be covered by the on-screen keyboard where practical.

Tablet layout:

- larger hit targets;
- less dense panel controls;
- simpler navigation;
- avoid hover-only interactions.

## 14. Privacy and security

### 14.1 Core rules

- Layout state is local-only by default.
- Full UI history is not kept by default.
- Full layout/navigation history is not exported in diagnostics.
- AI cannot read layout state by default.
- Extensions cannot read layout state by default.
- Extension views require declared contribution points.
- Extension views require permission-scoped access when they expose sensitive data.
- Protected path indicators must not leak to AI or extensions by default.
- Recent history remains governed by Recent policy.
- Explorer and Search remain governed by protected path policy.

### 14.2 AI restrictions

AI must not:

- infer workspace content from visible Explorer state by default;
- read Recent history by default;
- read Problems contents by default;
- read Logs or Diagnostics by default;
- open panels or run commands without permission;
- use Terminal, build, run, debug, Git, or extension actions without scoped permission and audit logging.

## 15. v0.1 scope

v0.1 should include:

- Activity Bar;
- primary sidebar;
- Explorer entry;
- Search entry;
- Recent entry;
- Problems entry;
- Extensions entry as a basic shell;
- Settings entry;
- bottom panel basic;
- Problems panel;
- Logs panel entry;
- Diagnostics panel entry;
- Search Results panel;
- sidebar collapse and resize;
- panel collapse and resize;
- machine-local layout persistence;
- reset layout command;
- restore default layout command;
- keyboard focus commands;
- touch and high-DPI baseline.

v0.1 should not include:

- integrated terminal;
- debugger;
- full Git integration;
- AI panel;
- secondary sidebar;
- full extension marketplace;
- compiler or runtime integrations;
- executable building;
- workspace-wide automation by default.

## 16. Future programming language toolchain and runtime extension track

After the standard and core Operre functions become usable, Operre may support optional programming language toolchain extensions.

Possible extension capabilities:

- compilers;
- interpreters;
- simulators;
- emulators;
- linkers;
- executable builders;
- package builders;
- live runtime surfaces;
- REPL surfaces;
- language servers;
- debuggers;
- build runners;
- test runners;
- benchmark runners;
- problem matchers;
- formatters;
- linters;
- language-specific project templates.

These capabilities must remain extension-driven. They must not become required Operre core dependencies.

Required safety gates:

- Workspace Trust before build, run, debug, or terminal-like execution;
- explicit permission for process execution;
- explicit permission for filesystem writes outside the workspace;
- explicit permission for network access;
- secrets protection by default;
- environment variable filtering;
- command audit logging;
- resource limits;
- timeout handling;
- output size limits;
- protected path restrictions;
- AI cannot use these tools without explicit scoped permission.

## 17. Relationship with later topics

The next workbench specification topic should be:

NEXT_TOPIC: Menus, toolbar, titlebar, status bar, and workbench chrome behavior

Likely later topics:

- Problems, Search Results, Output, Logs, and Diagnostics panel detailed behavior;
- extension contribution points and manifest schema;
- extension permission UI and approval flow;
- Workspace Trust deep behavior;
- safe terminal and process execution model;
- language toolchain and live runtime extension model;
- first implementation milestone freeze.
