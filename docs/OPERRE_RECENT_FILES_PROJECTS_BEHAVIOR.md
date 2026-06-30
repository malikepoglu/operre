# Operre Recent Files and Projects Behavior

## Purpose

This document defines Operre's Recent Files, Recent Projects, Recent Folders, pinned recent items, missing item handling, privacy behavior, and relationship with session restore.

This decision follows the large file memory and cache behavior decision.

## Core principle

Recent history must be useful, local-first, privacy-first, and safe by default.

Recent history must help users reopen their work without exposing sensitive files, protected metadata, AI logs, cache files, secrets, or private project paths to telemetry, diagnostics, AI, extensions, or cloud sync by default.

## Recent history is not session restore

Recent history and session restore are separate concepts.

Recent history means:

- files opened in the past;
- folders/projects opened in the past;
- optional recent comparisons later;
- optional pinned recent items.

Session restore means:

- last open tabs;
- active tab;
- split editor layout;
- cursor positions;
- scroll positions;
- last session UI state.

Rules:

- recent history can exist even if session restore is disabled;
- session restore can exist even if recent history is cleared;
- user settings must treat them separately.

## Recent Files

Recent Files lists normal files opened by the user.

Default behavior:

- most recently opened files appear first;
- file name is shown;
- file path is available;
- last opened time is stored;
- missing files are shown as missing instead of causing noisy errors;
- user can remove a single item from recent history;
- user can clear all recent files;
- protected/sensitive files are excluded by default.

Possible metadata:

- file path;
- display name;
- last opened timestamp;
- last modified timestamp where cheap/safe;
- file type;
- workspace/project relation where available;
- Large File marker where applicable;
- missing flag;
- pinned flag.

## Recent Folders / Projects

Recent Folders and Recent Projects are separate from Recent Files.

Default behavior:

- recently opened folders/projects appear on startup screen;
- recently opened folders/projects appear in Open Recent;
- missing folders/projects are shown as missing;
- user can remove a single recent folder/project;
- user can clear recent folders/projects;
- protected/system folders are not added by default.

Reason:

- a project/folder is not the same as a file;
- project-level reopening should be easy;
- startup screen should prioritize recent projects/folders.

## Pinned recent items

Users can pin important recent items.

Pinned items may include:

- files;
- folders;
- projects;
- comparisons later.

Rules:

- pinned items stay above unpinned recent items;
- clear recent history should not remove pinned items by default;
- removing pinned items requires separate user action;
- clear pinned items requires explicit confirmation.

## Missing recent items

Recent items may become missing if:

- file was deleted;
- folder was deleted;
- drive was disconnected;
- mount is unavailable;
- path moved;
- network path is unavailable later.

Behavior:

- show as missing;
- do not throw noisy startup errors;
- allow Remove from Recent;
- allow Clear Missing Entries;
- allow Reveal in File Manager only if path exists;
- allow retry/open if path returns.

## Startup screen

Startup screen should show:

- Continue Last Session;
- Recent Projects;
- Recent Files;
- Pinned;
- Open File;
- Open Folder / Project;
- New Text File;
- New Markdown Note;
- Operre Works.

Startup screen ordering can be refined later, but Recent Projects and Recent Files must be visible and easy to use.

## Open Recent command

Operre should provide Open Recent behavior.

Possible menu/command locations:

- File > Open Recent;
- Command Palette;
- startup screen;
- Explorer welcome area.

Open Recent sections:

- Pinned;
- Recent Projects/Folders;
- Recent Files;
- Recent Comparisons later.

## Recent Comparisons

File compare sessions may have a separate recent list later.

Recent Comparisons may store:

- left file path;
- right file path;
- optional baseline file path;
- compare layout;
- compare settings snapshot where safe;
- last opened timestamp.

Rules:

- Recent Comparisons must be separate from Recent Files;
- sensitive/protected exclusions apply;
- multi-file compare entries require extra care;
- missing files are shown as missing;
- large files may show Large File marker.

First implementation may skip Recent Comparisons, but architecture should not block it.

## Search history relationship

Search history is separate from Recent Files.

Rules:

- search history must not be mixed into Recent Files;
- search history must be local-only by default;
- sensitive-looking queries should not be stored where practical;
- user can clear search history separately;
- protected paths and sensitive paths must not be stored in search history by default.

## Large file relationship

Large files may be added to Recent Files if the user opens them normally.

Behavior:

- show Large File marker;
- remember that the file was opened in Large File Mode where useful;
- do not store file content;
- do not store chunks;
- do not store search results;
- do not store compare results;
- respect protected/sensitive exclusions.

## Privacy-first default

Recent history is local-only by default.

Recent history must not be:

- uploaded by default;
- included in telemetry by default;
- included in diagnostics by default;
- sent to AI by default;
- exposed to extensions by default;
- synced by default.

## Sensitive/protected exclusions

The following must not be added to recent history by default:

- files inside `.git/`;
- files inside `.operre/audit/`;
- files inside `.operre/secrets/`;
- files inside `.operre/cache/`;
- files inside `.operre/local-state/`;
- files inside `.operre/snapshots/`;
- `.env`;
- `.env.*`;
- `.ssh/`;
- token files;
- secret files;
- credential files;
- private key files;
- obvious cache files;
- obvious generated files;
- obvious log files where practical.

## User override

A future advanced setting may allow sensitive files in recent history.

Default:

- OFF.

If enabled:

- show warning;
- require explicit confirmation;
- never include protected paths automatically;
- still exclude `.operre/secrets/`, private keys, tokens, credentials, and `.git/` internals by default unless a very explicit advanced mode is designed later.

## Storage paths

Recent history is application state, not logs.

Linux suggested paths:

- `~/.local/state/operre/recent/`
- `~/.local/state/operre/recent/recent-files.json`
- `~/.local/state/operre/recent/recent-projects.json`
- `~/.local/state/operre/recent/recent-comparisons.json` later

Settings may live under:

- `~/.config/operre/recent-settings.json`

Windows suggested path:

- `%LOCALAPPDATA%\Operre\recent\`

macOS suggested path:

- `~/Library/Application Support/Operre/recent/`

Do not store recent history under logs by default.

## Retention and limits

User-configurable settings should include:

- max recent files;
- max recent projects;
- max recent comparisons later;
- retention duration;
- clear on exit;
- private mode;
- allow pinned items;
- include large file marker;
- store missing entries on/off;
- clear missing entries command.

Suggested defaults:

- max recent files: 100;
- max recent projects/folders: 50;
- max recent comparisons: 50 later;
- retention: forever unless user changes it;
- clear on exit: OFF;
- private mode: OFF.

## Private mode

Private mode temporarily disables writing new recent history.

Behavior:

- no new recent files;
- no new recent projects;
- no new recent comparisons;
- no search history if tied to private mode later;
- session restore behavior may be controlled separately.

Private mode must not delete existing history unless user explicitly clears it.

## Per-workspace recent

Two levels may exist:

### Global recent

Global recent applies across all Operre.

First implementation may start here.

### Workspace/project local recent

Workspace/project local recent lists files recently opened inside a specific project.

This is useful later for large projects.

First version may defer it, but architecture should not block it.

## UI actions

Recent list item actions:

- Open;
- Reveal in File Manager;
- Remove from Recent;
- Pin;
- Unpin;
- Clear Missing Entries;
- Clear All Recents;
- Copy Path;
- Show Details.

Bulk actions:

- Clear Recent Files;
- Clear Recent Projects;
- Clear Recent Comparisons later;
- Clear Missing Entries;
- Clear All Recent History.

Pinned item actions:

- Unpin;
- Remove from Recent with confirmation;
- Clear Pinned Items with confirmation.

## Missing item UI

Missing item UI should:

- avoid noisy error popups;
- show missing status clearly;
- allow remove;
- allow retry/open if path returns;
- allow clear all missing entries.

## Sync policy

Recent history sync is OFF by default.

Future sync requires:

- explicit user consent;
- sensitive/protected exclusions by default;
- user-owned sync preference where possible;
- clear settings;
- no silent upload.

## Export policy

Recent history export is not first core.

If added later:

- explicit user action;
- exclude sensitive/protected entries by default;
- warn before exporting full paths;
- do not include file contents.

## AI interaction

AI cannot access recent history by default.

AI cannot use recent history as hidden project context.

If AI access is ever allowed:

- explicit scoped permission required;
- sensitive/protected entries excluded;
- action logged;
- user can revoke permission.

## Extension interaction

Extensions cannot access recent history by default.

Extensions require explicit scoped permission for:

- reading recent files;
- reading recent projects;
- adding recent entries;
- contributing recent UI;
- exporting/syncing recent history.

Network sync or external export requires separate network permission.

## Diagnostics and telemetry

Recent history must not be included in diagnostics or telemetry by default.

Diagnostics export may include recent-history metadata only if:

- user explicitly chooses;
- paths are redacted by default;
- sensitive/protected entries excluded.

## First implementation recommendation

Operre v0.1 should include:

- Recent Files;
- Recent Projects/Folders;
- Pinned recent items;
- missing item handling;
- Clear Recent Files;
- Clear Recent Projects;
- Clear Missing Entries;
- local-only recent storage;
- sensitive/protected exclusions;
- Startup screen sections for Recent Projects and Recent Files;
- separation from Session Restore.

Future:

- Recent Comparisons;
- per-workspace recent;
- recent sync;
- recent export.

## Accepted decision summary

Accepted decisions:

- Recent Files is required.
- Recent Projects/Folders is required.
- Pinned recent items are required.
- Startup screen must show Recent Projects and Recent Files.
- Recent history and Session Restore are separate concepts.
- Recent history is local-only by default.
- Sensitive/protected files are excluded by default.
- User can clear recent history.
- Missing files/projects are shown as missing, not noisy errors.
- Search history is separate from Recent Files.
- Recent Comparisons may be added later and must be separate.
- Large files can appear in Recent Files with a Large File marker.
- AI and extensions cannot access recent history by default.
- Sync/export of recent history is OFF by default and requires explicit user consent if added later.

## Settings relationship

Accepted behavior:

- Recent history settings are separate from Session Restore settings.
- Recent history remains local-only by default.
- Private mode can temporarily disable writing new recent history.
- Settings sync must not sync recent history by default.
- Recent history export is not first core and must exclude sensitive/protected entries by default if added later.

## Crash recovery and session restore relationship

Accepted behavior:

- Recovery entries are not the same as Recent Files.
- Recovered files become recent only after user opens or saves them.
- Clearing recent files does not necessarily clear recovery data.
- Session Restore is separate from Recent Files and separate from Crash Recovery.
- Clearing recovery data requires separate confirmation.

## Symlink, hardlink, special file, and watcher recent/session relationship

Accepted behavior:

- Recent files should preserve the user-opened path where useful.
- Symlink target path should not silently replace user-opened path in recent history.
- Missing/deleted recent files should produce clear warning.
- Session restore must handle missing, moved, symlinked, and protected targets cautiously.
