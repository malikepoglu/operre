# Operre Symlink, Hardlink, Special File, and File Watcher Behavior

## Purpose

This document defines Operre's behavior for symbolic links, hard links, special files, file identity, path canonicalization, save semantics, file watchers, external changes, watcher limits, race conditions, network/removable filesystems, protected paths, AI/extension watcher boundaries, and related Settings/Command Palette integration.

This decision follows the Auto Save, file saving, atomic write, and backup behavior decision.

## Core principle

Operre must not silently change filesystem semantics.

Operre must not silently turn a symlink into a regular file.

Operre must not silently break hardlink relationships.

Operre must not treat special files as normal text files.

Dirty buffers must never be silently overwritten by external changes.

File watcher events must be useful without becoming noisy.

AI and extensions cannot access watcher event history by default.

Protected path watcher behavior must remain privacy-first.

## File identity model

Operre should track file identity with more than path strings.

Where supported, file identity may include:

- path used to open the file;
- canonical path;
- symlink path;
- target path;
- device ID;
- inode/file ID;
- link count;
- file type;
- size;
- mtime/ctime/change token;
- permissions;
- read-only state;
- filesystem type where practical;
- workspace trust state;
- protected path classification.

Rules:

- path string alone is not enough for safe conflict decisions;
- file identity may change after rename, replace, symlink retarget, or mount change;
- identity uncertainty must lead to cautious behavior;
- UI should expose safe file information where useful.

## lstat and stat distinction

Operre must distinguish link metadata from target metadata.

Accepted behavior:

- `lstat`-like behavior inspects the symlink itself;
- `stat`-like behavior inspects the target;
- symlink path and target path must not be confused;
- broken symlink is a valid filesystem object but not a readable regular target;
- target classification controls protected/secret/special-file policy;
- link classification controls symlink UI and save warnings.

## Path canonicalization

Operre should canonicalize paths where useful, but canonicalization must not erase user intent.

Rules:

- preserve the user-opened path;
- separately store resolved/canonical path where safe;
- do not display sensitive canonical paths unnecessarily;
- path canonicalization must respect protected path policy;
- symlink loops must be detected;
- path traversal through symlinks must not bypass workspace trust or protected path rules;
- diagnostics export may redact canonical paths.

## TOCTOU and race condition safety

Filesystem state can change between check and use.

Accepted behavior:

- permission/type/link checks must be treated as snapshots, not permanent truth;
- save operations must re-check critical assumptions close to write time;
- watcher events must not be trusted as complete truth;
- conflict handling must tolerate races;
- protected path checks must be repeated before risky actions;
- if identity is uncertain, Operre should pause Auto Save and ask the user.

## Symlink open behavior

Symlink files may be opened when the target is readable and safe.

Required behavior:

- detect symlink where practical;
- show symlink badge where useful;
- show link path and target path in File Info where safe;
- detect broken symlink;
- detect symlink loop;
- apply protected path policy to symlink target;
- apply secret-like warning to target where practical;
- do not let symlink traversal bypass workspace trust.

## Broken symlink behavior

Broken symlinks need explicit handling.

Rules:

- show broken symlink warning;
- do not treat broken symlink as empty text file silently;
- offer Remove Link only with confirmation later;
- offer Retarget Link later;
- offer Save As / Create Target only with clear explanation;
- Auto Save must remain disabled for broken symlink targets.

## Symlink save behavior

Symlink save semantics are dangerous and must be explicit.

Accepted behavior:

- saving through a symlink must not silently replace the symlink itself with a regular file;
- atomic rename must not silently break symlink semantics;
- default save strategy should preserve the user's expected target-content update where safe;
- if safe semantics are unclear, show conflict/warning UI;
- replacing the symlink object itself is advanced and confirmation-protected;
- target changes require conflict handling;
- protected target rules apply.

## Symlink target change behavior

Operre must detect important target changes.

Target change cases:

- target deleted;
- target path changed;
- symlink retargeted;
- target became read-only;
- target became protected;
- target became special file;
- target changed externally;
- target device/inode changed.

Accepted behavior:

- dirty buffer triggers conflict UI;
- Auto Save pauses;
- user may Compare, Reload, Save As, Keep Both, or Cancel;
- protected target changes trigger security-aware warnings;
- uncertain identity triggers conservative behavior.

## Hardlink detection

Hardlinks require careful handling.

Accepted behavior:

- detect link count greater than 1 where supported;
- show hardlink warning badge where useful;
- File Info should show hardlink count where safe;
- save strategy must not hide hardlink semantic changes;
- hardlink warnings should be configurable but safe by default.

## Hardlink save semantics

Hardlink saving has two different semantics.

Possible behaviors:

- in-place write: same inode, all hardlink paths see the change;
- replace/rename write: this path becomes a new inode and hardlink relationship may break.

Accepted behavior:

- Operre must not hide this difference;
- atomic write may break hardlink relationships;
- in-place write may update multiple paths;
- user content hardlinks require warning/confirmation when semantics may surprise the user;
- app-owned settings/keybindings can use atomic write according to app policy;
- detailed strategy may be selected through advanced settings later.

## Special file classification

Operre must classify special files before opening/saving.

Special file types include:

- directory;
- FIFO / named pipe;
- Unix socket;
- block device;
- character device;
- procfs/sysfs pseudo file;
- broken symlink;
- mount point;
- sparse file;
- binary file;
- extremely large file;
- permission-denied path;
- unsupported filesystem object.

## Special file open behavior

Special files must not be opened blindly as normal text files.

Rules:

- directories are opened in Explorer, not as text files;
- FIFO/socket/device files are blocked or read-only advanced mode;
- procfs/sysfs pseudo files are read-only or advanced explicit mode;
- permission-denied path shows clear error;
- binary file shows binary warning or preview mode;
- extremely large file uses Large File Mode;
- unsupported file type shows clear explanation.

## Special file save behavior

Special files require strict save boundaries.

Rules:

- do not save to device/socket/FIFO as normal text file by default;
- do not use atomic rename blindly on special files;
- do not rewrite sparse files blindly;
- do not follow special file paths to bypass protected path policy;
- require explicit advanced confirmation for risky actions;
- preserve dirty buffers on failure.

## Sparse file behavior

Sparse files need special caution.

Risks:

- rewrite may inflate sparse file size;
- atomic temp copy may consume too much disk;
- backup may consume too much disk;
- compare may be expensive.

Accepted behavior:

- detect sparse file where practical;
- warn before operations that may de-sparsify;
- Large File Mode and storage warnings apply;
- Auto Save may pause;
- user should be offered Save As where safer.

## Binary file behavior

Binary files require a safe mode.

Accepted behavior:

- binary detection should trigger warning;
- default editor should not corrupt binary files;
- binary preview/read-only mode may be used;
- editing binary as text requires explicit user intent;
- Auto Save should be disabled or warning-protected for binary files.

## File watcher purpose

File watcher tracks filesystem changes relevant to the user.

Watcher should support:

- external file changes;
- deleted files;
- renamed/moved files;
- created files;
- permission changes;
- metadata changes;
- symlink target changes where practical;
- directory tree changes;
- mount unavailable events;
- overflow/missed events;
- workspace rescan triggers.

## Watcher backend abstraction

Watcher backend must be abstracted.

Possible platform backends:

- Linux: inotify;
- macOS: FSEvents;
- Windows: ReadDirectoryChangesW;
- fallback: polling.

Rules:

- UI behavior should not depend on backend quirks;
- events should be normalized;
- polling fallback must be available;
- backend limitations must produce warnings where relevant.

## Watcher normalized event types

Normalized event types should include:

- created;
- modified;
- deleted;
- renamed;
- moved;
- permissionChanged;
- metadataChanged;
- symlinkChanged;
- targetChanged;
- directoryChanged;
- mountUnavailable;
- overflow;
- rescanRequired;
- unknown.

## Watcher debounce and deduplication

Watcher events can be noisy.

Rules:

- debounce bursts;
- deduplicate repeated events;
- group related rename/move events where practical;
- avoid showing multiple warnings for one operation;
- internal save events should not be shown as external changes;
- overflow must trigger warning and rescan.

## Internal save versus external change

Operre must distinguish its own writes from external edits.

Strategies may include:

- save transaction tracking;
- expected mtime/size update;
- write token where possible;
- file identity check;
- short suppression window;
- post-save verification.

Rules:

- internal save should not scare the user as external modification;
- uncertain state should fall back to cautious conflict handling;
- dirty buffers must not be silently overwritten.

## File changed on disk behavior

Open editors need conflict handling.

Rules:

- clean buffer may auto-reload according to settings;
- dirty buffer must never be silently reloaded;
- dirty buffer conflict UI is required;
- Auto Save must pause during conflict;
- user actions should include Compare with Disk, Reload, Keep Mine, Save As, Keep Both, and Cancel.

## Deleted or missing file behavior

If an open file is deleted or becomes missing:

- editor must not close silently;
- dirty buffer must be preserved;
- show "file deleted on disk" warning;
- allow Save As;
- allow Recreate;
- allow Discard with confirmation;
- Auto Save must pause.

## Rename and move behavior

If a file is renamed or moved externally:

- watcher may follow if identity is clear;
- if identity is uncertain, show missing/moved conflict;
- update editor title/path only when safe;
- do not silently change active path if that could surprise the user;
- user may Save As or Reconnect later.

## Workspace watcher behavior

Workspace watcher should update Explorer safely.

Rules:

- workspace tree updates should be debounced;
- ignored/excluded folders may not be watched;
- very large directories may use partial watcher mode;
- protected paths remain restricted;
- hidden file visibility remains separate from watcher existence;
- watcher events are not automatically AI/extension context.

## Watcher limits and overflow

Watcher limits must be handled explicitly.

Limit cases:

- too many files;
- too many directories;
- OS watch limit reached;
- event overflow;
- network filesystem unreliability;
- removable drive disconnect;
- polling too expensive;
- permission denied while watching.

Accepted behavior:

- show watcher limited warning;
- show watcher overflow warning;
- perform workspace rescan where safe;
- offer watcher status UI;
- allow exclude patterns;
- allow polling fallback;
- never pretend watcher is complete when it is limited.

## Snapshot reconciliation

Watcher events may be incomplete.

Operre should support snapshot reconciliation.

Rules:

- keep lightweight known file state where practical;
- rescan affected subtree after overflow or suspicious event;
- reconcile editor state against disk state before risky save;
- reconcile workspace tree after bulk operations;
- report uncertainty instead of guessing.

## Network and removable filesystem behavior

Network/removable filesystems require conservative behavior.

Rules:

- watcher events may be unreliable;
- atomic rename semantics may differ;
- mtime precision may be low;
- mount may disappear;
- save conflict handling should be more conservative;
- local Save As should be offered where practical;
- network filesystem conservative mode should be available.

## Protected path watcher behavior

Protected paths require privacy-first watcher policy.

Accepted behavior:

- protected paths may be excluded from watcher by default;
- protected path contents must not be scanned unnecessarily;
- raw protected paths may be redacted in diagnostics;
- watcher event history is not exposed to AI/extensions by default;
- secret-like filenames/paths may be redacted;
- protected target symlinks remain protected.

## Extension watcher API

Extensions may request watcher access later.

Rules:

- explicit permission is required;
- workspace scope is required;
- protected paths are excluded;
- event history is not exposed by default;
- high-volume watcher abuse must be rate-limited;
- extension telemetry remains denied by default;
- extension watcher access must respect Workspace Trust.

## AI watcher relationship

AI cannot watch workspace changes by default.

Rules:

- AI cannot receive watcher event history by default;
- AI cannot monitor protected paths;
- AI requires explicit scoped permission for workspace-change awareness later;
- raw watcher events are not hidden prompt context;
- AI may explain a visible file-changed warning only with user-visible context.

## Settings

Settings should include:

- file watcher enabled;
- watcher backend auto/polling;
- polling interval;
- watcher excludes;
- follow symlinks in explorer;
- open symlink target behavior;
- show symlink target path;
- warn on hardlinked files;
- preserve hardlink semantics strategy later;
- auto reload clean files;
- confirm reload dirty files;
- watcher notifications level;
- network filesystem conservative mode;
- protected path watcher exclusion;
- max watched files/directories;
- rescan workspace command;
- show file identity details in File Info.

## Command Palette relationship

Command Palette should expose file identity and watcher commands.

Suggested commands:

- `file.compareWithDisk`;
- `file.reloadFromDisk`;
- `file.revealSymlinkTarget`;
- `file.showFileInfo`;
- `file.showLinkInfo`;
- `workspace.rescan`;
- `watcher.restart`;
- `watcher.showStatus`;
- `settings.openFileWatcherSettings`;
- `settings.openSymlinkSettings`.

Rules:

- Command Palette must not bypass dirty conflict handling;
- Command Palette must not bypass protected path policy;
- Command Palette must not expose watcher history to AI/extensions.

## UI indicators

UI should expose risky filesystem states.

Possible indicators:

- symlink badge;
- broken symlink badge;
- hardlink warning badge;
- special file badge;
- read-only badge;
- binary file badge;
- sparse file badge;
- external changed badge;
- deleted on disk badge;
- watcher limited badge;
- watcher overflow badge;
- network/mount warning;
- protected target warning.

## Logs and diagnostics relationship

Logs and diagnostics must remain privacy-first.

Rules:

- watcher errors may be logged;
- file contents are not logged;
- watcher event history is not exported by default;
- protected raw paths may be redacted;
- symlink/target metadata may be summarized where safe;
- diagnostics may include watcher limited/overflow summary;
- diagnostics must not include protected contents.

## First implementation recommendation

Operre v0.1 should include:

- symlink detection;
- symlink link/target distinction;
- broken symlink warning;
- symlink loop detection;
- hardlink count detection where supported;
- hardlink warning when link count is greater than 1;
- special file classification;
- safe handling for device/socket/FIFO/procfs/sysfs;
- binary warning/read-only preview hook;
- sparse file warning hook;
- file changed on disk detection;
- dirty buffer conflict UI;
- delete/missing file handling;
- basic watcher backend abstraction;
- debounce/deduplication;
- internal save vs external change distinction;
- watcher overflow warning;
- workspace rescan command;
- protected path watcher exclusion or privacy-safe handling;
- AI/extension watcher access denied by default.

First version may defer:

- full extension watcher API;
- advanced symlink retarget UI;
- hardlink strategy selector;
- full sparse-preserving save implementation;
- advanced network filesystem heuristics;
- full File Info metadata viewer polish;
- advanced watcher diagnostics UI.

## Accepted decision summary

Accepted decisions:

- Symlink, hardlink, special file, and file watcher behavior must have a dedicated specification.
- Operre must not silently change filesystem semantics.
- Operre must distinguish path, canonical path, symlink path, target path, and file identity where practical.
- lstat/stat distinction is required by design.
- Symlink files may be opened, but link/target distinction must be visible where useful.
- Saving through symlink must not silently replace the symlink itself with a regular file.
- Broken symlink warning is required.
- Symlink loop detection is required.
- Hardlink count greater than 1 should trigger warning where supported.
- Atomic write must not silently break hardlink semantics for user files.
- Special files must not be treated as normal text files.
- Sparse and binary files require cautious handling.
- File watcher must detect external changes and workspace tree changes where practical.
- Dirty buffers must never be silently overwritten by external reload.
- Watcher debounce, deduplication, overflow handling, and rescan are required by design.
- Internal save events must be distinguished from external changes where practical.
- Watcher limits and network/removable filesystem unreliability must be visible.
- Protected paths must remain privacy-first in watcher behavior.
- AI and extensions cannot access watcher event history by default.
- Detailed File Explorer, workspace tree, File Info, tabs, and navigation behavior should be decided next.

## File Explorer, workspace tree, File Info, tabs, and navigation relationship

Accepted behavior:

- Explorer and File Info must expose symlink, hardlink, special-file, binary, sparse, read-only, external-change, deleted-on-disk, watcher-limited, and protected target states where useful.
- Same target opened through different symlink paths must not be silently merged.
- File Info should expose link path, target path, hardlink count, type, permissions, and watcher status where safe.
- Recent files should preserve the user-opened path where useful.
