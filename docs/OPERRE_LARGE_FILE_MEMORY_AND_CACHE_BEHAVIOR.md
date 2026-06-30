# Operre Large File Memory and Cache Behavior

## Purpose

This document defines how Operre should open, search, compare, preview, and manage very large files without uncontrolled memory usage.

This decision follows the search, replace, and file compare behavior decision.

## Core principle

Operre must be able to open very large files efficiently.

Large files must not be loaded into memory blindly.

Operre should prefer:

- bounded memory usage;
- lazy loading;
- streaming reads;
- chunk-based processing;
- user-visible warnings;
- safe feature downgrades;
- configurable thresholds;
- clear cache cleanup.

## File size modes

Operre should have multiple file handling modes.

### Normal file mode

Used for small and medium files.

Behavior:

- normal editor model;
- normal syntax highlighting;
- normal search;
- normal replace;
- normal minimap;
- normal file compare;
- normal undo/redo behavior.

### Large File Mode

Used when file size crosses a configured threshold.

Behavior:

- warning before opening where practical;
- memory-conscious loading;
- lazy syntax highlighting;
- limited expensive editor features;
- optional read-only opening;
- streaming search;
- safer replace rules;
- simplified compare rules for large files.

### Very Large File Mode

Used for extremely large files.

Behavior:

- streaming/chunked reading preferred;
- file may open read-only by default;
- only viewport-near content is prioritized;
- full-document analysis is disabled;
- full minimap is disabled;
- semantic/language tooling is disabled;
- search is streaming/limited;
- compare is line/chunk based;
- word/character diff may be disabled automatically.

## Suggested thresholds

Initial suggested thresholds:

- 50 MB: show large file warning;
- 100 MB: recommend Large File Mode;
- 500 MB and above: recommend Very Large File Mode / streaming mode.

Rules:

- these thresholds are defaults, not hard-coded forever;
- user can change thresholds in settings;
- hardware capability may influence recommendations;
- memory budget setting may lower or raise automatic behavior.

## Opening large files

When opening a large file, Operre should show a clear warning.

Example message:

- This is a large file. Some features may be limited for performance.

Possible choices:

- Open in Large File Mode;
- Open Read-only;
- Open normally anyway;
- Cancel.

## Read-only fallback

Large files may open read-only by default when needed.

Read-only fallback is useful when:

- file is too large for safe editing;
- encoding detection is expensive;
- line indexing is expensive;
- memory budget would be exceeded;
- file is likely generated/log/cache output;
- file is opened from a sensitive/protected area.

The user may choose Edit Anyway, but Operre should show a performance and safety warning.

## Streaming / chunked reading

Very large files should be read in chunks.

Behavior:

- do not load the whole file into RAM by default;
- load visible region first;
- load viewport-near regions next;
- cache recently viewed chunks;
- evict older chunks when memory budget is reached;
- keep file offsets/indexes where practical;
- avoid blocking the UI thread.

## Line index strategy

Large file navigation needs efficient line handling.

Possible strategy:

- build partial line index;
- build full line index lazily;
- store line offsets in bounded memory;
- optionally store temporary index in cache;
- invalidate index if file changes;
- show progress for long indexing tasks.

## Syntax highlighting in large files

Large files should use lazy syntax highlighting.

Behavior:

- highlight visible lines first;
- highlight nearby buffered lines next;
- disable full-document syntax passes;
- disable expensive semantic analysis;
- disable deep language intelligence by default;
- allow user override from settings.

## Minimap in large files

Default behavior:

- disable full minimap after a configured threshold;
- show simplified overview if cheap;
- allow user to force minimap with warning;
- allow per-user setting.

Reason:

- full minimap can be expensive for huge files.

## Search in large files

Large file search must be streaming-capable.

Behavior:

- do not require full file load;
- scan chunks;
- show progress;
- show partial results early;
- allow cancel;
- cap initial result count;
- allow continue search;
- avoid storing sensitive results in history;
- skip protected paths by default.

Possible default result limit:

- first 1000 matches.

User actions:

- continue search;
- refine query;
- stop search;
- open result.

## Replace in large files

Replace in large files is dangerous.

Default behavior:

- current-file replace may be available only after warning;
- replace-all requires preview;
- large-file replace-all requires confirmation;
- replace-in-files with large files requires stronger confirmation;
- create backup/snapshot strategy where practical;
- never silently rewrite a very large file.

Very large file replace may require a streaming rewrite strategy instead of in-place editing.

## File compare with large files

Large file compare must be memory-conscious.

Behavior:

- do not load both full files into RAM blindly;
- prefer line/chunk based comparison;
- show progress;
- allow cancel;
- disable word/character diff automatically above threshold;
- allow line-level diff first;
- allow detailed diff on selected sections later;
- support side-by-side and stacked layouts where practical.

For very large files:

- full diff may be expensive;
- Operre should warn user;
- Operre may offer approximate/limited diff;
- Operre may compare selected ranges;
- Operre may compare first N matches/changes;
- Operre may require user confirmation for full compare.

## Multi-file compare with large files

Multi-file compare is especially expensive.

Rules:

- choose baseline file;
- compare others against baseline;
- process one pair at a time where practical;
- avoid holding all full file contents in memory;
- show progress and memory warning;
- allow cancel;
- limit word/character-level detail by default.

## Cache management

Large file support may use cache.

Cache may include:

- temporary chunk cache;
- line offset index;
- preview cache;
- search result cache;
- compare index/cache;
- syntax token cache.

Rules:

- cache is untrusted;
- cache must be cleanable;
- cache must have size limits;
- cache must not store secrets by design;
- cache must not be synced by default;
- cache must not be committed;
- cache follows protected path rules;
- cache must respect workspace/project isolation.

## Cache path

Global cache follows existing Operre cache policy.

Linux:

- `~/.cache/operre/`

Windows:

- `%LOCALAPPDATA%\Operre\cache\`

macOS:

- `~/Library/Caches/Operre/`

Large file cache may live under a dedicated subfolder such as:

- `large-file-cache/`
- `large-file-index/`
- `compare-cache/`

## Memory budget

Operre should support user-configurable memory behavior.

Possible modes:

- Low memory;
- Balanced;
- Performance;
- Custom.

Settings may include:

- maximum memory budget in MB;
- maximum cache size;
- maximum open large files;
- maximum search result count;
- maximum compare result count;
- chunk size;
- line index cache on/off;
- minimap disable threshold;
- syntax highlighting disable threshold;
- compare detail threshold.

## Feature downgrade policy

Large File Mode may limit features automatically.

Possible downgrades:

- full minimap disabled;
- full syntax highlighting disabled;
- semantic analysis disabled;
- language server disabled;
- document outline disabled;
- full file decorations disabled;
- word/character diff disabled;
- full replace-all requires confirmation;
- auto-format disabled;
- AI context disabled by default.

UI must make downgrades visible.

## User settings

Large file settings should include:

- large file warning threshold;
- Large File Mode threshold;
- Very Large File Mode threshold;
- default open mode for large files;
- read-only fallback on/off;
- Edit Anyway availability;
- memory mode;
- custom memory limit;
- cache size limit;
- cache cleanup policy;
- streaming search result limit;
- compare mode threshold;
- disable minimap threshold;
- lazy syntax highlighting on/off;
- disable semantic tooling threshold;
- warn before replace-all in large file;
- warn before large file compare;
- allow detailed diff on selected ranges.

## UI status indicators

Large file UI should show clear state.

Possible indicators:

- Large File Mode badge;
- Read-only badge;
- Streaming search progress;
- Chunk loading progress;
- Feature-limited warning;
- Cache/memory warning;
- Compare limited-mode warning.

## Privacy and security

Large file memory/cache handling must respect existing privacy rules.

Rules:

- large file chunks are not uploaded by default;
- cache is local-only;
- protected paths are excluded by default;
- AI cannot access large file content by default;
- extensions cannot access large file content by default;
- diagnostics must not include large file contents;
- search/compare cache must not leak sensitive paths/content;
- cache must be clearable.

## AI interaction

AI access to large file contents is denied by default.

If enabled:

- access must be scoped;
- selected ranges preferred over whole file;
- user must see what content is sent;
- action must be logged;
- protected/sensitive paths remain denied by default.

## Extension interaction

Extensions cannot receive large file content by default.

Extensions need explicit permission for:

- reading large files;
- indexing large files;
- contributing large file viewers;
- contributing compare engines;
- exporting large file search/compare data.

## Implementation notes

First implementation should not try to perfect every large-file feature.

However, architecture must not require full-file memory loading.

Minimum architecture direction:

- separate editor model from file storage model;
- allow streaming reader abstraction;
- allow chunk cache abstraction;
- allow lazy line index;
- allow feature downgrade flags;
- allow cancellation for long operations;
- keep UI responsive.

## First implementation recommendation

Operre v0.1 should include:

- large file warning;
- Large File Mode concept;
- read-only fallback;
- disable full minimap for large files;
- lazy/limited syntax highlighting;
- streaming-capable search architecture;
- line/chunk-first large file compare architecture;
- bounded cache settings;
- cache cleanup command;
- user-configurable thresholds.

Very large file full editing, streaming replace, and advanced multi-file compare can come later.

## Accepted decision summary

Accepted decisions:

- large file support must be part of architecture from the beginning;
- very large files must not be loaded fully into RAM blindly;
- Large File Mode is required;
- Very Large File Mode / streaming mode is required as a design target;
- read-only fallback is required;
- streaming/chunked reading is required as a design target;
- lazy syntax highlighting is required for large files;
- minimap and semantic tooling may be disabled above thresholds;
- large file search should be streaming-capable;
- large file compare should be line/chunk first;
- word/character diff may be disabled automatically for large files;
- cache must be bounded, cleanable, local-only, and protected;
- memory budget settings are required;
- user must be able to configure thresholds and behavior;
- AI and extensions cannot access large file content without explicit scoped permission;
- next topic remains Recent files/projects behavior.

## Recent history interaction with large files

Accepted behavior:

- Large files may be added to Recent Files if opened normally.
- Large File marker should be shown where useful.
- Recent history must not store file contents, chunks, search results, or compare results.
- Large file recent behavior must still respect protected/sensitive exclusions.

## Settings relationship

Accepted behavior:

- Large file thresholds must be configurable.
- Large file memory budget must be configurable.
- Large file cache size and cleanup policy must be configurable.
- Large File Mode behavior must be visible and configurable where practical.
- Machine-local performance settings should not sync by default.

## Warning relationship

Accepted behavior:

- Large File Mode, Very Large File Mode, feature disabled states, search limits, compare limits, memory/cache pressure, and read-only fallback should produce clear warnings where useful.
- Large file warnings should be informative without becoming noisy.
- Large file warnings must respect notification fatigue controls.
