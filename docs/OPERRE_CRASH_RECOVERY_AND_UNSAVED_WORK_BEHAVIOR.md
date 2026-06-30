# Operre Crash Recovery and Unsaved Work Behavior

## Purpose

This document defines Operre's Crash Recovery, Unsaved Work Recovery, Hot Exit, Session Restore, recovery storage, recovery privacy, conflict handling, Safe Mode, atomic write requirements, and recovery relationship with logs, diagnostics, AI, extensions, protected paths, and Settings.

This decision follows the logs and diagnostics export behavior decision.

## Core principle

User-created work should not be lost easily.

Operre must protect unsaved edits after unexpected shutdowns.

Crash Recovery must be privacy-first.

Recovery data is local-only and machine-local by default.

Recovery content is not included in diagnostics export by default.

AI and extensions cannot access recovery content by default.

Crash Recovery, Auto Save, Hot Exit, and Session Restore are separate concepts.

## Separate concepts

Operre must separate these concepts:

- Auto Save: writes changes to the user's target file automatically according to user settings.
- Hot Exit: preserves dirty buffers when the user closes Operre or closes a workspace.
- Crash Recovery: restores recoverable work after unexpected shutdown or crash.
- Session Restore: restores tabs, windows, workspace, split layout, and UI state.
- Atomic Write: writes important files safely using temp/rename/backup behavior where practical.

These concepts must not be treated as one feature.

## Recovery scope

Crash Recovery should protect:

- unsaved editor buffers;
- dirty files;
- untitled documents;
- temporary notes;
- Markdown edits;
- settings edits;
- keybindings edits;
- safe editor session state;
- compare/editor session state where safe;
- search/replace state only where privacy-safe.

Recovery should not silently store sensitive transient input such as passwords.

## Default behavior

Recommended defaults:

- Auto Save is OFF by default or user-configurable.
- Hot Exit is ON by default.
- Crash Recovery is ON by default.
- Session Restore is configurable.
- Recovery UI is shown when recovered work exists.
- Recovery content is local-only.
- Recovery content is not included in diagnostics export by default.

## Recovery storage paths

Recovery data is machine-local state.

Suggested recovery paths:

Linux:

- `~/.local/state/operre/recovery/`

Windows:

- `%LOCALAPPDATA%\Operre\recovery\`

macOS:

- `~/Library/Application Support/Operre/recovery/`

Rules:

- recovery storage does not sync by default;
- recovery storage is not exposed to extensions by default;
- recovery storage is not exposed to AI by default;
- recovery storage is not included in diagnostics export by default.

## Recovery privacy

Recovery data may contain user content.

Rules:

- local-only by default;
- no automatic upload;
- no diagnostics export by default;
- no AI access by default;
- no extension access by default;
- no cloud sync by default;
- protected path content requires extra caution;
- secret-like content requires extra caution;
- recovery metadata may be exported only in redacted/summarized form.

## Recovery UI

After crash or unexpected shutdown, Operre should show a recovery surface.

Possible UI:

- "Recovered Work Available" panel;
- startup recovery dialog;
- Problems panel entry;
- Command Palette command.

Recovery UI should show where safe:

- file name;
- path, redacted if needed;
- last recovery timestamp;
- original file exists yes/no;
- disk file changed yes/no;
- read-only state;
- recovery size;
- workspace/project where relevant.

## Recovery actions

Users should be able to choose:

- Recover;
- Compare with disk version;
- Save As;
- Recover as New File;
- Keep Both;
- Discard;
- Discard All, with strong confirmation;
- Open Containing Folder where safe;
- Show Details.

Discarding recovered content is destructive and requires confirmation.

## Conflict handling

Operre must detect recovery conflicts.

Conflict examples:

- disk file changed after recovery snapshot;
- disk file deleted;
- original path missing;
- permission changed;
- file became read-only;
- recovery content differs from disk content;
- encoding or line ending changed;
- external editor modified the file.

Available actions should include:

- Recover as New File;
- Compare with disk version;
- Replace disk version, with strong confirmation;
- Keep Both;
- Discard recovery;
- Save As.

## Untitled documents

Untitled documents require special care.

Rules:

- untitled documents should be recoverable;
- names may use `Untitled-1`, `Untitled-2`, etc.;
- user can Save As after recovery;
- closing an untitled dirty document should ask whether to save, discard, or preserve recovery;
- crash recovery should not lose untitled content.

## Settings and keybindings recovery

Settings and keybindings must be protected from partial writes.

Required behavior:

- atomic write is required for settings and keybindings;
- invalid partial write must not corrupt the last valid configuration;
- previous valid version should be preserved where practical;
- temporary write files should not become active settings;
- rollback path is required by design;
- Settings Problems should report invalid recovered settings/keybindings;
- user should be able to compare or recover settings edits where practical.

## Atomic write

Atomic write is required for settings and keybindings.

Atomic write should use where practical:

- temp file;
- fsync file;
- fsync directory where practical;
- atomic rename;
- previous valid backup;
- corruption detection;
- rollback to last valid version.

Atomic write should be considered for other important user-facing files where safe and practical.

## Large file recovery

Large file recovery needs special handling.

Risks:

- copying a huge file may be too expensive;
- recovery snapshots may exceed storage limits;
- compare may be too expensive;
- memory/cache pressure may increase;
- large file modes may disable some recovery details.

Accepted behavior:

- Large File Mode recovery warnings are required where useful;
- Very Large File Mode may limit recovery;
- patch/delta recovery may be considered later;
- recovery must respect memory/cache limits;
- user should be warned when recovery is limited.

## Protected and secret-like file recovery

Protected paths and secret-like files require strict boundaries.

Rules:

- recovery content from protected paths is local-only;
- recovery content from protected paths is not included in diagnostics export by default;
- recovery content is hidden from AI and extensions by default;
- recovery UI may show privacy warning;
- path display may be redacted;
- secret-like content should trigger security warning where practical;
- discard confirmation should be careful for protected content.

## Crash loop handling

Operre must handle crash loops.

Safe Mode is required by design.

Crash loop recovery options may include:

- Safe Mode;
- disable extensions for this launch;
- disable AI agents for this launch;
- skip last workspace restore;
- skip last session restore;
- ignore suspicious workspace settings;
- load default settings fallback;
- open recovery panel without restoring risky UI state.

Safe Mode must be reachable from startup flow and Command Palette where practical.

## Session Restore

Session Restore is separate from Crash Recovery.

Session Restore may restore:

- open files;
- active tab;
- workspace/project;
- split layout;
- sidebar/panel state;
- window geometry, machine-local;
- recent session state;
- compare view state where safe.

Session Restore should not restore:

- password fields;
- sensitive transient input;
- raw AI prompts by default;
- raw protected file contents into diagnostics;
- raw search history if sensitive.

## Recovery retention

Recovery retention must be configurable.

Settings may include:

- recovery enabled;
- Hot Exit enabled;
- Session Restore enabled;
- keep recovery days;
- max recovery size;
- clear recovery data;
- clear resolved recovery data;
- show recovery on startup;
- Auto Save mode, separate setting;
- exclude protected files from recovery, advanced/dangerous;
- recovery storage location, advanced later.

## Destructive recovery confirmations

The following require confirmation:

- discard recovered content;
- discard all recovered content;
- overwrite disk file with recovery;
- replace external changes;
- clear all recovery data;
- include recovery data in diagnostics, default no;
- disable Crash Recovery;
- disable Hot Exit;
- disable protected-file recovery.

Risky confirmations should explain consequences clearly.

## Command Palette relationship

Command Palette should expose recovery commands.

Suggested commands:

- `recovery.open`;
- `recovery.showRecoveredWork`;
- `recovery.clearRecoveredWork`;
- `recovery.discardAllRecoveredWork`;
- `recovery.openSafeMode`;
- `session.restorePrevious`;
- `session.clearRestoreState`;
- `settings.openRecoverySettings`.

Rules:

- Command Palette must not bypass destructive confirmations;
- Command Palette must not expose recovery content to AI/extensions;
- recovery commands should explain disabled states.

## Logs and diagnostics relationship

Crash summary can be logged.

Recovery content must not be logged.

Diagnostics export behavior:

- recovery content is not included by default;
- recovery metadata may be included only as redacted/summarized information;
- crash reason summary may be included;
- Safe Mode launch summary may be included;
- recovered file contents are excluded by default;
- protected recovery contents are excluded by default.

## AI relationship

AI must not access recovery content by default.

Rules:

- AI access to recovery content requires explicit scoped permission later;
- AI cannot silently read recovered buffers;
- AI cannot silently inspect untitled recovered documents;
- AI cannot include recovery content in prompts automatically;
- AI recovery summaries must be privacy-controlled;
- AI proposed edits to recovered content require user review.

## Extension relationship

Extensions must not access recovery content by default.

Rules:

- extension access to recovery content requires explicit permission later;
- extensions cannot scan recovery storage;
- extensions cannot export recovery content;
- extensions cannot bypass recovery privacy;
- extension crash reports must not include recovery content by default.

## Workspace Trust relationship

Workspace Trust can restrict recovery behavior.

Rules:

- untrusted workspace may disable risky restore actions;
- workspace settings cannot silently disable Crash Recovery;
- workspace settings cannot silently expose recovery content;
- workspace keybindings cannot bypass recovery confirmations;
- protected path recovery remains restricted regardless of workspace trust.

## Recent files relationship

Recovery is not the same as Recent Files.

Rules:

- recovery entries should not automatically become recent files;
- recovered files may become recent only after user opens/saves them;
- broken recent paths and recovery conflicts should be handled separately;
- clearing recent files does not necessarily clear recovery data;
- clearing recovery data requires separate confirmation.

## Accessibility and ergonomics

Recovery UI must be accessible.

Rules:

- keyboard navigable;
- touch-friendly;
- high-DPI compatible;
- high contrast compatible;
- on-screen keyboard must not hide important inputs where practical;
- warnings must not rely only on color;
- destructive actions must have clear labels;
- screen-reader-friendly messages should be supported later.

## First implementation recommendation

Operre v0.1 should include:

- Crash Recovery ON by default;
- Hot Exit ON by default;
- Session Restore configurable;
- Auto Save separate;
- local-only recovery storage;
- recovery panel/dialog after crash;
- Recover action;
- Save As action;
- Compare with disk version where practical;
- Discard action with confirmation;
- conflict detection for changed/deleted/read-only files;
- untitled document recovery;
- atomic write for settings and keybindings;
- Safe Mode entry;
- recovery content excluded from diagnostics export by default;
- AI/extension access denied by default.

First version may defer:

- advanced delta recovery;
- full large-file patch recovery;
- complete session restore polish;
- advanced recovery storage relocation;
- detailed encrypted recovery storage;
- AI-assisted recovery review;
- extension recovery APIs.

## Accepted decision summary

Accepted decisions:

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
- Detailed Auto Save, file saving, atomic write, and backup behavior should be decided next.

## Auto Save and file saving relationship

Accepted behavior:

- Auto Save remains separate from Crash Recovery.
- Auto Save remains separate from Hot Exit.
- Auto Save is OFF by default.
- Auto Save can be enabled by user preference.
- Save failure must not destroy dirty buffers.
- Settings/keybindings atomic write supports recovery safety.
