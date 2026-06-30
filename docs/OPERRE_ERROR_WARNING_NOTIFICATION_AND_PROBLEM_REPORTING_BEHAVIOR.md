# Operre Error, Warning, Notification, and Problem Reporting Behavior

## Purpose

This document defines Operre's error, warning, notification, Problems panel, Settings Problems, severity levels, command failure behavior, configurable warning behavior, local logs, diagnostics privacy, and safety rules.

This decision follows the Command Palette and command system behavior decision.

## Core principle

Operre must communicate clearly without overwhelming the user.

Operre must not fail silently.

Operre must not drown users in repeated warnings.

Critical safety warnings must not be disabled silently.

Critical safety warnings must not be disabled casually.

Warning/error behavior must be configurable through Settings where safe.

## Severity levels

Operre should use explicit severity levels.

Required severity levels:

- Info;
- Success;
- Warning;
- Error;
- Critical;
- Security Warning;
- Blocking Problem.

## Severity meanings

### Info

Informational event.

Examples:

- file opened;
- extension installed;
- settings saved.

Default surface:

- status bar;
- short toast where useful.

### Success

Completed action.

Examples:

- file saved;
- export completed;
- cache cleared.

Default surface:

- short toast;
- status bar message.

### Warning

Something needs attention but work can continue.

Examples:

- hidden paths excluded from search;
- binary file skipped;
- large file limited mode;
- extension disabled by trust.

Default surface:

- toast;
- banner;
- Problems panel entry.

### Error

Operation failed.

Examples:

- save failed;
- permission denied;
- file missing;
- invalid settings JSONC.

Default surface:

- clear error message;
- retry action where practical;
- details link;
- Problems panel entry.

### Critical

Operation cannot continue safely.

Examples:

- data loss risk;
- storage full during save;
- crash recovery overwrite risk.

Default surface:

- modal or blocking dialog where needed;
- clear recovery actions.

### Security Warning

Security-sensitive condition.

Examples:

- secret-like value detected;
- extension permission grant;
- AI workspace access grant;
- protected path access;
- untrusted workspace risk.

Default surface:

- strong warning;
- explicit confirmation;
- audit/log where appropriate.

### Blocking Problem

Problem that blocks a workflow.

Examples:

- workspace cannot open;
- settings file cannot be parsed and fallback is needed;
- extension host failure later.

Default surface:

- modal or Problems panel;
- clear recovery path.

## Display surfaces

Operre should support multiple reporting surfaces.

Required or expected surfaces:

- toast notification;
- status bar message;
- inline editor warning;
- banner / warning bar;
- modal dialog;
- Problems panel;
- Settings Problems panel;
- Extension Problems;
- AI Agent warnings/audit;
- logs;
- diagnostics export.

## Surface selection rules

Not every message deserves the same UI.

Rules:

- transient success can be status bar or toast;
- repeated minor info should not interrupt;
- warning requiring action should use banner or Problems panel;
- failed operation needs visible error and details;
- data loss risk can use modal;
- security-sensitive action needs explicit warning and confirmation;
- blocking problems need clear recovery actions.

## Problems panel

Operre must have a general Problems panel.

Problems panel may include:

- settings errors;
- keybinding conflicts;
- extension errors;
- workspace trust blocked actions;
- search errors;
- compare errors;
- large file warnings;
- file save/load errors;
- broken recent paths;
- diagnostics warnings;
- AI permission problems;
- extension permission problems;
- protected path access problems.

Problems panel behavior:

- filter by severity;
- filter by source;
- show count;
- click to navigate where possible;
- copy problem details;
- clear resolved problems;
- keep unresolved problems visible.

## Settings Problems relationship

Settings Problems can be a dedicated panel or a filtered view inside Problems.

Settings Problems should include:

- invalid JSON/JSONC;
- invalid setting value;
- unknown setting;
- deprecated setting;
- migration warning;
- secret-like value in settings;
- workspace setting blocked by trust;
- extension setting schema error;
- keybinding conflict;
- invalid keybinding;
- restart required warning.

## Notification fatigue prevention

Operre must avoid notification fatigue.

Rules:

- duplicate warnings should be deduplicated;
- repeated warnings should be grouped;
- safe warnings may support Do Not Show Again;
- critical safety warnings must not be disabled silently;
- critical safety warnings must not be disabled casually;
- quiet mode may exist;
- focus mode may exist;
- quiet/focus modes must not hide critical safety warnings;
- security warnings must remain visible enough to prevent unsafe action.

## Configurable warning behavior

Settings must allow detailed warning and notification control where safe.

Configurable settings may include:

- toast duration;
- show info notifications on/off;
- show success notifications on/off;
- show warning banners on/off;
- show disabled command reasons on/off;
- show Problems panel automatically on/off;
- notification sound on/off later;
- quiet mode;
- focus mode;
- warning grouping;
- max visible notifications;
- notification history retention;
- per-category notification preferences;
- per-extension notification preferences;
- per-AI-agent warning preferences;
- dangerous action confirmation preferences where safe.

Non-negotiable rule:

- critical safety warnings must not be disabled casually;
- critical safety warnings must not be disabled silently.

## Warnings that must not be casually disabled

The following warnings must not be casually disabled:

- permanent delete;
- replace in files;
- secret/token exposure;
- extension permission grant;
- AI workspace access grant;
- network access grant;
- shell/terminal command later;
- Git destructive action later;
- diagnostics export containing paths/settings;
- crash recovery overwrite risk;
- untrusted workspace risk;
- protected path access.

## Error details

Users should be able to inspect error details.

Error details may include:

- short human message;
- technical detail expand/collapse;
- error code;
- command ID;
- file path where safe;
- extension ID where applicable;
- AI agent ID where applicable;
- retry action;
- copy details action;
- open logs action;
- export diagnostics action with confirmation.

## Privacy rules

Privacy-first defaults are required.

Rules:

- error reports are not uploaded automatically;
- diagnostics upload is OFF by default;
- file contents are never included automatically;
- secrets must be redacted;
- paths may be redacted in export;
- AI prompts/responses are not included automatically;
- extension telemetry remains denied by default;
- local logs must not store secrets by design.

## Command Palette relationship

Command Palette must expose relevant problem/warning commands.

Examples:

- `problems.open`;
- `warnings.open`;
- `notifications.open`;
- `notifications.clear`;
- `logs.openFolder`;
- `diagnostics.export`;
- `settings.openNotificationSettings`;
- `errors.showLastErrorDetails`.

Rules:

- dangerous diagnostic export still requires confirmation;
- Command Palette must not bypass warning/confirmation policy;
- failed commands should report visible errors.

## Status bar relationship

Status bar can show compact state.

Examples:

- saved;
- dirty;
- read-only;
- large file mode;
- warning count;
- error count;
- workspace trust state;
- extension warning;
- AI warning;
- diagnostics state.

Status bar messages should not replace detailed error handling for serious failures.

## File operation errors

File operation errors must be clear and data-loss-safe.

Examples:

- save failed;
- permission denied;
- file changed on disk;
- encoding problem;
- line ending conversion risk;
- read-only file;
- path missing;
- disk full;
- network/mount unavailable;
- backup/snapshot failed.

Rules:

- avoid silent failure;
- provide retry where practical;
- provide Save As fallback where practical;
- protect unsaved changes;
- avoid overwriting external changes silently.

## Large file warnings

Large file warnings should include:

- Large File Mode warning;
- Very Large File Mode warning;
- feature disabled warning;
- search result limit warning;
- compare limited mode warning;
- memory/cache warning;
- read-only fallback warning.

Large file warnings should be informative, not noisy.

## Search / replace / compare warnings

Search, replace, and compare warnings should include:

- replace in files confirmation;
- too many results;
- hidden/protected paths excluded;
- binary skipped;
- large file skipped/limited;
- compare too expensive;
- word/character diff disabled;
- read-only replace blocked;
- protected path skipped.

Replace in Files remains dangerous and requires strong confirmation.

## Extension warnings

Extension warnings should include:

- permission request;
- extension crash;
- slow extension;
- extension disabled;
- extension blocked by trust;
- extension network attempt blocked;
- extension protected path access blocked;
- extension command failed;
- extension settings invalid.

Extension warnings must respect extension security policy.

## AI warnings

AI warnings should include:

- AI access permission required;
- AI proposed file edits require diff approval;
- AI cannot access protected paths;
- AI cannot read full workspace by default;
- AI prompt/response logging OFF;
- AI provider credential missing;
- AI action logged;
- AI command blocked by trust;
- AI command failed.

AI warnings must respect AI audit and permission rules.

## Workspace Trust warnings

Workspace Trust warnings should include:

- untrusted workspace;
- workspace setting blocked;
- extension disabled by trust;
- AI disabled by trust;
- shell/network/Git command blocked;
- protected path access blocked;
- workspace keybinding blocked;
- workspace command blocked.

Workspace Trust warnings must be understandable and actionable.

## Accessibility

Warning and error UI must be accessible.

Rules:

- do not rely only on color;
- include icons/text/severity labels where practical;
- high contrast compatible;
- keyboard navigable;
- touch-friendly buttons;
- screen-reader-friendly messages later;
- on-screen keyboard must not hide dialogs/inputs where practical;
- focus should move safely to important blocking messages.

## Logs

Local logs may be ON by default if privacy-safe.

Log rules:

- local-only by default;
- no secrets;
- no file contents by default;
- no AI prompt/response by default;
- paths may be redacted in export;
- clear logs command required later;
- open logs folder command allowed;
- diagnostics export requires preview/confirmation.

## Diagnostics export

Diagnostics export must be explicit.

Rules:

- OFF by default for upload;
- user-initiated only;
- preview/summary before export where practical;
- redact secrets;
- exclude file contents by default;
- exclude AI prompt/response by default;
- allow user-reviewed export;
- warn before including paths/settings.

Diagnostics upload remains OFF by default.

## Error codes

Operre may use structured error codes.

Examples:

- `OPR-FILE-SAVE-001`;
- `OPR-SETTINGS-JSON-001`;
- `OPR-EXT-PERM-001`;
- `OPR-AI-SCOPE-001`;
- `OPR-COMPARE-LARGE-001`;
- `OPR-WORKSPACE-TRUST-001`.

First implementation may start simple, but architecture should not block structured error codes.

## Notification history

Notification history may exist.

Rules:

- local-only by default;
- clearable;
- retention configurable;
- sensitive notifications should be handled carefully;
- extension/AI access denied by default;
- no telemetry by default.

## Extension and AI access to warnings

Extensions and AI must not receive full warning/error history by default.

Rules:

- extension access requires permission;
- AI access requires scoped permission;
- protected/sensitive entries remain excluded;
- command/history/warning metadata must not become hidden context by default.

## First implementation recommendation

Operre v0.1 should include:

- severity levels;
- toast/status/banner/modal distinction;
- Problems panel;
- Settings Problems integration;
- configurable safe notification behavior;
- critical warnings not casually disabled;
- command failure visibility;
- file operation error clarity;
- large file warning support;
- search/replace/compare warning support;
- extension/AI/security warning hooks;
- local-only logs;
- diagnostics export OFF/upload OFF by default;
- Error Details expand/collapse;
- Copy Details;
- Command Palette commands for Problems/Warnings/Logs.

First version may defer:

- full notification history polish;
- sound settings;
- advanced per-extension notification profiles;
- advanced per-AI-agent warning profiles;
- complete structured error code catalog;
- detailed diagnostics export UI.

## Accepted decision summary

Accepted decisions:

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
- Detailed logs and diagnostics export behavior should be decided next.

## Logs and diagnostics export relationship

Accepted behavior:

- Logs support error/warning/problem debugging.
- Diagnostics export must remain privacy-first.
- Diagnostics upload is OFF by default.
- Crash upload is OFF by default.
- File contents, secrets, and AI prompts/responses are not included automatically.
- Diagnostics export should include preview/summary and redaction status.

## Crash recovery error/warning relationship

Accepted behavior:

- Crash Recovery should report recoverable work clearly.
- Recovery conflicts should appear as actionable warnings or Problems where useful.
- Discarding recovered content requires confirmation.
- Overwriting disk files with recovered content requires strong confirmation.
- Safe Mode should be offered for crash loops.

## Auto Save and file saving error/warning relationship

Accepted behavior:

- Save failure must preserve dirty buffer.
- Save conflicts should appear as actionable warnings or Problems where useful.
- Auto Save must pause or warn in risky conditions.
- External changes must never silently overwrite dirty buffers.
- Protected/secret-like save warnings must be security-aware.

## Symlink, hardlink, special file, and watcher warning relationship

Accepted behavior:

- Broken symlink warning is required.
- Symlink loop warning is required.
- Hardlink warning is required when link count is greater than 1 where supported.
- Watcher overflow and watcher limited warnings are required.
- Dirty buffer external change conflict must be visible and actionable.
- Special file open/save denial must produce clear errors.

## File Explorer, workspace tree, File Info, tabs, and navigation warning relationship

Accepted behavior:

- Dangerous Explorer actions require confirmation.
- Dirty buffers must never be silently discarded by Explorer, tab, reload, or navigation actions.
- Deleted-on-disk, external changed, watcher limited, watcher overflow, protected target, and special file states must be visible where useful.
- File operation conflicts must be actionable.
- Recursive delete, overwrite, protected path operation, and drag/drop move require warning or confirmation.
