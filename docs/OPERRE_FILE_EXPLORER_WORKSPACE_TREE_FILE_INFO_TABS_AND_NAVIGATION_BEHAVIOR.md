# Operre File Explorer, Workspace Tree, File Info, Tabs, and Navigation Behavior

## Purpose

This document defines Operre's File Explorer, workspace tree, File Info/Properties surface, editor tabs, breadcrumbs, navigation history, file operations, tree performance, accessibility, protected path integration, symlink/hardlink/special-file integration, watcher integration, and AI/extension boundaries.

This decision follows the symlink, hardlink, special file, and file watcher behavior decision.

## Core principle

Users must always understand where they are in the filesystem and workspace.

Explorer, tabs, breadcrumbs, recent files, search results, Problems, and Command Palette must share the same file identity model.

File Explorer must respect hidden-file policy, protected path policy, Workspace Trust, symlink/hardlink/special-file policy, and watcher policy.

AI and extensions cannot access the Explorer tree or navigation history by default.

Dangerous Explorer actions require confirmation.

Dirty buffers must never be silently discarded by Explorer, tab, reload, or navigation actions.

## Workspace model

Operre should support multiple opening modes.

Supported model:

- single file;
- single folder/workspace;
- no-folder untitled session;
- recent project/session restore;
- multi-root workspace later.

v0.1 should support single file and single folder/workspace cleanly.

Multi-root workspace is a later feature, but v0.1 design must not block it.

## Workspace root

Workspace root must be explicit.

Required behavior:

- workspace root is visible in Explorer;
- workspace root can be revealed from breadcrumbs or Command Palette;
- workspace root respects Workspace Trust;
- workspace root can be absent in single-file mode;
- workspace root path may be redacted in privacy-sensitive UI/export.

## Workspace Trust relationship

Workspace Trust must be visible where useful.

Rules:

- Explorer can show trust state for workspace root;
- untrusted workspaces may limit risky file operations;
- protected paths remain protected even inside trusted workspace;
- extension/AI access remains permission-scoped;
- Workspace Trust cannot silently override protected path policy.

## Explorer tree baseline

File Explorer tree should support:

- folders;
- files;
- hidden files;
- protected path indicators;
- symlink badges;
- broken symlink badges;
- hardlink warning badges;
- special file badges;
- binary file badges;
- sparse file badges where useful;
- read-only badges;
- dirty indicators;
- external changed indicators;
- deleted-on-disk indicators;
- watcher limited indicators;
- watcher overflow indicators;
- workspace trust indicators.

## Tree node identity

Explorer nodes must not be represented only by display names.

Tree node identity may include:

- opened path;
- relative path;
- canonical path where safe;
- symlink target where relevant;
- device/inode/file ID where supported;
- file type;
- workspace root ID;
- protected classification;
- hidden classification;
- watcher state;
- expanded/collapsed state.

Rules:

- symlink path and target path must not be silently merged;
- duplicate names in different folders must remain distinct;
- deleted/recreated files must be treated carefully if identity changes;
- tree state must tolerate watcher uncertainty.

## Hidden files behavior

Hidden file visibility is separate from protected path access.

Accepted behavior:

- hidden files may be hidden by default;
- hidden files can be toggled from Settings and Command Palette;
- hidden visible state does not grant protected access;
- hidden file search/compare behavior follows search policy;
- hidden file tree entries may still show badges/warnings.

## Protected paths behavior

Protected path policy applies inside Explorer.

Accepted behavior:

- protected paths may be hidden, redacted, or shown with warning depending on setting;
- protected path contents are not scanned unnecessarily;
- protected path tree expansion may require explicit confirmation;
- protected path operations require warning/confirmation;
- AI/extensions cannot read protected tree entries by default;
- raw protected path contents are not included in diagnostics export by default.

## Ignored and excluded paths

Explorer should distinguish hidden, ignored, excluded, and protected states.

Definitions:

- hidden: filesystem/UI visibility concept;
- ignored: project/tool ignore pattern;
- excluded: Operre performance/search/watch exclusion;
- protected: privacy/security-sensitive path.

Rules:

- ignored files may be optionally visible;
- excluded folders may be collapsed or marked;
- protected paths use stricter privacy rules;
- `.git`, `node_modules`, cache/build folders may be excluded from watcher/tree scanning where useful.

## File Info / Properties surface

File Info is a first-class surface.

File Info may show:

- display name;
- opened path;
- relative path;
- canonical path where safe;
- symlink target;
- broken symlink status;
- symlink loop status;
- hardlink count;
- file type;
- size;
- sparse file status where supported;
- binary/text detection;
- encoding;
- line endings;
- modified time;
- created time where available;
- permissions;
- executable bit;
- read-only state;
- owner/group where safe and supported;
- inode/file ID, advanced;
- device ID, advanced;
- filesystem type where practical;
- watcher status;
- workspace trust state;
- protected/secret-like classification;
- large file mode status;
- diagnostics/export redaction status where relevant;
- Git status later.

## File Info privacy

File Info must respect privacy.

Rules:

- advanced identity metadata may be hidden by default;
- protected paths may be redacted;
- canonical path may be hidden/redacted where sensitive;
- File Info must not expose secret file contents;
- File Info must not grant AI/extension access;
- Copy Details action must warn/redact where appropriate.

## Tabs baseline

Tabs represent open editor resources.

Tab indicators should include:

- dirty;
- saved;
- saving;
- save failed;
- read-only;
- external changed;
- deleted on disk;
- conflict;
- protected;
- symlink;
- binary/special file;
- large file mode.

Tabs must be keyboard accessible and touch-friendly.

## Tab identity

Tab identity must not be only a path string.

Accepted behavior:

- opened path is preserved;
- canonical path may be tracked separately;
- symlink target may be tracked separately;
- file identity may be tracked where supported;
- same target opened through different symlink paths must not be silently merged;
- duplicate detection may warn or offer merge, but silent merge is forbidden;
- untitled tabs have stable temporary identity.

## Duplicate open behavior

Opening the same resource twice needs clear policy.

Rules:

- same exact opened path may focus existing tab by default;
- same target through different symlink path may show warning or allow separate tabs;
- same file identity through different casing/path on case-insensitive filesystem must be handled carefully;
- user should not lose unsaved edits through duplicate handling;
- File Info should help explain duplicate/symlink cases.

## Preview tabs

Preview tab behavior is optional and configurable.

Accepted behavior:

- single-click may open preview tab if enabled;
- double-click or edit makes it permanent;
- preview mode can be disabled;
- touch/tablet mode may prefer explicit open;
- preview tabs must not hide dirty state;
- preview tab replacement must not discard dirty buffers.

## Pinned and protected tabs

Pinned tabs may be added later.

Design constraints:

- pinned tabs should survive session restore if enabled;
- protected tabs may require warning before close;
- dirty pinned tabs follow normal dirty confirmation rules;
- pinned state is local/session state unless user chooses otherwise.

## Tab groups and splits

Tab groups and splits are later or advanced behavior.

Design constraints:

- split layout should be restorable where safe;
- tab group operations must not discard dirty buffers;
- navigation history must account for split editor locations;
- large workspaces must not make tab operations slow.

## Breadcrumbs

Breadcrumbs help users understand location.

Accepted behavior:

- breadcrumbs may show workspace-relative path;
- breadcrumbs may show file symbol path later;
- symlink opened path versus target path must be clear where relevant;
- protected path segments may be redacted;
- breadcrumb segments may allow quick folder navigation;
- breadcrumbs must be keyboard accessible.

## Navigation surfaces

Navigation should be consistent across surfaces.

Navigation surfaces include:

- Explorer tree;
- editor tabs;
- breadcrumbs;
- Recent Files;
- Recent Projects;
- Go to File / Quick Open;
- Command Palette;
- Back/Forward navigation;
- File Info;
- Search results;
- Problems panel;
- compare results;
- diagnostics/error details.

## Back and Forward navigation

Back/Forward navigation should be local and privacy-safe.

Navigation entries may include:

- file switches;
- editor cursor locations;
- search result jumps;
- Problems jumps;
- compare jumps;
- breadcrumbs navigation;
- File Info jumps;
- symbol jumps later.

Rules:

- navigation history is local-only;
- navigation history is not exposed to AI/extensions by default;
- protected paths may be redacted where shown;
- navigation must not reopen dangerous/protected targets without policy checks;
- clearing navigation history should be possible later.

## Go to File / Quick Open relationship

Quick Open should integrate with Explorer and file identity.

Rules:

- respects hidden/protected visibility policy;
- respects excluded path policy;
- uses fuzzy search where useful;
- shows badges for symlink/protected/read-only/external changed where useful;
- does not expose protected paths to AI/extensions;
- large workspace indexing can be limited.

## File operations in Explorer

Explorer should support common file operations.

v0.1 candidates:

- New File;
- New Folder;
- Rename;
- Delete / Move to Trash where supported;
- Move;
- Copy;
- Duplicate;
- Reveal in OS File Manager;
- Copy Path;
- Copy Relative Path;
- Copy Name;
- Open File Info;
- Compare with Disk;
- Reload from Disk;
- Open Containing Folder;
- Rescan Workspace.

Later candidates:

- Permanent Delete;
- Open Terminal Here;
- advanced permissions editor;
- Retarget Symlink;
- Create Symlink;
- Create Hardlink.

## Dangerous Explorer actions

Dangerous actions require confirmation or warning.

Dangerous actions include:

- delete;
- permanent delete;
- recursive folder delete;
- overwrite;
- rename conflict;
- move across filesystem;
- move into protected path;
- protected path operation;
- symlink target operation;
- hardlink semantic change;
- special file operation;
- large folder operation;
- drag/drop move;
- operation on dirty open file;
- operation affecting recovery/backup state.

## Delete behavior

Delete behavior must be conservative.

Accepted behavior:

- Move to Trash is preferred where available;
- permanent delete requires stronger confirmation;
- deleting open dirty file must not discard buffer silently;
- deleting folder recursively requires clear confirmation;
- protected path delete requires security warning;
- delete failure must produce actionable error.

## Rename and move behavior

Rename/move must be conflict-aware.

Rules:

- overwrite target requires confirmation;
- moving open dirty file requires careful update or warning;
- symlink/hardlink semantics must be respected;
- watcher uncertainty must trigger rescan/conflict UI;
- moving protected/secret-like files requires warning;
- failure must preserve editor state.

## Drag and drop

Drag/drop is useful but risky.

Accepted behavior:

- drag/drop move can be disabled or confirmation-protected in v0.1;
- drag/drop into protected paths requires warning;
- drag/drop overwrite requires confirmation;
- drag/drop of large folders may require warning;
- drag/drop should be accessible by keyboard alternative;
- accidental touch drag should be prevented where practical.

## Copy and paste behavior

Explorer copy/paste should be explicit.

Rules:

- copy path operations should support full path and relative path;
- copy file/folder operation should check conflicts;
- paste overwrite requires confirmation;
- paste into protected path requires warning;
- copied file contents are not sent to AI/extensions by default;
- clipboard privacy must be considered later.

## Context menu behavior

Context menus must be consistent and not overloaded.

Rules:

- context menu should expose common actions;
- dangerous actions must not be too easy to trigger accidentally;
- protected/special/symlink/hardlink actions require warnings;
- keyboard access must exist;
- touch-friendly alternative must exist;
- extension-contributed menu items require permissions and trust policy.

## Sorting and grouping

Explorer should support predictable sorting.

Settings may include:

- folders first;
- files first later;
- alphabetical;
- modified time;
- file type;
- size;
- natural sort;
- case sensitivity behavior;
- group by type later;
- group by status later.

Sorting must not change file identity.

## Filtering and tree search

Explorer filtering may be added.

Possible filters:

- hidden files;
- ignored files;
- excluded files;
- protected path visibility;
- binary/special files;
- modified/dirty files;
- file type;
- text search in tree later.

Rules:

- filtering is UI-only unless explicitly stated;
- filtering must not grant protected access;
- tree search must respect protected path policy.

## Large workspace performance

Large workspace behavior must be designed from the start.

Required direction:

- lazy loading;
- tree virtualization;
- debounced updates;
- watcher exclude patterns;
- large folder warnings;
- partial watcher mode;
- rescan command;
- progressive rendering;
- avoid blocking UI thread;
- avoid scanning protected paths unnecessarily.

## Watcher integration

Explorer must integrate with file watcher.

Accepted behavior:

- watcher events update tree after debounce;
- internal save events are not shown as external changes;
- watcher overflow triggers warning and rescan;
- watcher limited state is visible;
- network/removable filesystem conservative mode is visible;
- stale tree state should be corrected by rescan.

## External change integration

External file changes must be visible.

Rules:

- clean open file may reload according to settings;
- dirty open file requires conflict UI;
- deleted-on-disk open file remains open until user decides;
- moved/renamed files update only when identity is clear;
- Auto Save pauses during conflicts;
- tabs and Explorer badges should agree.

## File operation queue

File operations should be represented as tasks where useful.

Rules:

- long-running operations should show progress;
- operations can be cancelable where safe;
- recursive operations should show item count where practical;
- failures should report partial results;
- dangerous operation summaries should be shown before execution;
- file operation logs must not include file contents.

## Undo for file operations

Undo for Explorer file operations is desirable but not guaranteed.

Accepted direction:

- simple rename/move undo may be possible later;
- delete undo depends on Trash support;
- permanent delete cannot be casually undone;
- failed partial operations need clear report;
- v0.1 may defer robust file operation undo.

## File operation conflict reporting

Conflicts must be actionable.

Conflict examples:

- target exists;
- permission denied;
- path too long;
- invalid filename;
- file locked;
- read-only;
- cross-device move;
- target protected;
- source disappeared;
- watcher stale state;
- symlink target changed.

Actions may include:

- retry;
- skip;
- replace with confirmation;
- keep both;
- save as;
- cancel;
- show details.

## Accessibility and ergonomics

Explorer and navigation must be accessible.

Rules:

- tree keyboard navigation is required;
- context menu keyboard access is required;
- tabs keyboard navigation is required;
- breadcrumbs keyboard navigation should exist;
- high-DPI icons must be crisp;
- badges must not rely only on color;
- rows must be touch-friendly;
- on-screen keyboard must not hide input/filter fields where practical;
- screen-reader-friendly labels should be supported later.

## Keyboard behavior

Keyboard behavior should be predictable.

Expected shortcuts or commands:

- focus Explorer;
- reveal active file;
- new file;
- new folder;
- rename;
- delete;
- copy path;
- open File Info;
- navigation back;
- navigation forward;
- close tab;
- close others;
- reopen closed tab later;
- toggle hidden files;
- rescan workspace.

Exact shortcuts should be decided in keybinding implementation.

## Command Palette relationship

Command Palette must expose Explorer and navigation commands.

Suggested commands:

- `explorer.focus`;
- `explorer.refresh`;
- `explorer.rescanWorkspace`;
- `explorer.revealActiveFile`;
- `explorer.toggleHiddenFiles`;
- `explorer.openFileInfo`;
- `explorer.copyPath`;
- `explorer.copyRelativePath`;
- `explorer.newFile`;
- `explorer.newFolder`;
- `file.rename`;
- `file.delete`;
- `file.revealInOS`;
- `file.compareWithDisk`;
- `file.reloadFromDisk`;
- `navigation.back`;
- `navigation.forward`;
- `tabs.close`;
- `tabs.closeOthers`;
- `tabs.reopenClosed` later;
- `breadcrumbs.focus`.

Command Palette must not bypass dangerous operation confirmation.

## Settings

Settings should include:

- show hidden files;
- protected path visibility mode;
- explorer row density;
- show file badges;
- show symlink target badge;
- show hardlink warning;
- show file size;
- show modified time;
- sort folders first;
- sort mode;
- single-click preview;
- preview tabs enabled;
- confirm drag and drop;
- confirm recursive delete;
- auto reveal active file;
- follow symlinks in explorer;
- watcher status badges;
- file info advanced metadata;
- breadcrumbs enabled;
- navigation history enabled;
- large workspace lazy loading;
- explorer excludes;
- tree search enabled later.

## AI boundaries

AI must not receive Explorer tree access by default.

Rules:

- AI cannot read Explorer tree by default;
- AI cannot read navigation history by default;
- AI cannot read protected paths by default;
- AI workspace tree summary requires explicit scoped permission later;
- AI cannot use hidden watcher/tree state as hidden prompt context;
- AI suggestions for file operations require user confirmation.

## Extension boundaries

Extensions must not receive Explorer tree access by default.

Rules:

- extension Explorer contributions require permission and Workspace Trust;
- extension tree providers may be added later;
- extension context menu items require permission;
- protected paths are excluded by default;
- extension cannot access navigation history by default;
- extension cannot bypass file operation confirmations;
- extension cannot silently run dangerous Explorer operations.

## Logs and diagnostics relationship

Explorer/navigation diagnostics must remain privacy-first.

Rules:

- file operation failures may be logged;
- file contents are not logged;
- protected raw paths may be redacted;
- navigation history is not exported by default;
- Explorer tree snapshot is not exported by default;
- diagnostics may include watcher limited/overflow summaries;
- diagnostics may include UI state summaries where safe.

## Recent files and session relationship

Explorer, tabs, and navigation interact with recent/session state.

Rules:

- opening a file may update Recent Files;
- preview-only open may not update Recent Files until made permanent;
- recovered files become recent only after user opens or saves them;
- symlink opened path should be preserved in recent history where useful;
- session restore must re-check protected/missing/moved/symlink targets;
- navigation history is separate from recent files.

## First implementation recommendation

Operre v0.1 should include:

- basic File Explorer tree;
- explicit workspace root;
- single file mode;
- single folder/workspace mode;
- hidden files toggle;
- protected path policy integration;
- symlink/hardlink/special/read-only/binary/external-change badges where practical;
- File Info basic panel;
- tabs with dirty/read-only/external-changed/deleted-on-disk indicators;
- tab identity based on opened path plus file identity metadata where practical;
- reveal active file;
- New File/New Folder/Rename/Delete basic flows;
- Copy Path and Copy Relative Path;
- Reveal in OS File Manager;
- watcher refresh/rescan integration;
- dirty buffer conflict UI integration;
- breadcrumbs basic;
- Back/Forward navigation basic;
- Command Palette integration;
- lazy loading and tree virtualization design;
- AI/extension Explorer tree access denied by default;
- accessibility/touch/high-DPI baseline.

First version may defer:

- multi-root workspace;
- advanced tree search;
- extension tree providers;
- full file operation undo;
- advanced drag/drop;
- advanced File Info metadata viewer;
- pinned tabs;
- tab groups;
- advanced breadcrumbs symbol path;
- complete Git status integration.

## Accepted decision summary

Accepted decisions:

- File Explorer, workspace tree, File Info, tabs, and navigation behavior must have a dedicated specification.
- Users must always understand where they are in the filesystem and workspace.
- Explorer, tabs, breadcrumbs, recent files, search results, Problems, and Command Palette must share the same file identity model.
- v0.1 supports single file and single folder/workspace; multi-root workspace remains a future-compatible design target.
- Workspace root must be explicit.
- Hidden file visibility is separate from protected path access.
- Protected path policy applies inside Explorer.
- File Info is a first-class surface.
- Tabs must show dirty/read-only/external-changed/deleted/conflict states.
- Tab identity must not be only a path string.
- Same target opened through different symlink paths must not be silently merged.
- Dirty buffers must never be silently discarded by Explorer, tab, reload, or navigation actions.
- Dangerous Explorer actions require confirmation.
- Large workspace lazy loading and tree virtualization are required by design.
- Watcher events must update Explorer through debounce/rescan behavior.
- AI and extensions cannot access Explorer tree or navigation history by default.
- Detailed panels, sidebars, activity bar, layout persistence, and view management behavior should be decided next.
