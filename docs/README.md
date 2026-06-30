# Operre Documentation

This directory contains structured project memory for Operre.

The root `specifications.md` remains the consolidated specification during the planning/specification phase. These documents split the accepted decisions into topic-focused memory files so the project can continue without losing context.

## Documents

- `OPERRE_PRODUCT_PRINCIPLES.md`
- `OPERRE_REPOSITORY_DISCIPLINE.md`
- `OPERRE_TECHNOLOGY_DECISIONS.md`
- `OPERRE_EXTENSION_SECURITY_MODEL.md`
- `OPERRE_AI_AGENT_SECURITY.md`
- `OPERRE_UI_UX_SPECIFICATION.md`
- `OPERRE_STORAGE_PRIVACY_SYNC.md`
- `OPERRE_MARKDOWN_AND_EDITOR_BEHAVIOR.md`
- `OPERRE_FUTURE_FEATURES_AND_RESTRAINTS.md`
- `OPERRE_DECISION_LOG.md`
- `OPERRE_CONVERSATION_IMPORT_AND_SOURCE_PROCESSING.md`
- `OPERRE_FILE_VISIBILITY_AND_PROTECTED_PATHS.md`
- `OPERRE_SEARCH_AND_FILE_COMPARE_BEHAVIOR.md`
- `OPERRE_LARGE_FILE_MEMORY_AND_CACHE_BEHAVIOR.md`
- `OPERRE_RECENT_FILES_PROJECTS_BEHAVIOR.md`
- `OPERRE_SETTINGS_UI_AND_SCHEMA_BEHAVIOR.md`
- `OPERRE_KEYBOARD_KEYBINDINGS_AND_INPUT_ERGONOMICS.md`
- `OPERRE_DISPLAY_DPI_SCALING_AND_RESPONSIVE_ERGONOMICS.md`
- `OPERRE_COMMAND_PALETTE_AND_COMMAND_SYSTEM_BEHAVIOR.md`
- `OPERRE_ERROR_WARNING_NOTIFICATION_AND_PROBLEM_REPORTING_BEHAVIOR.md`
- `OPERRE_LOGS_AND_DIAGNOSTICS_EXPORT_BEHAVIOR.md`
- `OPERRE_CRASH_RECOVERY_AND_UNSAVED_WORK_BEHAVIOR.md`
- `OPERRE_AUTO_SAVE_FILE_SAVING_ATOMIC_WRITE_AND_BACKUP_BEHAVIOR.md`
- `OPERRE_SYMLINK_HARDLINK_SPECIAL_FILE_AND_FILE_WATCHER_BEHAVIOR.md`
- `OPERRE_FILE_EXPLORER_WORKSPACE_TREE_FILE_INFO_TABS_AND_NAVIGATION_BEHAVIOR.md`

## Current phase

Current phase is still specification consolidation.

Implementation must wait until the specification baseline is stable and the first implementation TODO queue is explicitly approved.

## Source reviews

- `source-reviews/OPERRE_SOURCE_REVIEW_1_ODT.md`
- `source-reviews/OPERRE_SOURCE_REVIEW_2_ODT.md`
- `source-reviews/OPERRE_SOURCE_REVIEW_3_ODT.md`
- `source-reviews/OPERRE_SOURCE_REVIEW_4_ODT.md`
- `source-reviews/OPERRE_SOURCE_REVIEW_5_ODT.md`

## Workbench layout and view management

- `OPERRE_PANELS_SIDEBARS_ACTIVITY_BAR_LAYOUT_PERSISTENCE_AND_VIEW_MANAGEMENT_BEHAVIOR.md` - defines Activity Bar entries, sidebars, panels, view containers, layout persistence, view management commands, accessibility, privacy boundaries, extension view restrictions, and the later programming language toolchain/runtime extension track.

## Workbench chrome

- `OPERRE_MENUS_TOOLBAR_TITLEBAR_STATUS_BAR_AND_WORKBENCH_CHROME_BEHAVIOR.md` - defines menus, toolbar, titlebar, status bar, workbench chrome, command integration, high-DPI behavior, tablet/phone/MacBook ergonomics, responsive overflow, accessibility, and safety/privacy indicators.

## Problems, Search Results, Output, Logs, and Diagnostics panels

- `OPERRE_PROBLEMS_SEARCH_RESULTS_OUTPUT_LOGS_AND_DIAGNOSTICS_PANEL_BEHAVIOR.md` - defines structured Problems, Search Results, Output channels, Logs, Diagnostics, Visual Studio-like future diagnostic depth on desktop/workstation platforms, privacy-first redaction, AI/extension access restrictions, and limited phone/tablet panel capabilities.

## Extension contribution points and manifest schema

- `OPERRE_EXTENSION_CONTRIBUTION_POINTS_AND_MANIFEST_SCHEMA.md` - defines Operre's extension classes, TypeScript/JavaScript control-plane direction, manifest schema, contribution points, permission defaults, external toolchain broker direction, local install flow, private registry bootstrap, single-VPS feasibility, profile-aware sync planning, and phone/tablet capability limits.

## Extension permission UI and approval flow

- `OPERRE_EXTENSION_PERMISSION_UI_AND_APPROVAL_FLOW.md` - defines extension permission timing, install summaries, runtime prompts, scoped grants, duration choices, risk bars, status bar persistence, update permission policy, local extension Developer Mode, phone/tablet disabled desktop-required capability display, revocation, Safe Mode, and audit behavior.

## Workspace Trust deep behavior

- `OPERRE_WORKSPACE_TRUST_DEEP_BEHAVIOR.md` - defines scoped, revocable, device-local Workspace Trust; opening bars; runtime prompts; restricted mode; per-root multi-root trust; extension trust relationship; external toolchain and live runtime trust chain; trust review needed; phone/tablet limits; no trust sync; and audit behavior.
