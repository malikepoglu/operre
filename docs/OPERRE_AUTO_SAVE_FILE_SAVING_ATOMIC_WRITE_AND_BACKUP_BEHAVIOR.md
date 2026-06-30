# Operre Auto Save, File Saving, Atomic Write, and Backup Behavior

## Purpose

This document defines Operre's Auto Save, Manual Save, Save As, file saving, save conflict handling, atomic write, backup behavior, file changed on disk behavior, encoding/line-ending preservation, large/protected file saving, and Settings/Command Palette integration.

This decision follows the crash recovery and unsaved work recovery behavior decision.

## Core principle

User files must not be silently corrupted.

Save failures must not destroy dirty buffers.

Auto Save, Manual Save, Save As, Hot Exit, Crash Recovery, Session Restore, Atomic Write, and Backup are separate concepts.

Auto Save is OFF by default.

Auto Save can be enabled by user preference.

The project owner may not personally use Auto Save, but Operre must still support user-controlled opt-in Auto Save.

Settings and keybindings require atomic write and last-known-good backup behavior.

## Separate save concepts

Operre must separate these concepts:

- Manual Save: user explicitly saves through Ctrl+S, menu, Command Palette, or toolbar.
- Save As: user chooses a new target path.
- Save Copy As: saves a copy without changing the active file path, later.
- Auto Save: automatically saves according to user settings.
- Hot Exit: preserves dirty buffers when closing Operre or a workspace.
- Crash Recovery: restores recoverable work after crash/unexpected shutdown.
- Backup: preserves prior valid versions or snapshots.
- Atomic Write: writes important files through safer temp/flush/rename/backup flow where practical.

These concepts must not be collapsed into one behavior.

## Auto Save default

Accepted behavior:

- Auto Save is OFF by default.
- Auto Save can be enabled by user preference.
- Auto Save must remain separate from Hot Exit and Crash Recovery.
- Auto Save must be clearly visible in Settings.
- Auto Save must not silently overwrite conflicts.
- Auto Save must pause or warn when saving is risky.

Possible Auto Save modes:

- off;
- afterDelay;
- onFocusChange;
- onWindowChange;
- onExplicitIdle later.

Suggested delay:

- user-configurable;
- reasonable default when enabled: 1000-3000 ms.

## Auto Save risk conditions

Auto Save must be careful in risky situations.

Risk conditions include:

- file changed on disk;
- read-only file;
- protected path;
- secret-like file;
- large file;
- binary file;
- network mount;
- removable drive;
- permission denied;
- disk full;
- encoding uncertainty;
- line ending conversion risk;
- symlink/hardlink uncertainty;
- special file;
- unsafe atomic rename condition.

Accepted behavior:

- Auto Save may pause;
- Auto Save may show warning;
- Auto Save may require user confirmation;
- Auto Save must not silently overwrite external changes;
- Auto Save must not silently destroy dirty buffers.

## Manual Save behavior

Manual Save represents explicit user intent.

Rules:

- Manual Save can still require conflict handling.
- Manual Save must not silently overwrite external changes.
- Manual Save failure must preserve dirty buffer.
- Manual Save failure should offer Retry, Save As, Show Details, and Cancel where practical.
- Manual Save should report status clearly.

## Save As behavior

Save As must be safe and clear.

Rules:

- user chooses target path;
- overwrite existing file requires confirmation;
- protected path target may require warning;
- secret-like path may require warning;
- Save As failure must preserve dirty buffer;
- Save As should update active file path only after successful write.

## Save Copy As behavior

Save Copy As may be added later.

Rules:

- saves a copy without changing the active file path;
- overwrite requires confirmation;
- failure must not affect dirty buffer;
- file contents must not be logged.

## Atomic write requirement

Atomic write is mandatory for:

- settings;
- keybindings;
- workspace settings;
- extension settings;
- AI settings;
- recovery metadata;
- session state;
- recent files metadata;
- project metadata.

Atomic write is recommended for user files where safe and practical, but it must not be blindly applied where it changes file semantics or metadata unexpectedly.

## Atomic write method

General atomic write flow:

- create temp file in the same directory where practical;
- write complete content;
- flush/fsync file where practical;
- preserve permissions/metadata where practical;
- atomic rename to target where safe;
- fsync directory where practical;
- keep last-known-good backup where required;
- verify post-write state where practical;
- report failure without losing dirty buffer.

## Atomic write risks

Atomic rename can be risky in some cases.

Risk cases include:

- symlink;
- hardlink;
- special file;
- network mount;
- removable drive;
- permission/ownership mismatch;
- file attributes;
- external file watchers;
- huge files;
- non-local filesystem;
- platform-specific filesystem behavior.

User content files need a cautious strategy. Settings/keybindings still require atomic write semantics and rollback design.

## Backup behavior

Backup behavior must be deliberate.

Backup types:

- settings backup;
- keybindings backup;
- before-save backup;
- crash recovery snapshot;
- manual user backup/export;
- versioned backup later.

Default behavior:

- settings backup is ON by design;
- keybindings backup is ON by design;
- last-known-good backup is required for settings/keybindings;
- normal user file before-save backup is not aggressive by default;
- user file backup should be configurable.

## Backup storage

Config/settings backup may use app state/config backup storage.

User file backups should not create sidecar `.bak` files by default.

Accepted behavior:

- user file backup path should be configurable if enabled;
- sidecar backups must be opt-in;
- backup files must respect hidden/protected/privacy policies;
- backup content is not included in diagnostics export by default;
- backup content is not exposed to AI/extensions by default.

## Save conflict handling

Operre must detect and handle save conflicts.

Conflict examples:

- file changed on disk;
- file deleted;
- path moved;
- read-only changed;
- encoding changed;
- line endings changed;
- permission changed;
- disk full;
- network disconnected;
- removable drive missing;
- symlink target changed;
- external editor modified file.

Available actions should include:

- Compare with disk;
- Overwrite with confirmation;
- Save As;
- Reload from disk, with dirty-buffer-loss confirmation;
- Keep Both;
- Cancel.

External changes must never silently overwrite dirty buffers.

## File changed on disk

Operre should detect external changes.

Accepted behavior:

- if buffer is dirty, show conflict UI;
- if buffer is clean, reload may be automatic or user-configurable;
- external changes must not silently replace dirty buffer;
- file watcher behavior requires a detailed follow-up decision;
- stale file metadata must be handled cautiously.

## Encoding and line endings

Saving should preserve text intent.

Rules:

- preserve existing encoding where practical;
- UTF-8 is the default for new text files;
- unknown encoding should show warning where risk exists;
- preserve existing line endings where practical;
- line ending conversion should be user-controlled or warning-protected;
- encoding conversion risk should be visible before destructive change.

## Large file saving

Large file saving requires caution.

Rules:

- memory usage must be controlled;
- atomic temp copy may be too expensive;
- before-save backup may be too expensive;
- Auto Save may be limited for large files;
- Large File Mode save warnings are required where useful;
- Very Large File Mode may disable Auto Save or backup features;
- save failure must preserve dirty buffer where practical.

## Protected and secret-like file saving

Protected/secret-like files require strict behavior.

Rules:

- Auto Save should be cautious or paused for protected/secret-like files;
- extension/AI access remains denied by default;
- backup/recovery/diagnostics export must not include contents by default;
- path and content privacy must be preserved;
- secret/token exposure warning is required where practical;
- overwrite and backup behavior must be warning-protected.

## Network and removable drives

Network/removable storage can fail differently.

Accepted behavior:

- mount unavailable warning;
- network disconnected warning;
- removable drive missing warning;
- retry action where practical;
- Save As local option where practical;
- atomic rename strategy must be cautious;
- partial save risk must be avoided where practical.

## Permissions and metadata

Saving should preserve metadata where practical.

Metadata may include:

- file permissions;
- executable bit;
- ownership where possible and safe;
- timestamps where appropriate;
- extended attributes later;
- platform-specific attributes later.

Metadata preservation must not override security expectations.

## Symlink, hardlink, and special file caution

Symlink/hardlink/special file behavior needs a detailed follow-up decision.

Accepted interim behavior:

- detect symlink where practical;
- detect special file where practical;
- hardlink risk should be considered;
- warn when save semantics may surprise the user;
- do not blindly replace symlink/hardlink/special file targets;
- detailed behavior is next topic.

## Settings and keybindings special rules

Settings/keybindings have strict requirements.

Rules:

- validate JSON/JSONC before activation;
- invalid write must not corrupt last valid config;
- last-known-good backup is required;
- migration requires backup before modification;
- Settings Problems must report invalid settings/keybindings;
- rollback path is required by design;
- partial writes must not become active settings.

## Save UI states

Operre UI should show save state.

States:

- Saved;
- Saving;
- Dirty;
- Save failed;
- Conflict;
- Read-only;
- Auto Save paused;
- Auto Save enabled;
- Large File Save Limited;
- External Change Detected.

Status bar, Problems panel, editor tab markers, and Command Palette should reflect save state where practical.

## Settings

Settings should include:

- Auto Save mode;
- Auto Save delay;
- Auto Save on focus change;
- Auto Save on window change;
- Auto Save exclude large files;
- Auto Save exclude protected paths;
- confirm overwrite external changes;
- preserve line endings;
- default encoding;
- atomic write for user files: auto/on/off later;
- config backup retention;
- settings/keybindings last-known-good backup;
- before-save backup on/off;
- backup location;
- save conflict behavior;
- show save warnings;
- trim trailing whitespace later;
- final newline later.

Required settings facts:

- Auto Save is OFF by default.
- Auto Save can be enabled by user preference.
- settings and keybindings require atomic write.
- settings and keybindings require last-known-good backup.
- user file backup is not aggressive by default.

## Command Palette relationship

Command Palette should expose saving and backup commands.

Suggested commands:

- `file.save`;
- `file.saveAs`;
- `file.saveAll`;
- `file.saveCopyAs` later;
- `file.revert`;
- `file.compareWithDisk`;
- `file.showSaveConflict`;
- `settings.openSaveSettings`;
- `backups.openFolder`;
- `backups.clearOld`.

Rules:

- Command Palette must not bypass conflict confirmation;
- Command Palette must not bypass overwrite confirmation;
- Command Palette must not bypass protected path warnings.

## Logs and diagnostics relationship

Save failures may be logged.

Rules:

- file contents are not logged;
- dirty buffer contents are not logged;
- backup/recovery content is not logged;
- paths may be redacted in diagnostics export;
- diagnostics export may include save error summaries;
- backup/recovery content is not included in diagnostics export by default.

## AI and extension relationship

AI and extensions must respect save boundaries.

Rules:

- AI cannot silently save user files;
- AI proposed edits require user review according to AI policy;
- extensions cannot bypass save conflict handling;
- extensions cannot bypass protected path save warnings;
- extensions cannot access backup/recovery content by default;
- extension-triggered saves must report errors clearly.

## First implementation recommendation

Operre v0.1 should include:

- Manual Save;
- Save As;
- safe save failure behavior;
- dirty buffer preservation on save failure;
- file changed on disk detection;
- save conflict handling;
- settings/keybindings atomic write;
- settings/keybindings last-known-good backup;
- Auto Save OFF by default;
- Auto Save setting available for user preference;
- Hot Exit and Crash Recovery as separate concepts;
- basic encoding/line-ending preservation;
- large/protected file warning hooks;
- save state indicators;
- Command Palette save commands.

First version may defer:

- Save Copy As;
- advanced before-save backup for normal user files;
- detailed symlink/hardlink/special file handling;
- advanced file watcher policy;
- complete metadata preservation;
- versioned backups;
- cloud backup.

## Accepted decision summary

Accepted decisions:

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
- Detailed symlink, hardlink, special file, and file watcher behavior should be decided next.

## Symlink, hardlink, special file, and watcher save relationship

Accepted behavior:

- Saving through symlink must not silently replace the symlink itself with a regular file.
- Atomic write must not silently break hardlink semantics for user files.
- Special files must not be saved as normal text files by default.
- Auto Save must pause during dirty external-change conflicts.
- Network/removable filesystem uncertainty requires conservative save behavior.
