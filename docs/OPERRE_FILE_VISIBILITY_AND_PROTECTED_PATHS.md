# Operre File Visibility and Protected Paths

## Purpose

This document defines how Operre handles hidden files, dotfiles, protected metadata folders, sensitive files, and Explorer visibility.

This decision continues the product specification after the accepted delete behavior baseline.

## Default rule

Hidden files and dotfiles are hidden by default in the Explorer.

The user can enable:

- Show Hidden Files

When disabled, hidden files and hidden folders are not shown in the normal Explorer tree.

## What counts as hidden

On Linux/macOS:

- names starting with `.`
- examples:
  - `.git`
  - `.operre`
  - `.env`
  - `.vscode`
  - `.idea`
  - `.cache`

Exceptions:

- `.`
- `..`

On Windows:

- files/folders with Hidden attribute
- files/folders with System attribute
- dot-prefixed files are also treated as hidden by Operre for cross-platform consistency.

## Explorer behavior

Default Explorer behavior:

- hidden files are hidden;
- protected paths are hidden;
- sensitive files are not surfaced casually;
- search excludes hidden/protected paths by default;
- recent history excludes protected paths by default.

When Show Hidden Files is enabled:

- hidden files become visible;
- dotfiles become visible;
- `.git/` becomes visible but protected;
- `.operre/` becomes visible but protected;
- sensitive-looking files show warnings before open/edit where appropriate.

## `.operre/` visibility

`.operre/` is hidden by default.

When Show Hidden Files is enabled:

- `.operre/` is visible;
- `.operre/` has a protected/metadata visual marker;
- destructive actions require stronger confirmation;
- some subtrees remain strongly protected.

## `.operre/` protected subtrees

Always protected:

- `.operre/audit/`
- `.operre/secrets/`
- `.operre/cache/`
- `.operre/local-state/`
- `.operre/snapshots/`

Default behavior for these subtrees:

- excluded from normal search;
- excluded from recent files/projects;
- excluded from Markdown preview resource loading;
- excluded from automatic indexing;
- excluded from AI context by default;
- not synced by default;
- not tracked by Git by default.

## `.operre/shared/`

`.operre/shared/` is the only optional shared/tracked `.operre` subtree.

Rules:

- hidden by default because it is under `.operre/`;
- visible when Show Hidden Files is enabled;
- may be tracked by Git if the project explicitly chooses it;
- must not contain secrets;
- must not contain local-only logs;
- must not contain AI prompt/response logs by default;
- must not contain caches or snapshots.

## `.git/` visibility

`.git/` is hidden by default.

When Show Hidden Files is enabled:

- `.git/` is visible;
- `.git/` has a protected/repository-metadata visual marker;
- opening text files may be allowed in read-only mode;
- destructive Explorer actions should be blocked or require an advanced confirmation;
- normal users should manage Git state through Git extension UI, not by manually editing `.git/`.

## Sensitive dotfiles

Sensitive-looking dotfiles include:

- `.env`
- `.env.*`
- `.npmrc`
- `.pypirc`
- `.netrc`
- `.ssh/`
- files containing names such as `secret`, `token`, `credential`, `private`, `key`

Default behavior:

- hidden by default;
- excluded from search by default;
- excluded from recent history by default where practical;
- never sent to AI by default;
- never included in diagnostics by default;
- warning before preview/open if Operre recognizes the file as sensitive.

## Search behavior baseline

Search default:

- include normal visible files;
- exclude hidden files;
- exclude `.git/`;
- exclude `.operre/`;
- exclude protected subtrees;
- exclude obvious binary/cache/generated files where practical.

Future search options may include:

- Include Hidden Files
- Include Git Metadata
- Include Operre Metadata

The first implementation should not expose protected metadata search by default.

## Recent files/projects baseline

Recent files/projects default:

- include normal user-opened files/projects;
- exclude protected `.operre` subtrees;
- exclude `.git` internals;
- avoid adding sensitive dotfiles to recent history by default where practical.

Future settings may allow privacy-safe recent-history customization.

## Delete behavior interaction

Accepted delete baseline remains:

- normal Delete moves item to OS Trash/Recycle Bin;
- Permanent Delete is a separate command;
- every delete operation requires confirmation;
- folder delete requires extra warning.

Additional hidden/protected path rule:

- deleting hidden files requires explicit confirmation that the file is hidden;
- deleting protected metadata paths requires stronger confirmation or is blocked;
- deleting `.operre/secrets/` must be strongly discouraged and may be blocked in normal Explorer;
- deleting `.git/` must be strongly discouraged and may be blocked in normal Explorer.

## AI interaction

AI agents cannot access hidden/protected paths by default.

AI default exclusions:

- `.git/`
- `.operre/`
- `.env`
- `.env.*`
- `.ssh/`
- secrets/tokens/credentials/private keys
- caches/logs/snapshots

AI access to hidden files requires explicit scoped permission and should still exclude protected secrets by default.

## Extension interaction

Extensions cannot access hidden/protected paths by default.

Extensions must request explicit permissions for:

- hidden files;
- workspace metadata;
- Git metadata;
- Operre metadata;
- credentials;
- secrets;
- cache/snapshot areas.

Default permission remains deny all.

## UI indicators

Possible UI indicators:

- hidden file marker;
- protected metadata marker;
- sensitive file warning;
- workspace trust warning;
- extension access warning.

The first version can use simple labels/icons, but the policy must already exist.

## Accepted decision summary

Accepted decisions:

- Hidden files/dotfiles are hidden by default.
- Show Hidden Files toggle is required.
- `.operre/` is hidden by default and protected when visible.
- `.git/` is hidden by default and protected when visible.
- `.operre/audit/`, `.operre/secrets/`, `.operre/cache/`, `.operre/local-state/`, and `.operre/snapshots/` are always protected.
- `.operre/shared/` is the only optional shared/tracked `.operre` subtree.
- Sensitive dotfiles such as `.env` are hidden, excluded from search/recent by default where practical, and never sent to AI by default.
- Search excludes hidden/protected paths by default.
- Recent history excludes protected paths by default.
- AI and extensions cannot access hidden/protected paths without explicit scoped permission.

## Search/compare interaction with hidden and protected paths

Accepted behavior:

- Search excludes hidden/protected paths by default.
- File compare follows the same hidden/protected path safety model.
- Include Hidden Files does not automatically include protected paths.
- `.git/`, `.operre/`, `.env`, `.env.*`, `.ssh/`, secrets, tokens, credentials, private keys, caches, logs, and snapshots are excluded by default.
- If a sensitive file is manually opened for compare, Operre should warn before compare where practical.

## Recent history interaction with protected paths

Accepted behavior:

- `.git/` internals are excluded from recent history by default.
- `.operre/audit/`, `.operre/secrets/`, `.operre/cache/`, `.operre/local-state/`, and `.operre/snapshots/` are excluded from recent history by default.
- `.env`, `.env.*`, `.ssh/`, secrets, tokens, credentials, and private keys are excluded from recent history by default.
- Hidden/generated/cache/log files are excluded where practical.

## Warning relationship with protected paths

Accepted behavior:

- Protected path access attempts should produce clear warnings.
- Secret/token/private-key exposure warnings are security warnings.
- Protected path warning details must avoid leaking sensitive contents.
- Diagnostics export must exclude protected path contents by default.

## Logs and diagnostics protected path baseline

Accepted behavior:

- Protected path contents are not included in logs or diagnostics export by default.
- Diagnostics export should redact protected paths by default.
- Secret-like path segments should be redacted.
- Diagnostics export must not include raw `.env`, credentials, private keys, or hidden/protected contents by default.

## Crash recovery protected path baseline

Accepted behavior:

- Protected path recovery content is local-only by default.
- Protected path recovery content is not included in diagnostics export by default.
- Protected path recovery content is hidden from AI/extensions by default.
- Recovery UI may redact protected paths and show privacy warnings.
- Secret-like recovered content should trigger security warnings where practical.

## Save behavior protected path baseline

Accepted behavior:

- Protected/secret-like file saving requires strict privacy boundaries.
- Auto Save should be cautious or paused for protected/secret-like files.
- Backup/recovery/diagnostics export must not include protected contents by default.
- Secret/token exposure warning is required where practical.

## Symlink, hardlink, special file, and watcher protected path baseline

Accepted behavior:

- Protected paths may be excluded from watcher by default.
- Symlink targets inside protected paths remain protected.
- Protected path contents must not be scanned unnecessarily.
- Secret-like filenames/paths may be redacted.
- Watcher event history is not exposed to AI/extensions by default.
