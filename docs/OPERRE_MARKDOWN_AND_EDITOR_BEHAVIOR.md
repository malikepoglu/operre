# Operre Markdown and Editor Behavior

## Default file/language support

Initial default file support:

- `.txt`;
- `.md`;
- `.html`;
- `.css`;
- `.js`;
- `.ts`;
- `.json`;
- `.sql`;
- `.c`;
- `.cpp`;
- `.h`;
- `.hpp`;
- `.java`;
- `.php`;
- `.py`;
- `.sh`;
- `.xml`;
- `.yaml`;
- `.yml`.

Purpose:

- open;
- edit;
- save;
- syntax highlighting;
- language-aware basic behavior.

This is not full IDE support.

## Language isolation

One file must have one active primary language mode.

Controlled embedded cases may exist:

- HTML with CSS/JS blocks;
- PHP with HTML/PHP blocks;
- Markdown with fenced code blocks.

Even in embedded cases, language behavior must be scoped and safe.

## Basic editing

Initial basic editing includes:

- line numbers;
- tab/space settings;
- indentation;
- auto indent;
- bracket matching;
- basic find/replace;
- multi-cursor;
- undo/redo;
- selection tools;
- word wrap;
- read-only mode;
- file encoding detection/warnings.

## Encoding and BOM

Default encoding:

- UTF-8 without BOM.

Rules:

- UTF-8 with BOM option available;
- preserve existing BOM state by default;
- user can convert with BOM / without BOM;
- risky file types may warn if BOM is added.

Risky examples:

- `.sh`;
- `.py`;
- `.php`;
- `.js`;
- `.json`;
- `.yaml`;
- `.env`;
- Dockerfile;
- Makefile.

## Line endings

Policy:

- new files default: LF on all platforms, including Windows;
- existing files: preserve;
- user conversion: LF / CRLF;
- mixed line endings: warning;
- status bar: show LF/CRLF.

## Indentation

Policy:

- default: language-aware;
- default insert: spaces;
- existing files: detect and preserve;
- user conversion: tabs <-> spaces;
- mixed indentation: warning;
- status bar: show current indentation.

Language-aware defaults:

- `.txt`: no strong indentation rule;
- `.md`: 2 spaces;
- `.html`: 2 spaces;
- `.css`: 2 spaces;
- `.js` / `.ts`: 2 spaces;
- `.json`: 2 spaces;
- `.yaml` / `.yml`: 2 spaces;
- `.sql`: 2 spaces initially;
- `.py`: 4 spaces;
- `.c` / `.h`: 4 spaces;
- `.cpp` / `.hpp`: 4 spaces;
- `.java`: 4 spaces;
- `.php`: 4 spaces;
- `.sh`: 2 spaces initially.

## Theme

Default theme:

- System.

Built-in options:

- System;
- Light;
- Dark;
- Gray background / neutral gray;
- High contrast.

Do not assume dark mode preference.

## Font

Default editor font:

- system monospace.

Reason:

- avoid bundled proprietary font licensing problems.

User options:

- font family;
- font size;
- line height;
- ligatures on/off.

## Markdown behavior

When `.md` opens:

- default: edit mode.

User can switch to:

- preview only;
- side-by-side edit + preview;
- live preview toggle.

Users can create their own `.md` files.

## Markdown licensing

Markdown files created by users belong to users.

Markdown format support is acceptable, but parser/renderer dependencies must be license-audited before implementation.

Rules:

- prefer permissive dependencies;
- preserve required license notices;
- add a third-party notices mechanism later;
- verify official dependency license sources before implementation.

## Markdown preview security

Default security:

- raw HTML disabled or sanitized;
- scripts always blocked;
- remote images/resources blocked by default;
- local images allowed only from current workspace;
- yellow warning bar shown when content is blocked or downgraded.

Warning bar style:

- web-browser-like;
- top yellow warning bar;
- clear message;
- safe management actions.

Example warning:

- Remote resources were blocked for your safety.
- Allow for this file.
- Allow for this workspace.
- Settings.

## Source 4 Markdown baseline

The `4.odt` review confirms Markdown behavior and security.

Accepted Markdown behavior:

- users can create `.md` files;
- `.md` opens in edit mode by default;
- preview only mode exists;
- side-by-side edit + preview exists;
- live preview toggle exists.

Accepted Markdown preview security:

- raw HTML disabled or sanitized;
- scripts always blocked;
- remote images/resources blocked by default;
- local images allowed only from current workspace;
- blocked/downgraded content displays a browser-like yellow top warning bar.

Dependency rule:

- Markdown parser/renderer must be license-audited before implementation.

## Large file editor behavior baseline

Accepted editor behavior:

- Large files may disable expensive editor features.
- Lazy syntax highlighting is required for large files.
- Full-document analysis may be disabled above thresholds.
- Minimap may be disabled above thresholds.
- Read-only fallback is allowed for very large files.
- User can override with warning where practical.

## Crash recovery and unsaved editor work baseline

Accepted editor behavior:

- Unsaved editor buffers should be recoverable after crash.
- Untitled documents must be recoverable.
- Dirty files should be recoverable.
- Markdown edits should be recoverable.
- Recovery actions should include Recover, Compare, Save As, Keep Both, and Discard where practical.
- Auto Save remains separate from Crash Recovery.

## Auto Save and editor save baseline

Accepted editor behavior:

- Auto Save is OFF by default.
- Auto Save can be enabled by user preference.
- Manual Save and Save As must be safe and conflict-aware.
- Save failure must preserve dirty buffer.
- File changed on disk detection is required by design.
- Encoding and line endings should be preserved where practical.

## Symlink, hardlink, special file, and watcher editor relationship

Accepted editor behavior:

- Dirty buffers must never be silently overwritten by external reload.
- File changed on disk requires conflict handling.
- Deleted-on-disk files must not close the editor silently.
- Binary/special file editing must be warning-protected.
- File Info should be reachable from editor context where practical.
