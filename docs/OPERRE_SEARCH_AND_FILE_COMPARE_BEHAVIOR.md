# Operre Search and File Compare Behavior

## Purpose

This document defines Operre's detailed search, replace, and file comparison behavior.

This decision follows the hidden files, dotfiles, and protected paths decision.

## Search principle

Search must be useful, predictable, local-first, and safe by default.

Default search must not expose protected metadata, secrets, AI logs, cache data, raw diagnostics, or hidden sensitive files.

## Current file search

Shortcut:

- Ctrl+F

Scope:

- active file only.

Required features:

- search input;
- next match;
- previous match;
- match count;
- current match position;
- case sensitive toggle;
- whole word toggle;
- regex toggle;
- highlight all matches;
- clear search;
- keyboard navigation.

Default behavior:

- search inside the currently opened text/editor model;
- no filesystem scanning;
- no hidden/protected path issue because scope is current file.

## Opened folder / project search

Shortcut:

- Ctrl+Shift+F

Scope:

- only the folder/project explicitly opened by the user.

Required features:

- search query;
- include/exclude glob patterns later;
- case sensitive toggle;
- whole word toggle;
- regex toggle;
- result grouping by file;
- line preview;
- click result to open file at line/column;
- result count;
- skipped file count where practical.

Default exclusions:

- `.git/`;
- `.operre/`;
- `.env`;
- `.env.*`;
- `.ssh/`;
- hidden files and dotfiles;
- protected paths;
- binary files;
- large generated files;
- cache folders;
- log folders;
- dependency/build output folders.

Common generated/dependency exclusions:

- `node_modules/`;
- `dist/`;
- `build/`;
- `target/`;
- `.cache/`;
- `cache/`;
- `logs/`;
- `tmp/`;
- `temp/`.

## Hidden and protected paths in search

Hidden files:

- excluded by default;
- may be included through an Include Hidden Files toggle.

Protected paths:

- excluded by default;
- not included by the normal Include Hidden Files toggle;
- require separate advanced permission/confirmation if ever supported.

Protected examples:

- `.git/`;
- `.operre/audit/`;
- `.operre/secrets/`;
- `.operre/cache/`;
- `.operre/local-state/`;
- `.operre/snapshots/`.

## Binary files

Binary files are skipped by default.

UI should show a safe message such as:

- Binary file skipped.

Binary search is not part of the first core.

## Search history

Search history is local-only.

Default behavior:

- store only safe search history;
- do not store sensitive-looking queries where practical;
- do not store protected path searches by default;
- allow user to clear search history.

Search history must not be uploaded by default.

## Replace in current file

Shortcut:

- Ctrl+H

Scope:

- active file only.

Required features:

- replace one;
- replace all;
- preview current match;
- undo support through editor undo stack;
- case sensitive toggle;
- whole word toggle;
- regex toggle.

## Replace in files

Replace in files is more dangerous than search.

Accepted behavior:

- available later or advanced in first version;
- must not silently change files;
- must show preview before applying;
- must show affected file list;
- must show match count;
- must require confirmation;
- must support undo/snapshot strategy where practical;
- must exclude hidden/protected paths by default;
- must not replace inside `.git/`, `.operre/secrets/`, AI logs, caches, or binary files.

First implementation recommendation:

- implement current-file replace first;
- implement replace-in-files only with strong preview/confirmation.

## File compare feature

Operre must include a file comparison feature.

Use cases:

- compare two similar files;
- compare two versions of a document;
- compare generated output with expected output;
- compare configuration files;
- compare source files with small differences;
- compare more than two related files later.

## Two-file compare

Two-file compare is required.

Layouts:

- side-by-side;
- stacked / top-bottom.

Required behavior:

- synchronized scrolling option;
- line-level diff;
- word-level diff option;
- character-level diff option later;
- show changed lines clearly;
- show same/unchanged lines normally;
- optional unchanged-line highlighting;
- collapse unchanged sections later;
- open either file from Explorer/context menu;
- compare selected file with active file;
- compare two selected files.

## Multi-file compare

Operre should support two or more files in the design.

Practical model:

- choose a baseline file;
- compare selected files against baseline;
- show per-file differences;
- allow opening pairwise compare views;
- later allow grouped multi-file compare dashboard.

First implementation may start with two-file compare, but architecture must not block multi-file compare.

## Compare highlighting

Default visual policy:

- differences are highlighted clearly;
- changed/different areas may use red background or red-tinted background;
- unchanged/same areas are normally not highlighted strongly;
- unchanged/same areas may optionally use green background or green-tinted background if the user enables it.

Accepted user preference:

- red background-color for differences is acceptable;
- green background-color for identical/same areas is optional;
- user settings must allow detailed control.

Possible diff color semantics:

- removed/left-only content: red-tinted background;
- added/right-only content: green-tinted or separate accent;
- modified content: red/orange-tinted difference marker;
- identical content: normal background by default;
- identical content optional green background if enabled.

Important accessibility rule:

- color must not be the only signal;
- icons, gutters, line markers, or labels should also indicate changes where practical.

## Compare settings

Settings should control:

- default layout: side-by-side or stacked;
- synchronized scrolling on/off;
- highlight differences on/off;
- highlight same/identical regions on/off;
- show unchanged sections on/off;
- collapse unchanged sections on/off later;
- diff granularity: line / word / character;
- ignore whitespace on/off;
- ignore leading/trailing whitespace on/off;
- ignore line endings on/off;
- ignore case on/off;
- ignore blank lines on/off;
- wrap long lines on/off;
- show minimap/overview on/off;
- color/highlight intensity;
- accessibility-friendly indicators.

## Compare and protected paths

File compare follows the same safety model as search.

Default exclusions:

- hidden/protected paths;
- `.git/`;
- `.operre/`;
- `.env`;
- `.env.*`;
- `.ssh/`;
- secrets/tokens/credentials/private keys;
- binary files unless a binary compare feature is explicitly added later.

If the user manually opens a sensitive file, Operre should warn before compare where practical.

## Compare and AI

AI cannot access compare contents by default.

AI cannot read compared files unless:

- the user explicitly grants scoped AI permission;
- protected/sensitive paths remain denied by default;
- action is logged.

## Compare and extensions

Extensions cannot receive compare contents by default.

Extensions require explicit scoped permission for:

- reading compared files;
- contributing compare viewers;
- exporting compare reports;
- sending compare data externally.

## Compare export

Future compare export may include:

- Markdown report;
- HTML report;
- patch/diff file;
- unified diff;
- side-by-side HTML.

Not first core unless explicitly selected later.

## First implementation recommendation

Operre Search v0.1 should include:

- current file search;
- opened folder/project search;
- replace in current file;
- basic two-file compare;
- side-by-side compare;
- stacked compare;
- red/difference highlighting;
- optional same/green highlighting setting;
- hidden/protected path exclusions.

Replace in files should be added carefully with preview/diff/confirmation.

Multi-file compare should be supported by architecture and may be implemented after two-file compare.

## Accepted decision summary

Accepted decisions:

- Current file search is required.
- Opened folder/project search is required.
- Replace in current file is required.
- Replace in files requires preview and confirmation.
- Search excludes hidden/protected/generated/binary paths by default.
- Include Hidden Files toggle may include hidden files but not protected paths by default.
- File compare is required.
- Two-file side-by-side compare is required.
- Two-file stacked compare is required.
- Multi-file compare must be supported by design.
- Differences may use red background-color.
- Same/identical content may optionally use green background-color.
- Compare UI details must be user-configurable.
- Compare follows hidden/protected path safety rules.
- AI and extensions cannot access search/compare contents without explicit scoped permission.

## Large file search and compare baseline

Accepted behavior:

- Large file search should be streaming-capable.
- Large file search should show progress and allow cancel.
- Large file search may limit initial result count.
- Large file compare should be line/chunk first.
- Word/character diff may be disabled automatically above thresholds.
- Detailed diff may be offered for selected ranges later.
- Full multi-file compare of very large files should be carefully limited and cancellable.

## Recent history relationship

Accepted behavior:

- Search history is separate from Recent Files.
- Recent Comparisons may be added later and must be separate from Recent Files.
- Recent comparison entries must apply sensitive/protected exclusions.
- Missing files in recent comparisons should be marked as missing.

## Settings relationship

Accepted behavior:

- Search defaults must be configurable.
- Replace safety behavior must be configurable without weakening protected path defaults silently.
- File compare layout and highlight behavior must be configurable.
- Search history settings are separate from Recent Files.
- Include Hidden Files does not automatically include protected paths.

## Warning relationship

Accepted behavior:

- Replace in Files requires strong confirmation.
- Hidden/protected exclusions, binary skips, large file limits, too many results, expensive compare, and disabled word/character diff should produce clear warnings where useful.
- Search/compare warnings should be configurable where safe but must not weaken protected path safety silently.
