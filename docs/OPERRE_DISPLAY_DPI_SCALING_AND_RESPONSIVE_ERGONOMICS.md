# Operre Display, DPI, Scaling, and Responsive Ergonomics

## Purpose

This document defines how Operre should behave across different screen sizes, resolutions, DPI values, display scales, device classes, multi-monitor setups, touch devices, tablets, phones, and MacBook-style high-DPI environments.

This decision follows the keyboard, keybindings, touch input, and input ergonomics decision.

The topic must be revisited in greater detail when detailed UI implementation, responsive layout implementation, mobile/tablet design, and platform packaging work begins.

## Core principle

Operre must be ergonomic and readable on different screen sizes and display densities.

Operre must not assume only one large desktop monitor.

Operre must support:

- small laptop screens;
- large desktop monitors;
- ultra-wide monitors;
- high-DPI 4K/5K displays;
- fractional scaling;
- multi-monitor setups;
- touch-enabled PCs;
- tablets;
- phones later;
- MacBook screens and trackpads;
- external displays with different DPI values.

The product principle remains:

- same core;
- adaptive ergonomics.

## Ergonomic-first display behavior

Operre does not need to look pixel-identical on every display.

Operre must be:

- readable;
- stable;
- comfortable;
- predictable;
- efficient;
- accessible;
- responsive to available space.

Visual precision is important, but production usability is more important than pixel-perfect sameness.

## UI scale

Operre must provide UI scale control.

Suggested scale options:

- 80%;
- 90%;
- 100%;
- 110%;
- 125%;
- 150%;
- 175%;
- 200%;
- custom.

Rules:

- UI scale must cooperate with system scaling;
- Operre may provide additional app-level UI scale;
- layout must not break at common scale values;
- UI scale must not be confused with editor font size.

## Font scale separation

UI scale and editor font size are separate settings.

Separate controls should exist for:

- app UI font size;
- editor font size;
- Markdown preview font size;
- Explorer/sidebar font size;
- status bar font size;
- terminal font size later;
- compare view font size where practical.

Reason:

- a user may want a larger editor font without enlarging the whole UI;
- a user may want a larger UI while keeping dense editor text;
- high-DPI displays often need independent tuning.

## DPI awareness

Operre must be high-DPI aware.

Required behavior:

- avoid blurry rendering on high-DPI displays;
- support common scaling values such as 100%, 125%, 150%, 175%, and 200%;
- support fractional scaling where the platform allows;
- respect platform DPI behavior on Linux, Windows, and macOS;
- adapt when moved between monitors with different DPI values;
- avoid layout clipping at high scale values.

## Multi-monitor DPI behavior

Operre must handle multi-monitor setups.

Required behavior:

- moving the window between monitors should not break layout;
- UI should adapt to the target monitor scale;
- window restore must not place the window off-screen;
- missing/disconnected monitor state must fall back safely;
- maximized/fullscreen state should be restored separately from raw coordinates;
- window geometry is machine-local state and must not sync by default.

## Responsive layout

Operre must support responsive layout behavior.

Wide screens:

- sidebar can stay open;
- split editor is comfortable;
- compare side-by-side is useful;
- panels can be visible without blocking editor.

Medium screens:

- sidebar may be collapsible;
- panels may auto-collapse;
- split editor still possible;
- compare may remain side-by-side or switch based on width.

Compact screens:

- single-pane default may be better;
- sidebar can hide by default;
- panels should become overlay/collapsible;
- compare stacked layout may be preferred;
- touch targets may become larger.

Very small screens:

- single-pane workflow is preferred;
- bottom/floating action surfaces may be needed later;
- compare may use focused diff or stacked view;
- hover-only actions must not be required.

## Responsive breakpoints

Operre should define ergonomic breakpoints.

Possible conceptual breakpoints:

- compact;
- medium;
- wide;
- ultra-wide.

Breakpoints should not be treated only as fixed pixels.

They should consider:

- effective viewport size;
- DPI scale;
- touch mode;
- OS scaling;
- sidebar visibility;
- panel visibility;
- current workflow;
- editor font size.

## Split editor ergonomics

Split editor behavior should adapt to display conditions.

Rules:

- wide screens can prefer vertical split;
- narrow screens may prefer horizontal/stacked split;
- phones may use single-pane or limited split;
- tablets may use stacked or responsive split;
- user can configure default split direction;
- split state must not make the UI unusable after display changes.

## File compare ergonomics

File compare must adapt to screen size.

Wide screens:

- side-by-side compare is preferred.

Narrow screens:

- stacked compare may be preferred.

Very narrow screens:

- focused diff sections may be needed later;
- changed-section list may be useful;
- side-by-side compare may be too cramped.

Rules:

- compare layout must be configurable;
- compare layout may adapt by screen width;
- red/difference and optional green/same highlights must remain readable at different DPI scales;
- gutters, line numbers, and change markers must scale correctly;
- color must not be the only signal.

## Touch target size

Touch mode must use larger hit targets.

Rules:

- mouse mode and touch mode may use different density;
- touch mode should increase important tap targets;
- minimum touch target size should be configurable later;
- automatic touch detection may exist;
- user override is required;
- destructive touch actions still require confirmation.

## On-screen keyboard interaction

Operre must handle on-screen keyboards.

Required behavior:

- editor caret must not be hidden behind the on-screen keyboard;
- search fields must remain visible when focused;
- Command Palette input must remain visible when focused;
- Settings input fields must remain visible when focused;
- file rename input must remain visible when focused;
- viewport should resize or scroll into view where practical;
- bottom padding / safe area should be applied on tablets/phones where needed.

## Safe area, notch, and rounded corners

Operre must not block future support for safe areas.

Design considerations:

- macOS notch areas;
- mobile safe areas;
- tablet rounded corners;
- OS titlebar / traffic light regions on macOS;
- taskbar/dock overlap;
- fullscreen safe regions.

First desktop implementation may keep this simple, but architecture should not prevent later platform-specific safe area handling.

## Window size and position persistence

Window size and position may be remembered.

Rules:

- window geometry is machine-local;
- window geometry must not sync by default;
- fullscreen/maximized state is stored separately;
- monitor identity may be stored only as local state;
- if a monitor is missing, restore safely to a visible area;
- if DPI changes, recalculate layout safely;
- do not restore unusable off-screen windows.

## Zoom model

Operre must distinguish different zoom concepts.

Separate concepts:

- app UI scale;
- editor font size / editor zoom;
- Markdown preview zoom;
- compare view zoom;
- image/diagram zoom later;
- browser-like app zoom later, if needed.

Suggested behavior:

- if editor has focus, Ctrl+Plus/Ctrl+Minus affects editor zoom or editor font size;
- if Markdown preview has focus, Ctrl+Plus/Ctrl+Minus affects preview zoom;
- if compare view has focus, Ctrl+Plus/Ctrl+Minus affects compare view zoom;
- app-level UI scale is controlled through Settings.

This should be decided in more detail during keybinding/command implementation.

## Accessibility relationship

Display and scaling behavior must support accessibility.

Rules:

- high contrast theme is required by design;
- focus rings must remain visible;
- increasing font size must not break layout;
- important UI must not rely only on color;
- reduced motion should be considered later;
- screen reader compatibility should be considered later;
- touch targets must be large enough in touch mode;
- keyboard navigation must remain usable at high scale.

## High contrast and color

High contrast support must remain compatible with diff/search/status indicators.

Rules:

- red/green compare colors need non-color indicators;
- warnings must include icons/text, not only color;
- focus state must be visible in high contrast;
- disabled state must remain readable;
- themes must be tested at different DPI/scale values.

## Large file relationship

Large file UI may be affected by screen size.

Examples:

- minimap may be useful on wide screens but not on compact screens;
- very large editor font size may reduce usefulness of minimap;
- large file feature warnings must fit on small screens;
- large file compare may default to stacked layout on narrow screens;
- large file search progress UI must be compact but visible.

## Settings required

Display and ergonomics settings should include:

- UI scale;
- app font size;
- editor font size;
- Markdown preview font size;
- sidebar/explorer font size;
- status bar font size;
- touch mode auto/on/off;
- touch target size;
- compact mode;
- sidebar default visibility;
- panel default position;
- split default direction;
- compare default layout;
- compare layout by screen size;
- high-DPI rendering preference where applicable;
- window restore on/off;
- safe window restore;
- remember window position;
- remember window size;
- fullscreen behavior;
- reduced motion later;
- high contrast theme;
- responsive layout mode.

## Storage and sync

Display ergonomics settings split into user settings and machine-local state.

User settings may include:

- UI scale preference;
- font sizes;
- touch mode preference;
- compact mode preference;
- split direction preference;
- compare layout preference;
- accessibility preferences.

Machine-local state includes:

- window position;
- window size;
- current monitor;
- maximized/fullscreen state;
- monitor-specific scale cache;
- local display arrangement.

Machine-local display state must not sync by default.

## Technology direction

Technology decisions must consider:

- high-DPI rendering;
- fractional scaling;
- per-monitor DPI behavior;
- responsive CSS/layout system;
- touch target density;
- safe area variables;
- viewport resize handling;
- on-screen keyboard avoidance;
- platform-specific window restore behavior;
- rendering crispness on Linux, Windows, and macOS.

## Platform notes

Linux:

- fractional scaling can vary by desktop environment;
- Wayland/X11 behavior can differ;
- app should avoid assumptions that only one DPI source exists.

Windows:

- per-monitor DPI awareness is important;
- moving windows between monitors must be handled safely;
- system scaling values are common.

macOS:

- Retina/high-DPI is normal;
- MacBook trackpad ergonomics are important;
- safe area/notch handling may matter on some devices;
- Cmd-based shortcuts and trackpad behavior must feel native.

## Detailed future pass

This topic must be revisited later in greater detail.

Future detailed pass should cover:

- actual breakpoint values;
- exact UI scale defaults;
- exact font defaults;
- minimum touch target sizes;
- compact layout rules;
- tablet layout rules;
- phone layout rules;
- MacBook-specific ergonomics;
- multi-monitor restore algorithms;
- high-DPI testing matrix;
- accessibility testing matrix;
- compare layout responsive thresholds;
- safe area implementation details.

This future pass should happen when detailed UI implementation, platform packaging, responsive layout, and mobile/tablet planning become active.

## First implementation recommendation

Operre v0.1 should include:

- UI scale setting;
- separate editor font size;
- high-DPI-aware rendering;
- safe window restore;
- machine-local window geometry;
- basic responsive layout;
- collapsible sidebar/panels;
- configurable split direction;
- configurable compare layout;
- touch mode design hooks;
- on-screen keyboard avoidance design hooks;
- high contrast design compatibility;
- no sync for machine-local display state.

First version may defer:

- full phone UI;
- full tablet UI;
- exact safe area implementation;
- advanced monitor profiles;
- full gesture customization;
- reduced motion polish.

## Accepted decision summary

Accepted decisions:

- display, DPI, scaling, and responsive ergonomics must have a dedicated specification.
- UI scale and editor font size are separate concepts.
- high-DPI and fractional scaling must be supported by design.
- multi-monitor different-DPI behavior must be considered.
- responsive/collapsible layout is required by design.
- compare view should adapt between side-by-side and stacked layouts.
- touch mode and mouse mode may use different ergonomics.
- on-screen keyboard must not cover active editor/input areas where practical.
- MacBook screens, high-DPI, trackpads, and safe area/notch behavior must be considered.
- window size and position are machine-local state and must not sync by default.
- display/scale/font/touch/window behavior must be configurable.
- accessibility and high contrast must remain compatible with scaling.
- this topic must be revisited later for a deeper detailed UI implementation pass.
- next topic remains detailed Command Palette and command system behavior.
