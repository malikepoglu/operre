# Operre Menus, Toolbar, Titlebar, Status Bar, and Workbench Chrome Behavior

Status: Accepted specification
Topic ID: OPR-SPEC-0036
Scope: Menus, toolbar, titlebar, status bar, workbench chrome, responsive ergonomics, DPI behavior, device adaptation, and safe command surfaces.

## 1. Purpose

This document defines Operre's visible workbench chrome: menus, toolbar, titlebar, status bar, and related command surfaces.

The most important rule is simple: Operre must remain usable on different devices, screen sizes, pixel densities, scaling factors, input modes, and operating systems. Menus, toolbar buttons, titlebar items, status bar items, and command surfaces must not become microscopic, clipped, unreachable, overlapping, or unusable on high-DPI desktop monitors, tablets, phones, MacBooks, external displays, or mixed-DPI multi-monitor setups.

A known failure mode is the Notepad++ on a 4K 27-inch monitor problem: the editor area is large, but menu text, toolbar icons, and chrome controls become too small to read or use comfortably. Operre must not repeat that failure mode.

## 2. Product direction

Operre may learn from useful VS Code patterns:

- command-driven menus;
- predictable top-level menu groups;
- status bar awareness;
- file and workspace context in the titlebar;
- keyboard-first navigation;
- command palette access to all important actions;
- extension contribution discipline;
- visible problems and diagnostics summaries.

Operre must improve the experience by being simpler, calmer, safer, and more ergonomic:

- fewer default toolbar buttons;
- fewer default status bar items;
- no mandatory AI, Git, Terminal, Run, Debug, or build chrome in v0.1;
- strong privacy and security indicators;
- responsive chrome across phone, tablet, desktop, laptop, MacBook, and external monitor layouts;
- density-independent sizing instead of hard-coded pixel-only sizing;
- user-controlled UI scale separate from editor font size;
- clear recovery when layout or scaling settings become bad.

## 3. Workbench chrome definition

Workbench chrome includes:

- application menu or menubar;
- toolbar;
- titlebar;
- status bar;
- breadcrumb relationship;
- window controls;
- command palette entry points;
- contextual command surfaces;
- keyboard focus surfaces;
- responsive overflow surfaces;
- compact and touch modes;
- platform-specific safe areas.

Chrome must support mouse, keyboard, touchpad, trackpad, stylus, touch, and on-screen keyboard usage.

## 4. Non-negotiable responsive and DPI rules

### 4.1 No hard-coded pixel-only chrome

Menus, toolbar icons, titlebar controls, status bar items, badges, and separators must not depend only on fixed physical pixels. Operre should use scalable layout units, design tokens, CSS variables, and effective logical pixels where practical.

### 4.2 Separate editor font size from UI scale

Editor font size and UI chrome scale are separate controls.

Required settings:

- editor font size;
- workbench UI scale;
- toolbar density;
- status bar density;
- compact mode;
- touch mode;
- reduce animations.

A user must be able to increase chrome size without making editor text absurdly large, and increase editor text without making toolbar controls enormous.

### 4.3 Effective target size

Interactive chrome controls should have usable hit targets.

Baseline targets:

- pointer-oriented compact target: at least 32 effective CSS px;
- comfortable desktop target: at least 36 effective CSS px;
- touch target: at least 44 effective CSS px;
- phone primary target: at least 48 effective CSS px where practical;
- spacing between touch targets must prevent accidental activation.

Icons may be visually smaller than the hit target, but the clickable area must remain comfortable.

### 4.4 Minimum legibility

Chrome text should not fall below a legible effective size.

Required behavior:

- menu text scales with UI scale;
- toolbar icons scale with UI scale;
- status bar text scales with UI scale;
- high-DPI icons must remain sharp;
- text must not become clipped when scaled;
- badges must not rely on color alone;
- ellipsis must have tooltip or accessible label.

### 4.5 Fractional scaling

Fractional scaling must be considered from the start.

Required cases:

- 100 percent;
- 125 percent;
- 150 percent;
- 175 percent;
- 200 percent;
- mixed-DPI monitors;
- moving a window between monitors with different scale factors.

Chrome must avoid blurry icons, uneven spacing, clipped text, misaligned hit targets, and off-by-one overflow artifacts.

## 5. Device classes

### 5.1 Desktop monitor

Desktop monitor behavior:

- full menubar can be visible;
- toolbar can be visible but minimal;
- status bar can show multiple compact items;
- hover tooltips are allowed but not required for critical meaning;
- keyboard shortcuts should be first-class;
- mouse pointer hit targets can be compact but not tiny.

### 5.2 4K and high-DPI desktop monitor

High-DPI desktop behavior:

- toolbar icons and menu text must scale with UI scale;
- default toolbar must not look like microscopic legacy Win32 chrome;
- status bar must remain readable;
- icon assets must have high-DPI variants or vector rendering;
- UI scale warnings should appear if effective chrome size becomes too small;
- user can increase UI scale from Settings and Command Palette.

The Notepad++ on a 4K 27-inch monitor failure mode is an explicit anti-pattern.

### 5.3 Laptop and MacBook

Laptop and MacBook behavior:

- titlebar must respect platform window controls;
- MacBook notch and safe area must be considered;
- trackpad usage must be comfortable;
- toolbar and status bar must avoid wasting vertical space;
- compact mode should work well;
- native titlebar should be preferred for v0.1 unless custom titlebar accessibility is proven.

### 5.4 Tablet

Tablet behavior:

- touch mode should increase hit targets;
- hover-only controls are not acceptable;
- toolbar should collapse into grouped actions when width is limited;
- status bar can become summarized;
- panels can become drawers or stacked surfaces;
- on-screen keyboard must not cover active editor input where practical;
- long menus should become searchable command lists or grouped sheets.

### 5.5 Phone

Phone behavior is future-facing but must not be blocked by desktop assumptions.

Phone behavior:

- full desktop menubar is not appropriate;
- primary actions should move to a compact command surface;
- toolbar should become bottom or top compact action groups depending on platform;
- status bar should become summarized or hidden behind a details surface;
- titlebar should show short file context;
- breadcrumbs should be collapsed;
- command palette/searchable command sheet becomes more important;
- large dialogs must become full-screen sheets;
- touch targets should be larger than desktop targets;
- no menu item should require pixel-perfect tapping.

### 5.6 External display and multi-monitor

External display behavior:

- layout state is machine-local;
- window position should recover safely if a monitor disappears;
- moving between monitors should re-evaluate effective scale;
- status bar and toolbar must not become tiny or huge after monitor moves;
- titlebar controls must remain reachable.

## 6. Menubar

### 6.1 v0.1 top-level menus

Required menus:

- File;
- Edit;
- Selection;
- View;
- Go;
- Search;
- Extensions;
- Help.

Later menus:

- Run;
- Debug;
- Source Control;
- AI;
- Tools.

Run, Debug, Source Control, AI, and Tools must remain later until the related permission, process execution, runtime, Git, AI, and extension models are specified.

### 6.2 Menu behavior

Menus must:

- be keyboard accessible;
- support mnemonics where platform-appropriate;
- expose shortcuts where available;
- use the central command registry;
- show disabled reasons where practical;
- avoid hidden dangerous actions;
- adapt to narrow layouts;
- become searchable command surfaces on phone or tablet where classic menus are unsuitable.

### 6.3 Menu density

Menu density must adapt:

- desktop compact;
- laptop compact;
- tablet comfortable;
- phone sheet-style;
- high-DPI scaled;
- accessibility enlarged.

Menu text must not clip at larger UI scale.

## 7. Toolbar

### 7.1 v0.1 toolbar actions

Required toolbar actions:

- Open File;
- Open Folder;
- Save;
- Search;
- Toggle Sidebar;
- Toggle Panel;
- Command Palette;
- Settings.

Not in v0.1 toolbar:

- Run;
- Debug;
- Terminal;
- AI;
- Git;
- compiler;
- interpreter;
- emulator;
- simulator;
- linker;
- executable builder.

### 7.2 Toolbar overflow

Toolbar must have overflow behavior:

- hide low-priority actions first;
- move overflow actions to a more menu;
- keep Save and Command Palette reachable;
- keep unsafe or later actions out of v0.1;
- never shrink icons below usable size just to fit more buttons;
- never create a microscopic legacy toolbar.

### 7.3 Toolbar icon scaling

Toolbar icons must:

- scale with UI scale;
- remain sharp on high-DPI displays;
- have accessible labels;
- have tooltips;
- have sufficient hit targets;
- support compact and touch modes;
- not rely on color alone.

## 8. Titlebar

### 8.1 Purpose

The titlebar answers:

- which file is active;
- which workspace is active;
- whether the file is dirty;
- whether the file is read-only;
- whether external changes exist;
- whether a conflict exists;
- whether the workspace is trusted;
- whether Safe Mode is active;
- whether the path is protected or restricted.

### 8.2 Recommended format

Default desktop title pattern:

    file-name - workspace-name - Operre

Dirty state pattern:

    * file-name - workspace-name - Operre

The dirty indicator must not rely on color alone. It needs tooltip and accessible label support.

### 8.3 Native vs custom titlebar

v0.1 should prefer native titlebar behavior where practical.

Reasons:

- platform window controls are safer;
- accessibility is easier;
- drag regions are less error-prone;
- OS integration is more predictable;
- MacBook and Linux desktop environment behavior is less risky.

A custom titlebar may be considered later only after accessibility, window controls, platform safe areas, and hit testing are specified.

## 9. Status bar

### 9.1 Purpose

The status bar gives compact state awareness without becoming a dumping ground.

v0.1 status items:

- file state;
- line and column;
- selection summary, basic or later;
- encoding;
- line endings;
- language mode;
- problems count;
- Workspace Trust;
- protected or restricted state;
- Large File Mode;
- Auto Save state;
- diagnostics/log indicator.

Later status items:

- Git;
- AI;
- cloud sync;
- build status;
- test status;
- runtime status;
- extension toolchain status.

### 9.2 Status bar overflow

The status bar must adapt to limited width:

- show critical security state first;
- show file state before decorative extension state;
- collapse noncritical items into a summary;
- allow user customization;
- expose full details through a command or popover;
- avoid tiny unreadable text;
- avoid horizontal scrolling as the default solution.

### 9.3 Status item contribution rules

Extension status items must:

- declare contribution points;
- declare permissions;
- have stable IDs;
- be user-hideable;
- follow priority limits;
- avoid secret leakage;
- avoid path leakage;
- not track users secretly;
- not bypass Workspace Trust.

## 10. Security and privacy indicators

Workbench chrome must expose security state clearly but calmly.

Required visible states:

- Workspace not trusted;
- protected path;
- restricted file;
- read-only file;
- external change;
- deleted file;
- conflict;
- Safe Mode;
- diagnostics upload OFF;
- telemetry OFF;
- AI no access by default;
- extension restricted.

Security indicators must be understandable without color-only meaning.

AI and extensions must not read full chrome state, layout state, recent history, title history, status history, or navigation history by default.

## 11. Breadcrumb relationship

Titlebar, breadcrumbs, File Info, Explorer, and status bar have different jobs.

- Titlebar: short active file and workspace context.
- Breadcrumbs: current path hierarchy.
- File Info: detailed file identity and metadata.
- Explorer: workspace tree position.
- Status bar: compact operational state.

The same information should not be repeated everywhere. Each surface should have a clear purpose.

## 12. Command IDs

Required command IDs:

- workbench.action.focusMenuBar;
- workbench.action.toggleMenuBar;
- workbench.action.focusToolbar;
- workbench.action.toggleToolbar;
- workbench.action.focusStatusBar;
- workbench.action.toggleStatusBar;
- workbench.action.showAbout;
- workbench.action.openLogs;
- workbench.action.exportDiagnostics;
- workbench.action.openKeyboardShortcuts;
- workbench.action.openSettings;
- workbench.action.showWorkspaceTrust;
- workbench.action.showFileInfo;
- workbench.action.showSecuritySummary;
- workbench.action.increaseUIScale;
- workbench.action.decreaseUIScale;
- workbench.action.resetUIScale;
- workbench.action.enableTouchMode;
- workbench.action.disableTouchMode;
- workbench.action.toggleCompactMode;
- workbench.action.showChromeOverflow;

All menu, toolbar, titlebar, and status bar actions must use the central command registry.

## 13. Settings

Recommended settings:

- window.menuBarVisibility;
- workbench.toolbar.visible;
- workbench.toolbar.compact;
- workbench.toolbar.overflowBehavior;
- workbench.statusBar.visible;
- workbench.statusBar.compact;
- workbench.statusBar.showSecurityIndicators;
- workbench.statusBar.showEncoding;
- workbench.statusBar.showLineEndings;
- workbench.statusBar.showLanguageMode;
- workbench.titleBar.style;
- workbench.uiScale;
- workbench.touchMode;
- workbench.compactMode;
- workbench.reduceAnimations;
- workbench.minTouchTarget;
- workbench.autoDetectHighDPI;
- workbench.warnWhenChromeTooSmall;
- workbench.phoneLayoutMode;
- workbench.tabletLayoutMode;

Settings must be schema-validated. Invalid settings must not break the workbench chrome.

## 14. Responsive layout breakpoints

The exact implementation can evolve, but the specification should require behavior classes:

- tiny phone;
- phone;
- small tablet;
- tablet;
- laptop;
- desktop;
- large desktop;
- high-DPI desktop;
- mixed-DPI multi-monitor.

Responsive behavior must be based on available logical size, effective scale, input mode, and platform, not only raw pixel resolution.

## 15. Acceptance tests for future implementation

Future implementation must test at least:

- 1366 x 768 laptop;
- 1920 x 1080 desktop at 100 percent;
- 2560 x 1440 desktop;
- 3840 x 2160 27-inch high-DPI desktop;
- 3840 x 2160 with 150 percent scaling;
- 3840 x 2160 with 200 percent scaling;
- small tablet portrait;
- small tablet landscape;
- phone portrait;
- phone landscape;
- MacBook-like safe area;
- mixed-DPI external monitor movement;
- on-screen keyboard active;
- UI scale increased;
- compact mode;
- touch mode.

Failure conditions:

- menus are unreadable;
- toolbar icons are microscopic;
- status bar text is clipped;
- buttons are too small to tap;
- titlebar controls overlap;
- window controls are unreachable;
- security indicators disappear;
- command palette cannot be reached;
- keyboard focus gets trapped;
- on-screen keyboard covers the active input;
- overflow hides critical actions.

## 16. v0.1 scope

Included in v0.1:

- menubar;
- minimal toolbar;
- native titlebar preference;
- status bar;
- file and workspace title;
- dirty and read-only indicators;
- line and column;
- encoding and line ending indicators;
- basic language mode;
- problems count;
- Workspace Trust indicator;
- protected/restricted indicator;
- command palette integration;
- UI scale setting;
- compact mode baseline;
- touch mode baseline;
- high-DPI baseline;
- toolbar overflow;
- status bar overflow;
- keyboard accessibility;
- phone and tablet future-compatible rules.

Excluded from v0.1:

- Run menu;
- Debug menu;
- integrated terminal chrome;
- AI toolbar button;
- Git/source-control chrome;
- full extension marketplace chrome;
- full custom titlebar;
- cloud/sync status;
- compiler status;
- runtime status;
- executable builder status.

## 17. Relationship with later topics

Next topic:

NEXT_TOPIC: Problems, search results, output, logs, and diagnostics panel detailed behavior

Likely later topics:

- extension contribution points and manifest schema;
- extension permission UI and approval flow;
- Workspace Trust deep behavior;
- safe terminal and process execution model;
- programming language toolchain and live runtime extension model;
- first implementation milestone freeze.
