# Operre Specifications

This document records Operre product decisions, architecture decisions, security rules, UX rules, storage rules, repository discipline, extension model, and accepted planning decisions.

The specification is intentionally detailed. Operre must be disciplined from the beginning.

Current phase:

- specification consolidation first;
- implementation TODO after specifications are stable;
- code only after product and repository rules are clear.

## 1. Product identity

### 1.1 Name

Product name:

- Operre

Domain:

- operre.com

### 1.2 Meaning

The domain was originally chosen with operation research in mind.

The name can also be interpreted through:

- operation;
- operate;
- operation research;
- organize;
- prepare;
- execute;
- repository;
- workspace;
- German "Oper" as a stage/performance metaphor.

Internal interpretation:

> Operre is a lightweight place where projects are prepared, organized, and performed.

The stage/performance metaphor should remain subtle. Operre must stay technical, clean, and lightweight, not overly poetic.

### 1.3 Product type

Operre is a lightweight, independent, cross-platform project working environment.

It starts as a fast Notepad-like editor and grows into a project platform through extensions and connectors.

### 1.4 Independence rule

Operre must be independent.

It must not require:

- Ideboard;
- GitHub;
- cloud account;
- AI account;
- online sync;
- marketplace account.

Ideboard may later connect through an optional Connector Extension.

### 1.5 Source model

Operre is not planned as open source.

Rules:

- the basic/core application may be free;
- future extensions may be free or paid;
- the internal development repository should normally be private;
- the current public state is temporary for inspection/setup;
- a separate public repository may later be created for public distribution or public documentation.

## 2. Project relationship and priority

### 2.1 LogisticSearch relationship

Operre can be developed in parallel with LogisticSearch.

LogisticSearch is a long-running project involving crawler, backend, frontend, infrastructure, runtime work, Raspberry Pi deployment, and strict repository discipline.

Operre should use a similarly strict audit, documentation, commit, push, and TODO discipline, but Operre is a separate product and repository.

### 2.2 Ideboard relationship

Ideboard is a separate project and separate application.

Ideboard may later become:

- a meeting environment;
- a collaboration environment;
- a project/future board platform;
- a separate cross-platform workspace;
- an optional Operre Connector Extension.

Ideboard must not be part of Operre core.

### 2.3 Historical idea evolution

The early idea moved through these stages:

1. general editor/workspace connected with ideboard.com;
2. code + drawing + diagram + project board environment;
3. separate project from Ideboard;
4. final project name/domain decision: Operre / operre.com;
5. final direction: lightweight independent project platform, local-first, extension-driven.

Superseded idea:

- Operre must not be an Ideboard shell.
- Operre must not start as a huge IDE.
- Operre must not start as a cloud-first collaboration platform.

Accepted idea:

- Operre starts as a very lightweight editor and grows through controlled extensions.

## 3. Development discipline

### 3.1 Repository as memory

The GitHub repository is the project memory.

Every meaningful detail must be recorded.

### 3.2 Documentation-first rule

Documentation is mandatory.

Document:

- product ideas;
- accepted decisions;
- rejected decisions;
- architecture decisions;
- security decisions;
- storage paths;
- user data rules;
- extension rules;
- UI/UX behavior;
- implementation details;
- TODO state changes;
- completed work;
- post-push audit state.

### 3.3 Specification before implementation

Current rule:

- finish detailed specifications first;
- do not start application implementation until the accepted specification baseline is stable;
- after specifications are stable, create detailed TODO/work plan;
- then implement step by step.

### 3.4 TODO-driven workflow

After the specification phase, all work must flow through TODO.

Workflow:

1. Select one TODO item.
2. Audit current state.
3. Implement or document.
4. Verify.
5. Update documentation.
6. Update TODO.
7. Review git diff.
8. Commit.
9. Push.
10. Post-push audit.

### 3.5 Language rule

Repository documentation and planning must be English-only.

Chat discussion can be Turkish, but GitHub documentation must be English.

### 3.6 Terminal/audit style

Operre should follow the disciplined terminal workflow used for LogisticSearch:

- named Bash code blocks;
- read-only audit blocks before write blocks;
- explicit paths;
- fail fast on dirty worktrees;
- post-push audit;
- no silent assumptions;
- no hidden state changes.

## 4. Product principles

Operre must be:

- very lightweight;
- local-first;
- privacy-first;
- secure by default;
- extension-driven;
- usable as a simple text editor;
- useful offline;
- usable without account;
- usable without cloud;
- ergonomic across environments;
- clear and disciplined;
- useful to both general users and technical users.

Core principle:

> Core-first, cloud-optional, extension-driven.

### 4.1 Notepad-like start

Operre must initially feel closer to the old Windows 10 Notepad than to a huge IDE.

Initial user expectation:

- install/open quickly;
- create `.txt`;
- type text;
- save;
- close;
- reopen.

Windows 11 Notepad is not the reference experience. The older simple Notepad feeling is the preferred lightweight reference.

### 4.2 Growth model

Core must remain small.

Additional capabilities must come through:

- Built-in Features;
- Extensions;
- Connectors;
- Services.

## 5. Technology stack

### 5.1 Preferred stack

Preferred stack:

- Tauri;
- Rust native side through Tauri;
- Monaco Editor;
- TypeScript;
- Vite;
- Solid;
- pnpm.

### 5.2 Fallback stack

Fallbacks:

- Electron as desktop fallback;
- React as frontend fallback;
- Svelte not first choice.

### 5.3 Rationale

Tauri is preferred because Operre must be lightweight, security-conscious, and potentially suitable for future tablet/mobile direction.

Electron remains a fallback because it is mature and proven for VS Code-like applications, but it is heavier.

Solid is preferred because it is lightweight and suitable for fast UI.

React remains a fallback because of its ecosystem and broad library support.

Svelte is not the first choice.

pnpm is preferred because it is efficient, strict, and suitable for workspace/extension architecture.

### 5.4 Package manager rule

Operre uses pnpm.

Allowed:

- pnpm-lock.yaml;
- pnpm-workspace.yaml when needed;
- packageManager field in package.json.

Forbidden:

- package-lock.json;
- yarn.lock;
- bun.lockb.

### 5.5 Monaco Editor decision

Monaco Editor is the preferred editor engine.

Important distinction:

- Monaco is the editor engine.
- Monaco is not the full VS Code workbench.
- Explorer, command palette, extension host, terminal, Git UI, settings UI, and security model must be designed by Operre.

Monaco may support:

- text buffer;
- syntax highlighting;
- multi-cursor;
- diff editor;
- minimap;
- decorations;
- editor model;
- language workers.

Operre must not assume that Monaco alone provides IDE behavior.

## 6. Platform order and ergonomics

Initial target order:

1. Linux Desktop
2. Windows Desktop
3. macOS Desktop
4. Tablet/mobile later

Monaco Editor weight is not considered the primary problem for mobile.

The primary mobile/tablet challenge is ergonomics.

Design rule:

> Same core. Adaptive ergonomics.

Desktop ergonomics:

- keyboard;
- mouse;
- multi-panel layout;
- split editor;
- folder tree;
- minimap;
- command palette;
- classic menu.

Tablet ergonomics:

- touch;
- optional keyboard;
- simplified panel switching;
- adaptive minimap behavior;
- larger hit targets.

Phone ergonomics:

- fast notes;
- small edits;
- preview;
- focused single-file workflows;
- adaptive UI shell.

Operre should keep a future path open for tablet and phone without weakening the desktop-first plan.

## 7. Data and storage paths

### 7.1 User workspace

Default user workspace path must avoid spaces.

Linux/macOS:

- `~/Operre/Works/`

Windows:

- `%USERPROFILE%\Operre\Works\`

### 7.2 Workspace folders

Default user workspace structure:

- `~/Operre/Works/Notes/`
- `~/Operre/Works/Projects/`
- `~/Operre/Works/Diagrams/`
- `~/Operre/Works/Cad/`
- `~/Operre/Works/Exports/`
- `~/Operre/Works/Scratch/`
- `~/Operre/Works/Templates/`

Rules:

- Diagrams and Cad must be separate.
- Users may change the default workspace path.
- Users without a formal project can save simple notes into the default workspace or their chosen directory.

### 7.3 Installed extension code

Installed/runnable extension code must be separated from user work data.

Linux:

- `~/.local/share/operre/extensions/`

Windows:

- `%APPDATA%\Operre\extensions\`

macOS:

- `~/Library/Application Support/Operre/extensions/`

### 7.4 Application configuration

Linux:

- `~/.config/operre/`

Windows:

- `%APPDATA%\Operre\config\`

macOS:

- `~/Library/Application Support/Operre/config/`

Example files:

- settings.json;
- keybindings.json;
- workspace-defaults.json;
- extensions-enabled.json.

### 7.5 Cache, temporary, and generated data

Linux:

- `~/.cache/operre/`

Windows:

- `%LOCALAPPDATA%\Operre\cache\`

macOS:

- `~/Library/Caches/Operre/`

Possible subfolders:

- preview-cache/;
- syntax-cache/;
- thumbnail-cache/;
- extension-cache/;
- download-cache/;
- temporary-build-cache/.

Security rules:

- cache is not trusted;
- no secrets in cache;
- no tokens in cache;
- no private keys in cache;
- no executable trust from cache;
- path traversal must be blocked;
- symlink escape must be blocked;
- cross-project data mixing must be blocked;
- cache must be cleanable.

### 7.6 Logs and audit records

Linux:

- `~/.local/state/operre/logs/`

Windows:

- `%LOCALAPPDATA%\Operre\logs\`

macOS:

- `~/Library/Logs/Operre/`

Logs may include:

- application logs;
- crash logs;
- extension audit logs;
- security events;
- AI connector system logs.

## 8. Privacy and telemetry

### 8.1 Default privacy mode

Default privacy mode:

- Strict Privacy

### 8.2 Crash and telemetry defaults

Defaults:

- crash upload: OFF;
- telemetry: OFF;
- diagnostics upload: OFF;
- local safe logs: ON;
- user-reviewed diagnostics export: allowed.

Optional anonymous crash reports may be added later only with explicit opt-in.

### 8.3 Crash report content policy

Acceptable crash report fields, if user explicitly opts in later:

- Operre version;
- OS type;
- OS version;
- CPU architecture;
- Tauri version;
- WebView type/version;
- crash timestamp;
- crash module;
- error code;
- stack trace;
- extension id/version if extension-related.

Must not be uploaded by default:

- source code;
- document contents;
- clipboard contents;
- full file paths;
- user name;
- home directory path;
- GitHub token;
- SSH key;
- `.env` content;
- API key;
- project name;
- repo URL;
- commit message;
- terminal command history.

### 8.4 Telemetry policy

Telemetry is more sensitive than crash reports.

Default:

- no telemetry.

If telemetry is ever added, it must be opt-in and must avoid:

- opened file names;
- project names;
- document contents;
- source code;
- typed words;
- repo URLs;
- GitHub account data;
- full paths;
- extension-specific sensitive usage.

### 8.5 User privacy levels

Possible future privacy levels:

Level 0: Strict Privacy

- no crash upload;
- no telemetry;
- no diagnostics upload;
- local logs only.

Level 1: Anonymous Crash Reports

- technical crash data only;
- no file content;
- no source code;
- no full paths;
- no project names;
- no personal data.

Level 2: Extended Diagnostics

- only if explicitly enabled;
- still no file content/source code/secrets.

### 8.6 Local log restrictions

Local logs must not include by default:

- source code;
- document contents;
- secrets;
- tokens;
- private keys;
- clipboard contents;
- full user paths;
- prompt/AI content.

Local logs must be:

- inspectable;
- deletable;
- rotatable;
- safe by default.

### 8.7 Extension telemetry

Extension telemetry is denied by default.

Any extension telemetry requires separate explicit user permission.

An extension must clearly show:

- destination;
- data categories;
- frequency;
- reason.

## 9. Architecture categories

Do not use "module" as the main product category.

Use:

- Core;
- Built-in Features;
- Extensions;
- Connectors;
- Services.

The word "module" may be used internally in code, but not as the main product/marketplace category.

### 9.1 Core

Core is the minimum safe application foundation.

Core includes:

- app shell;
- file open/save foundation;
- text editor foundation;
- workspace path handling;
- settings loader;
- safe logging;
- extension runtime foundation;
- permission manager.

### 9.2 Built-in Features

Built-in features are included by default but are not core internals.

Examples:

- `.txt` editing;
- Markdown edit/preview;
- syntax highlighting;
- folder/project tree;
- search/replace;
- theme switching;
- default language modes;
- minimap.

### 9.3 Extensions

Extensions are installable/enableable feature packages.

Examples:

- Git;
- TODO list;
- Work plan;
- Service plan;
- Diagrams;
- CAD later;
- AI later;
- advanced language tooling later.

### 9.4 Connectors

Connectors are extensions that connect Operre to external services or ecosystems.

Examples:

- GitHub connector;
- Ideboard connector;
- local sync connector;
- WebDAV connector;
- cloud/self-hosted sync connector;
- future GitLab connector.

### 9.5 Services

Services are Operre-side online services.

Examples:

- extension marketplace;
- update service;
- license service;
- account service;
- optional sync service later.

Services must not be required for local core usage.

## 10. Ideboard, Git, and GitHub

### 10.1 Ideboard

Ideboard:

- separate project;
- separate application;
- future meeting/collaboration environment;
- not Operre core;
- optional Connector Extension later;
- default not enabled;
- not required.

### 10.2 Git

Git:

- optional Extension;
- not core;
- local source-control tooling.

### 10.3 GitHub

GitHub:

- optional Connector Extension;
- not core;
- external service connector.

Git and GitHub must be separated.

Possible future GitHub support:

- login;
- repo list;
- clone;
- push/pull;
- issue/PR later.

## 11. Extension system

### 11.1 Design inspiration

Operre extension system is inspired by VS Code but stricter.

It should be practical like VS Code, but security must be tighter.

### 11.2 Default permission rule

Default:

- deny all permissions.

### 11.3 Extension manifest requirements

Every extension must declare:

- id;
- name;
- publisher;
- version;
- extensionType;
- activationEvents;
- contributes;
- capabilities;
- permissions;
- languageScopes;
- connector scopes if applicable.

Possible manifest file name:

- operre-extension.json

### 11.4 Activation events

Extensions should lazy-load through activation events.

Possible activation events:

- onStartup;
- onFileOpen pattern;
- onLanguage;
- onCommand;
- onWorkspaceOpen;
- onConnectorLogin;
- onDiagramOpen;
- onSettingChanged.

Rule:

- no extension should load unnecessarily.

### 11.5 Contributions

Extensions should contribute through controlled contribution points.

Possible contribution points:

- commands;
- menus;
- views;
- languages;
- themes;
- keybindings;
- status bar items;
- webviews;
- connectors.

Extensions must not arbitrarily modify UI outside approved contribution points.

### 11.6 Permission approval

User approval is required for:

- network access;
- process execution;
- credentials;
- diagnostics sending;
- workspace-wide file access;
- connector access;
- Git operations;
- AI agent operations;
- external toolchain operations.

### 11.7 Permission groups

Initial permission groups may include:

- files.read;
- files.write;
- workspace.metadata;
- network.access;
- network.domain;
- process.run;
- process.run.git;
- process.run.compiler;
- credentials.read;
- credentials.write;
- git.access;
- github.access;
- ideboard.access;
- diagnostics.send;
- clipboard.read;
- clipboard.write;
- shell.open;
- webview.render.

### 11.8 Workspace Trust

Workspace Trust controls:

- build actions;
- debug actions;
- process execution;
- external tools;
- connector sync;
- AI agent access;
- workspace-wide operations.

Unknown or downloaded workspaces should default to restricted behavior.

Possible modes:

- Trusted;
- Restricted;
- Read-only Review Mode.

### 11.9 Publisher Trust

Publisher trust levels may include:

- Operre verified;
- community;
- unknown;
- blocked.

Unknown publisher extensions should have restricted permissions by default.

### 11.10 Language scope rule

Language-specific features must not pollute other file types.

Examples:

- PHP files must not expose C++-specific commands.
- C++ files must not expose PHP-specific commands.
- SQL files must not expose Java-specific commands.

Command visibility rule:

- active language + workspace trust + permission + extension enabled.

### 11.11 Webview security

Extension webviews must be:

- sandboxed;
- CSP controlled;
- message-schema validated;
- blocked from direct system access;
- blocked from network by default;
- blocked from arbitrary local file access.

### 11.12 Secret storage

Operre needs a Secret Vault model.

Rules:

- no plaintext token files;
- OS keychain integration later;
- extension-scoped secrets;
- GitHub token visible only to GitHub Connector;
- Ideboard token visible only to Ideboard Connector;
- no sync by default for secrets.

### 11.13 Marketplace-ready planning

Even if the first extension foundation is small, it must be designed for a future marketplace.

Future marketplace requirements:

- package signing;
- malware scanning;
- static analysis;
- permission review;
- publisher verification;
- update integrity checks;
- rollback support;
- license metadata.

## 12. AI agent connectors

### 12.1 AI agent category

AI agents are optional Connector Extensions.

Examples:

- Codex-like connector;
- Claude-like connector;
- local LLM connector;
- custom API connector;
- self-hosted agent connector.

### 12.2 AI default restrictions

AI agents cannot by default:

- read the full workspace;
- edit files;
- run commands;
- access Git;
- access terminal;
- access secrets;
- send data to network destinations;
- push;
- commit.

### 12.3 AI allowed access

AI agents may access only:

- selected files;
- selected folders;
- selected project context;

and only after explicit scoped permission.

### 12.4 AI edit rule

All AI-made edits must be shown as diff before apply.

AI must not silently change anything.

### 12.5 AI audit logging

Every AI agent action must be logged one by one.

Log fields should include:

- timestamp;
- agent/connector id;
- model/provider;
- requested action;
- granted permissions;
- selected files/folders;
- read operations;
- proposed edits;
- diff before apply;
- user approval/rejection;
- executed commands if any;
- Git actions if any;
- network destinations if any;
- errors/warnings.

### 12.6 AI prompt/response logging

Prompt/response logging:

- default: OFF;
- optional: ON per project/per agent;
- preferred mode: redacted;
- full mode: explicit warning required.

Reason:

- prompt/response may contain source code, secrets, or private information.

### 12.7 AI log storage

Project-related AI actions:

- `~/Operre/Works/Projects/<project>/.operre/audit/ai-agents/`

Global AI connector/system logs:

Linux:

- `~/.local/state/operre/logs/ai-agents/`

Windows:

- `%LOCALAPPDATA%\Operre\logs\ai-agents\`

macOS:

- `~/Library/Logs/Operre/ai-agents/`

### 12.8 AI audit format

Preferred format:

- JSON Lines for event logs;
- `.diff` files for proposed edits;
- optional redacted prompt/response Markdown if user enables it.

AI agent should not write arbitrary audit logs directly.

Rule:

- AI logs must go through Operre Core Audit API.

## 13. Project-local metadata

### 13.1 `.operre/` hybrid Git model

Default:

- `.operre/` ignored by Git.

Optional tracked:

- `.operre/shared/`

Always ignored:

- `.operre/audit/`;
- `.operre/secrets/`;
- `.operre/cache/`;
- `.operre/local-state/`;
- `.operre/snapshots/`.

AI audit logs and prompt/response logs are Git-ignored by default.

### 13.2 Rationale

This protects:

- personal paths;
- local state;
- AI logs;
- prompts;
- snapshots;
- secrets;
- cache data.

Shared safe metadata may be placed under `.operre/shared/` only if explicitly desired.

## 14. Core application scope

### 14.1 Initial free core

Initial free core includes:

- `.txt` open/edit/save;
- Markdown write/edit/preview;
- basic code editing;
- syntax highlighting;
- file open/save;
- folder/project tree;
- lightweight settings;
- extension foundation.

### 14.2 Default built-in usefulness

Operre must be useful immediately after installation.

Default built-in support must cover enough basic work for:

- text notes;
- Markdown notes/docs;
- web/frontend/backend source files;
- common scripting and programming files;
- configuration files.

### 14.3 Future-ready architecture

First versions are not full IDE/debugger products, but architecture must allow future support for:

- debugger;
- object generation;
- binary generation;
- linking;
- executable creation;
- compiler integration;
- linker integration;
- open-source toolchains;
- build tasks;
- language tooling extensions.

## 15. Basic code editing

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

This is basic editing, not full IDE functionality.

## 16. Default file/language support

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

## 17. Language isolation

One file must have one active primary language mode.

Controlled embedded cases may exist:

- HTML with CSS/JS blocks;
- PHP with HTML/PHP blocks;
- Markdown with fenced code blocks.

Even in embedded cases, language behavior must be scoped and safe.

## 18. File open/save behavior

Initial file behavior:

- new file;
- open file;
- save;
- save as;
- reopen recent files;
- dirty/unsaved indicator;
- overwrite warning;
- external file changed warning;
- encoding handling;
- newline handling.

## 19. Startup screen

Startup screen should show:

- recent files/projects;
- restore previous session / reopen open files;
- new text file;
- new Markdown note;
- open file;
- open folder/project;
- Operre Works shortcut.

## 20. Session restore

Session restore:

- default: ON;
- user can disable it.

Saved:

- open files;
- open folder/project;
- active tab;
- cursor position;
- scroll position;
- split/panel layout.

Not saved:

- file contents;
- clipboard;
- secrets/tokens;
- prompt/AI content.

## 21. Autosave

Autosave:

- default: OFF.

Possible later options:

- OFF;
- after delay;
- on focus lost;
- prompt on window close.

Default behavior:

- user controls saving;
- Operre does not silently overwrite user files.

## 22. Dirty/unsaved behavior

Rules:

- dirty tab indicator: `*`;
- close warning;
- choices: Save / Don't Save / Cancel;
- local recovery snapshot may exist for crash recovery.

## 23. Crash recovery

Crash recovery:

- default: ON;
- local-only;
- cloud-disabled;
- user-configurable.

Crash recovery must not conflict with normal session restore.

Opening order:

1. If crash recovery exists, show recovery screen.
2. User chooses Recover / Discard / Compare if possible.
3. After recovery decision, normal session restore may run.
4. If no recovery exists, normal startup flow runs.

Crash recovery must never silently overwrite files.

Retention:

- default: 7 days;
- options: 1 day, 7 days, 30 days, manual only.

## 24. Encoding and BOM

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

## 25. Line endings

Policy:

- new files default: LF on all platforms, including Windows;
- existing files: preserve;
- user conversion: LF / CRLF;
- mixed line endings: warning;
- status bar: show LF/CRLF.

Always-LF new files are preferred for cross-platform consistency.

## 26. Indentation

Policy:

- default: language-aware;
- default insert: spaces;
- existing files: detect and preserve;
- user conversion: tabs <-> spaces;
- mixed indentation: warning;
- status bar: show current indentation.

Examples:

- web/Markdown/JSON/YAML: usually 2 spaces;
- Python/C/C++/Java/PHP: usually 4 spaces.

## 27. Themes

Default theme:

- System.

Built-in options:

- System;
- Light;
- Dark;
- Gray background / neutral gray;
- High contrast.

User can change theme anytime.

User preference note:

- do not assume dark mode preference.

## 28. Font policy

Default editor font:

- system monospace.

Reason:

- avoid bundled proprietary font licensing problems.

User options:

- font family;
- font size;
- line height;
- ligatures on/off.

## 29. Tabs

Tab system:

- multiple tabs supported;
- dirty tab indicator: `*`;
- close tab button;
- reopen closed tab;
- pin tab later;
- tab restore through session restore.

## 30. Split editor

Split editor:

- first version: side-by-side vertical split;
- horizontal split later;
- session restore remembers split layout.

## 31. Markdown support

### 31.1 Markdown behavior

When `.md` opens:

- default: edit mode.

User can switch to:

- preview only;
- side-by-side edit + preview;
- live preview toggle.

Users can create their own `.md` files.

### 31.2 Markdown licensing

Markdown files created by users belong to users.

Markdown format support is acceptable, but parser/renderer dependencies must be license-audited before implementation.

Rules:

- prefer permissive dependencies;
- preserve required license notices;
- add a third-party notices mechanism later;
- verify official dependency license sources before implementation.

### 31.3 Markdown preview security

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

## 32. Minimap

Minimap:

- default: ON;
- position: right.

Settings:

- on/off;
- left/right;
- width small/medium/large;
- adaptive tablet/phone/small-screen behavior.

## 33. Status Bar

Status Bar:

- bottom bar;
- file type;
- encoding;
- BOM yes/no;
- LF/CRLF;
- Spaces/Tabs;
- cursor position: Ln, Col;
- dirty/saved state;
- workspace trust status;
- extension warnings.

## 34. Command Palette

Command Palette shortcut:

- Ctrl+Shift+P

Initial commands:

- New Text File;
- New Markdown Note;
- Open File;
- Open Folder;
- Save;
- Save As;
- Toggle Markdown Preview;
- Toggle Minimap;
- Change Theme;
- Convert Line Endings;
- Convert Indentation;
- Manage Extensions.

## 35. Keyboard shortcuts

Keyboard shortcuts must be configurable.

Defaults:

- Ctrl+N: New File;
- Ctrl+O: Open File;
- Ctrl+S: Save;
- Ctrl+Shift+S: Save As;
- Ctrl+W: Close Tab;
- Ctrl+Shift+T: Reopen Closed Tab;
- Ctrl+F: Find;
- Ctrl+H: Replace;
- Ctrl+Shift+P: Command Palette.

Users can customize through:

- keybindings.json.

macOS should later use platform-native Cmd conventions where appropriate.

## 36. Menu system

Initial classic desktop menu:

- File;
- Edit;
- View;
- Go;
- Tools;
- Extensions;
- Help.

## 37. Activity Bar / Sidebar

Left Activity Bar / Sidebar:

- Explorer;
- Search;
- Recent;
- Extensions;
- Settings.

Later icons appear only through installed/enabled extensions/connectors:

- Git;
- GitHub;
- Ideboard.

## 38. Explorer / folder tree

Explorer first version:

- opened folder/project;
- files and folders;
- create file;
- create folder;
- rename;
- delete with confirmation;
- reveal in file manager;
- refresh.

Security:

- default scope = only user-opened folder/project.

## 39. Delete behavior

Delete behavior:

- default delete moves item to OS Trash/Recycle Bin;
- permanent delete is a separate command;
- every delete operation requires confirmation;
- folder delete requires extra warning.

Detailed permanent delete UI and OS Trash/Recycle Bin implementation remain open for further discussion.

## 40. Search and Recent

Accepted initial Activity Bar entries include Search and Recent.

Details still open:

- search in current file;
- search in opened folder/project;
- replace in files;
- ignore patterns;
- hidden files;
- binary file handling;
- recent files;
- recent folders;
- recent projects;
- privacy-safe recent history.

## 41. Sync strategy

Operre may need servers for:

- app operation;
- extension system;
- extension marketplace/distribution;
- licensing;
- updates;
- account services.

But user-created work data should be local-first by default.

Examples:

- TODO lists;
- work plans;
- service plans;
- notes;
- project docs;
- personal boards;
- local project metadata.

Sync is allowed, but:

- explicit;
- configurable;
- extension/data-domain level;
- not mandatory core cloud dependency.

All Operre apps across environments should eventually be able to sync, but exact details remain future design work.

User-owned sync is important:

- user devices;
- user storage;
- self-hosted storage;
- chosen ecosystem;
- no mandatory upload to Operre servers.

## 42. Drawing, diagrams, and CAD

Drawing and diagram features are part of the broader product direction, but not first implementation priority.

Diagrams and CAD must remain separate categories.

Diagrams may later support:

- free canvas;
- flowcharts;
- architecture diagrams;
- mind maps;
- entity diagrams;
- sequence diagrams;
- SVG/PNG/JSON export.

CAD comes later and must not be mixed with basic diagram features.

Default workspace reflects this separation:

- Diagrams/
- Cad/

## 43. TODO list, work plan, and service plan extensions

Future extensions may include:

- TODO list;
- work plan;
- service plan;
- project planning;
- project notes;
- decision records;
- risk lists.

These are not first core implementation details.

They should be local-first by default and syncable later through explicit extension-level sync.

## 44. Git/GitHub strategy

Git and GitHub are not core.

Git:

- optional Extension.

GitHub:

- optional Connector Extension.

GitHub support may include later:

- GitHub login;
- repo clone;
- push/pull;
- repo list;
- issue/PR later.

Git and GitHub must be separated.

## 45. Ideboard strategy

Ideboard is separate.

Ideboard is not core.

Ideboard may later be:

- optional Connector Extension.

Ideboard is also a future meeting/collaboration project.

## 46. Security baseline

Core security rules:

- no secrets in repository;
- no tokens in repository;
- no private keys in repository;
- no `.env` commit;
- no forced cloud dependency;
- no auto-running extensions;
- no unsafe extension permissions;
- no hidden Ideboard dependency;
- no GitHub dependency in core;
- no silent AI actions;
- no silent file writes;
- no silent network upload;
- no silent command execution;
- no source code upload without explicit permission;
- no prompt/response logging without explicit enablement.

## 47. Dependency and license policy

Operre is not open source, but it may use open-source dependencies if licenses allow it.

Rules:

- perform license audit before adding dependencies;
- preserve required copyright notices;
- maintain third-party notices later;
- avoid proprietary bundled fonts by default;
- avoid unclear license dependencies;
- verify official source/license at implementation time.

Known planning stance:

- Monaco Editor is a strong candidate;
- Markdown parser/renderer must be audited before selection;
- wrapper packages must be audited separately;
- extension marketplace packages must include license metadata later.

## 48. Repository file strategy

Current root documents:

- README.md;
- specifications.md;
- TODO.md;
- .gitignore.

During specification phase:

- specifications.md is the main source of product truth;
- TODO.md stays planning-level and must not prematurely become implementation queue;
- implementation TODOs begin after specification baseline is stable.

Future document split may include:

- docs/repository-discipline.md;
- docs/security-baseline.md;
- docs/architecture.md;
- docs/extension-system.md;
- docs/ai-agent-security.md;
- docs/ui-ux.md;
- docs/storage-paths.md;
- docs/license-policy.md.

## 49. Definition of done for documentation changes

A documentation change is done only when:

- the accepted decision is written;
- related security rule is written if applicable;
- related path rule is written if applicable;
- TODO status is updated if applicable;
- git diff is reviewed;
- commit is pushed;
- post-push audit is clean.

## 50. Research baseline: VS Code, Cursor, and Monaco

### 50.1 VS Code architecture reference

VS Code is an important architectural reference, but Operre must not become a VS Code clone.

Useful VS Code-inspired ideas:

- Electron-style cross-platform workbench concept;
- Monaco Editor as the editor engine;
- custom TypeScript workbench/UI concept;
- Activity Bar;
- Sidebar;
- Explorer;
- tabs;
- split editor;
- status bar;
- command palette;
- extension manifest;
- activation events;
- contribution points;
- extension host separation;
- language-scoped activation;
- Workspace Trust;
- webviews;
- secret storage.

Important distinction:

- Monaco is only the editor engine.
- VS Code Workbench is a much larger platform.
- Operre must design its own workbench, extension model, permission system, and security model.

### 50.2 Cursor architecture reference

Cursor is useful as an AI-first reference but not as Operre's product model.

Cursor is understood as:

- VS Code / Code-OSS fork base;
- Electron/Chromium desktop lineage;
- Monaco/VS Code editor-core lineage;
- VS Code extension compatibility direction;
- additional proprietary AI layer;
- AI chat/composer;
- inline AI editing;
- codebase indexing;
- cloud/local agent workflows;
- backend-mediated AI request flow.

Operre must not copy Cursor's cloud-first AI assumptions.

Operre AI direction:

- AI is optional;
- AI is a Connector Extension;
- full workspace access is denied by default;
- all reads, writes, command execution, network calls, Git actions, and proposed edits require scoped permission;
- all AI edits require diff before apply;
- all AI actions must be auditable.

### 50.3 Monaco license and usage policy

Monaco Editor is accepted as the preferred editor engine candidate.

Planning assumption:

- Monaco Editor is open source;
- Monaco Editor uses a permissive license suitable for commercial/proprietary usage when notices are preserved.

Implementation rule:

- verify the official Monaco package license before dependency addition;
- preserve required copyright/license notices;
- audit wrapper packages separately;
- do not assume Monaco includes the VS Code extension system;
- do not use VS Code or Microsoft branding.

### 50.4 Why not full VS Code/Cursor clone

Operre must stay smaller.

Accepted positioning:

- VS Code is code-centered.
- Cursor is AI-coding-centered.
- Operre is lightweight workspace/editor-centered, local-first, privacy-first, and extension-driven.

Operre should learn from VS Code usability, but use stricter privacy and permission rules.

## 51. Detailed technology decision notes

### 51.1 Frontend framework decision

Accepted primary frontend stack:

- TypeScript;
- Vite;
- Solid.

Fallback:

- TypeScript;
- Vite;
- React.

Not first choice:

- Svelte.

Reasoning:

- Solid is preferred for lightweight UI and fine-grained reactivity.
- React remains a fallback because its ecosystem is large.
- Svelte is considered good but not the first choice for this project direction.

### 51.2 Package manager decision

Accepted package manager:

- pnpm.

Reasoning:

- better fit for monorepo/workspace structure;
- better disk efficiency through shared store model;
- stricter dependency discipline;
- good fit for apps/packages/extensions layout;
- better match for future extension-based architecture.

Repository rule:

- use pnpm only;
- commit pnpm-lock.yaml when implementation begins;
- use pnpm-workspace.yaml when workspace structure begins;
- packageManager field should pin pnpm version later;
- do not commit package-lock.json;
- do not commit yarn.lock;
- do not commit bun.lockb.

Future CI rule:

- pnpm install --frozen-lockfile.

### 51.3 Desktop framework decision

Accepted primary desktop framework:

- Tauri.

Fallback:

- Electron.

Reasoning for Tauri:

- lightweight product goal;
- smaller package direction;
- lower RAM target;
- Rust-native command layer;
- stronger fit with explicit permissions/capabilities;
- future Android/iOS path stays open;
- better match for privacy-first, local-first architecture.

Reasoning for Electron fallback:

- proven desktop maturity;
- more predictable Chromium runtime;
- strong Node.js ecosystem;
- easier VS Code-like extension/tooling patterns;
- fallback if Tauri + Monaco + platform WebView behavior creates unacceptable limitations.

Implementation rule:

- start with Tauri;
- keep Electron fallback documented;
- test Tauri + Solid + Monaco early on Linux;
- later test Windows and macOS;
- do not assume Tauri solves mobile ergonomics automatically.

### 51.4 Web-first idea status

Earlier planning considered web-first direction because Ideboard is web-oriented.

Final Operre direction is different:

- Operre is primarily a lightweight desktop application first;
- web technologies still power the UI;
- Tauri is the primary desktop shell;
- future web or mobile shells may exist later;
- Ideboard remains a separate project.

## 52. Earlier drawing, diagram, and project-board ideas

### 52.1 Accepted broad direction

Operre may eventually include or support:

- drawing;
- diagrams;
- project boards;
- TODO lists;
- work plans;
- service plans;
- documentation;
- Git/GitHub workflows;
- AI-assisted workflows.

But these must not bloat the first core.

### 52.2 Diagram ideas

Future diagram capabilities may include:

- free canvas;
- boxes/arrows;
- flowcharts;
- architecture diagrams;
- mind maps;
- entity diagrams;
- sequence diagrams;
- SVG export;
- PNG export;
- JSON document model.

### 52.3 CAD separation

CAD is future work.

Rule:

- CAD must stay separate from diagrams.
- CAD must not be part of first core.
- Default workspace keeps `Diagrams/` and `Cad/` separate.

### 52.4 Project board idea status

Earlier combined-product ideas included:

- ideas;
- tasks;
- decisions;
- risks;
- docs;
- Git;
- code;
- diagrams.

Final current rule:

- these may become extensions or future built-in features;
- not first implementation target;
- TODO/work plan/service plan are later extension/data-domain topics.

## 53. Repo discipline details to split later

Current root documents are acceptable for the specification phase.

Later, after the specification baseline is stable, split documentation into focused files.

Candidate future docs:

- docs/README.md
- docs/repository-discipline.md
- docs/product-principles.md
- docs/security-baseline.md
- docs/privacy-policy-draft.md
- docs/architecture.md
- docs/technology-decisions.md
- docs/extension-system.md
- docs/extension-security.md
- docs/ai-agent-security.md
- docs/storage-paths.md
- docs/ui-ux.md
- docs/markdown-security.md
- docs/sync-strategy.md
- docs/license-policy.md
- docs/implementation-plan.md

During the specification phase, specifications.md remains the single consolidated source of truth.

## 54. First implementation shape draft

Implementation must not start yet, but the likely future shape is:

- apps/desktop/
- packages/editor-core/
- packages/workbench-core/
- packages/ui/
- packages/file-core/
- packages/settings-core/
- packages/security-core/
- packages/extension-api/
- packages/markdown-core/
- packages/logging-core/
- docs/
- extensions/ later

This is not yet final.

Rules:

- do not create application scaffolding until specification and first implementation TODO are approved;
- keep first implementation minimal;
- no premature marketplace;
- no premature AI;
- no premature GitHub;
- no premature Ideboard;
- no premature CAD.

## 55. Implementation restraint rules

Operre must not start too large.

First implementation target should not include:

- full IDE;
- debugger;
- terminal;
- marketplace;
- AI agent;
- GitHub connector;
- Ideboard connector;
- CAD;
- cloud sync;
- collaboration;
- remote workspace.

First implementation should likely focus on:

- Tauri shell;
- Solid/Vite UI;
- Monaco editor display;
- create/open/save text file;
- basic Markdown editing;
- basic layout;
- status bar skeleton;
- settings foundation;
- no unsafe extension execution.

## 56. Specification consolidation status

Current specification has consolidated decisions through:

- project identity;
- domain/name meaning;
- open-source/source model;
- LogisticSearch parallelism;
- Ideboard separation;
- technology direction;
- platform order;
- storage paths;
- privacy/telemetry;
- extension terminology;
- VS Code-like but stricter extension model;
- AI agent security/audit model;
- `.operre/` hybrid Git model;
- default workspace structure;
- startup/session/autosave/crash recovery;
- encoding/BOM;
- line endings;
- indentation;
- themes/fonts;
- tabs/split editor;
- Markdown preview/security;
- minimap/status bar;
- command palette;
- keyboard shortcuts;
- menu system;
- Activity Bar/Sidebar;
- Explorer/folder tree;
- delete behavior baseline.

Next discussion continues after delete behavior.

## 57. Open decisions / future topics

Topics still to decide after delete behavior:

- detailed permanent delete UI;
- exact OS Trash/Recycle Bin implementation;
- search behavior;
- recent files/projects behavior;
- settings UI;
- settings schema;
- extension manifest schema;
- extension permission UI;
- workspace trust UI;
- extension marketplace design;
- Git extension scope;
- GitHub connector permissions;
- Ideboard connector permissions;
- sync connector model;
- TODO/workplan/service-plan extension model;
- build/debug/toolchain extension model;
- AI connector API;
- installer/update strategy;
- Tauri project layout;
- desktop app packaging strategy;
- legal/license document for non-open-source freeware core;
- public/private repository split strategy;
- first implementation milestone after specification freeze.

## 58. Structured documentation split

The consolidated specification remains the source of truth during the specification phase, but accepted decisions are also split into topic-focused documents under `docs/`.

Structured docs:

- `docs/OPERRE_PRODUCT_PRINCIPLES.md`
- `docs/OPERRE_REPOSITORY_DISCIPLINE.md`
- `docs/OPERRE_TECHNOLOGY_DECISIONS.md`
- `docs/OPERRE_EXTENSION_SECURITY_MODEL.md`
- `docs/OPERRE_AI_AGENT_SECURITY.md`
- `docs/OPERRE_UI_UX_SPECIFICATION.md`
- `docs/OPERRE_STORAGE_PRIVACY_SYNC.md`
- `docs/OPERRE_MARKDOWN_AND_EDITOR_BEHAVIOR.md`
- `docs/OPERRE_FUTURE_FEATURES_AND_RESTRAINTS.md`
- `docs/OPERRE_DECISION_LOG.md`

## 59. Source review: 1.odt

`docs/source-reviews/OPERRE_SOURCE_REVIEW_1_ODT.md` records the first source-file review from the uploaded five-part ODT transcript.

It covers:

- VS Code architecture reference;
- Cursor architecture and AI/privacy lessons;
- Monaco Editor distinction from full VS Code;
- Monaco license planning rules;
- early Operre editor/workspace direction;
- early drawing/diagram/project-board ideas;
- initial restraint rules for first implementation.

Processing status:

- 1.odt: processed into repository memory.
- 2.odt: pending dedicated review.
- 3.odt: pending dedicated review.
- 4.odt: pending dedicated review.
- 5.odt: pending dedicated review.
