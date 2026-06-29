# Operre Specifications

This document records Operre product decisions, architecture decisions, security rules, UX rules, storage rules, and development discipline.

The specification is intentionally detailed. Operre must be disciplined from the beginning.

## 1. Product identity

### 1.1 Name

Product name:

Operre

Domain:

operre.com

### 1.2 Meaning

The domain was originally chosen with operation research in mind.

The name can also be interpreted through:

- operation;
- organize;
- prepare;
- execute;
- repository;
- workspace;
- German "Oper" as a stage/performance metaphor.

Internal interpretation:

Operre is a lightweight place where projects are prepared, organized, and performed.

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
- online sync.

Ideboard may later connect through an optional connector extension.

### 1.5 Source model

Operre is not planned as open source.

Rules:

- the basic/core application may be free;
- future extensions may be free or paid;
- the internal development repository should normally be private;
- a separate public repository may later be created for public distribution or public documentation.

## 2. Project relationship and priority

### 2.1 LogisticSearch relationship

Operre can be developed in parallel with LogisticSearch.

LogisticSearch is a long-running project involving crawler, backend, frontend, infrastructure, and runtime work.

Operre should use a similarly strict repository/audit/TODO/documentation discipline.

### 2.2 Ideboard relationship

Ideboard is a separate project and separate application.

Ideboard may later become:

- a meeting environment;
- a collaboration environment;
- a project/future board platform;
- an optional Operre connector extension.

Ideboard must not be part of Operre core.

## 3. Development discipline

### 3.1 Repository as memory

The GitHub repository is the project memory.

Every meaningful detail must be recorded.

### 3.2 Documentation-first rule

Documentation is mandatory.

Document:

- product ideas;
- product decisions;
- architecture decisions;
- security decisions;
- storage paths;
- user data rules;
- extension rules;
- UI/UX behavior;
- implementation details;
- TODO state changes;
- completed work.

### 3.3 TODO-driven workflow

All work must flow through TODO.

Workflow:

1. Select TODO item.
2. Audit current state.
3. Implement or document.
4. Verify.
5. Update documentation.
6. Update TODO.
7. Review git diff.
8. Commit.
9. Push.
10. Post-push audit.

### 3.4 Language rule

Repository documentation and planning must be English-only.

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
- clear and disciplined.

Core principle:

Core-first, cloud-optional, extension-driven.

## 5. Technology stack

### 5.1 Preferred stack

Preferred stack:

- Tauri;
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

Tauri is preferred because Operre must be lightweight and may later target tablet/mobile environments.

Electron remains a fallback because it is mature and proven for VS Code-like applications, but it is heavier.

Solid is preferred because it is lightweight.

React remains a fallback because of its ecosystem.

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

## 6. Platform order and ergonomics

Initial target order:

1. Linux Desktop
2. Windows Desktop
3. macOS Desktop
4. Tablet/mobile later

Monaco Editor weight is not considered the primary problem for mobile.

The primary mobile/tablet challenge is ergonomics.

Design rule:

Same core. Adaptive ergonomics.

Desktop ergonomics:

- keyboard;
- mouse;
- multi-panel layout;
- split editor;
- folder tree;
- minimap.

Tablet ergonomics:

- touch;
- optional keyboard;
- simplified panel switching;
- adaptive minimap behavior.

Phone ergonomics:

- fast notes;
- small edits;
- preview;
- focused single-file workflows.

## 7. Data and storage paths

### 7.1 User workspace

Default user workspace path must avoid spaces.

Linux/macOS:

~/Operre/Works/

Windows:

%USERPROFILE%\Operre\Works\

### 7.2 Workspace folders

Default user workspace structure:

~/Operre/Works/
  Notes/
  Projects/
  Diagrams/
  Cad/
  Exports/
  Scratch/
  Templates/

Rules:

- Diagrams and Cad must be separate.
- Users may change the default workspace path.
- Users without a formal project can save simple notes into the default workspace or their chosen directory.

### 7.3 Installed extension code

Installed/runnable extension code must be separated from user work data.

Linux:

~/.local/share/operre/extensions/

Windows:

%APPDATA%\Operre\extensions\

macOS:

~/Library/Application Support/Operre/extensions/

### 7.4 Application configuration

Linux:

~/.config/operre/

Windows:

%APPDATA%\Operre\config\

macOS:

~/Library/Application Support/Operre/config/

Example files:

- settings.json;
- keybindings.json;
- workspace-defaults.json;
- extensions-enabled.json.

### 7.5 Cache, temporary, and generated data

Linux:

~/.cache/operre/

Windows:

%LOCALAPPDATA%\Operre\cache\

macOS:

~/Library/Caches/Operre/

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

~/.local/state/operre/logs/

Windows:

%LOCALAPPDATA%\Operre\logs\

macOS:

~/Library/Logs/Operre/

Logs may include:

- application logs;
- crash logs;
- extension audit logs;
- security events.

## 8. Privacy and telemetry

### 8.1 Default privacy mode

Default privacy mode:

Strict Privacy

### 8.2 Crash and telemetry defaults

Defaults:

- crash upload: OFF;
- telemetry: OFF;
- diagnostics upload: OFF;
- local safe logs: ON;
- user-reviewed diagnostics export: allowed.

Optional anonymous crash reports may be added later only with explicit opt-in.

### 8.3 Local log restrictions

Local logs must not include by default:

- source code;
- document contents;
- secrets;
- tokens;
- private keys;
- clipboard contents;
- full user paths;
- prompt/AI content.

### 8.4 Extension telemetry

Extension telemetry is denied by default.

Any extension telemetry requires separate explicit user permission.

## 9. Architecture categories

Do not use "module" as the main product category.

Use:

- Core;
- Built-in Features;
- Extensions;
- Connectors;
- Services.

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

- .txt editing;
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

## 10. Ideboard, Git, and GitHub

### 10.1 Ideboard

Ideboard:

- separate project;
- separate application;
- future meeting/collaboration environment;
- not Operre core;
- optional Connector Extension later.

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

## 11. Extension system

### 11.1 Design inspiration

Operre extension system is inspired by VS Code but stricter.

It should be practical like VS Code, but security must be tighter.

### 11.2 Default permission rule

Default:

deny all permissions

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

### 11.4 Permission approval

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

### 11.5 Workspace Trust

Workspace Trust controls:

- build actions;
- debug actions;
- process execution;
- external tools;
- connector sync;
- AI agent access;
- workspace-wide operations.

Unknown or downloaded workspaces should default to restricted behavior.

### 11.6 Publisher Trust

Publisher trust levels may include:

- Operre verified;
- community;
- unknown;
- blocked.

Unknown publisher extensions should have restricted permissions by default.

### 11.7 Language scope rule

Language-specific features must not pollute other file types.

Examples:

- PHP files must not expose C++-specific commands.
- C++ files must not expose PHP-specific commands.
- SQL files must not expose Java-specific commands.

Command visibility rule:

active language + workspace trust + permission + extension enabled.

### 11.8 Webview security

Extension webviews must be:

- sandboxed;
- CSP controlled;
- message-schema validated;
- blocked from direct system access;
- blocked from network by default;
- blocked from arbitrary local file access.

### 11.9 Marketplace-ready planning

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

### 12.6 Prompt/response logging

Prompt/response logging:

- default: OFF;
- optional: ON per project/per agent;
- preferred mode: redacted;
- full mode: explicit warning required.

Reason:

Prompt/response may contain source code, secrets, or private information.

### 12.7 AI log storage

Project-related AI actions:

~/Operre/Works/Projects/<project>/.operre/audit/ai-agents/

Global AI connector/system logs:

Linux:

~/.local/state/operre/logs/ai-agents/

Windows:

%LOCALAPPDATA%\Operre\logs\ai-agents\

macOS:

~/Library/Logs/Operre/ai-agents/

## 13. Project-local metadata

### 13.1 `.operre/` hybrid Git model

Default:

.operre/ ignored by Git.

Optional tracked:

.operre/shared/

Always ignored:

- .operre/audit/;
- .operre/secrets/;
- .operre/cache/;
- .operre/local-state/;
- .operre/snapshots/.

AI audit logs and prompt/response logs are Git-ignored by default.

## 14. Core application scope

### 14.1 Initial free core

Initial free core includes:

- .txt open/edit/save;
- Markdown write/edit/preview;
- basic code editing;
- syntax highlighting;
- file open/save;
- folder/project tree;
- lightweight settings;
- extension foundation.

### 14.2 Future-ready architecture

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

## 16. Default file/language support

Initial default file support:

- .txt;
- .md;
- .html;
- .css;
- .js;
- .ts;
- .json;
- .sql;
- .c;
- .cpp;
- .h;
- .hpp;
- .java;
- .php;
- .py;
- .sh;
- .xml;
- .yaml;
- .yml.

Purpose:

- open;
- edit;
- save;
- syntax highlighting;
- language-aware basic behavior.

This is not yet full IDE support.

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

- dirty tab indicator: *;
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

UTF-8 without BOM.

Rules:

- UTF-8 with BOM option available;
- preserve existing BOM state by default;
- user can convert with BOM / without BOM;
- risky file types may warn if BOM is added.

Risky examples:

- .sh;
- .py;
- .php;
- .js;
- .json;
- .yaml;
- .env;
- Dockerfile;
- Makefile.

## 25. Line endings

Policy:

- new files default: LF;
- existing files: preserve;
- user conversion: LF / CRLF;
- mixed line endings: warning;
- status bar: show LF/CRLF.

Always-LF new files are preferred for cross-platform consistency, including Windows.

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

System.

Built-in options:

- System;
- Light;
- Dark;
- Gray background / neutral gray;
- High contrast.

User can change theme anytime.

## 28. Font policy

Default editor font:

system monospace.

Reason:

Avoid bundled proprietary font licensing problems.

User options:

- font family;
- font size;
- line height;
- ligatures on/off.

## 29. Tabs

Tab system:

- multiple tabs supported;
- dirty tab indicator: *;
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

When .md opens:

default: edit mode.

User can switch to:

- preview only;
- side-by-side edit + preview;
- live preview toggle.

Users can create their own .md files.

### 31.2 Markdown licensing

Markdown files created by users belong to users.

Markdown parser/renderer dependencies must be license-audited.

Permissive libraries are preferred.

Required license notices must be preserved.

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

Example:

Remote resources were blocked for your safety.
Allow for this file / Allow for this workspace / Settings.

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

Ctrl+Shift+P

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

Users can customize through keybindings.json.

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

Default scope = only user-opened folder/project.

## 39. Delete behavior

Delete behavior:

- default delete moves item to OS Trash/Recycle Bin;
- permanent delete is a separate command;
- every delete operation requires confirmation;
- folder delete requires extra warning.

## 40. Sync strategy

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

## 41. Security baseline

Core security rules:

- no secrets in repository;
- no tokens in repository;
- no private keys in repository;
- no .env commit;
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

## 42. Open decisions / future topics

Topics still to decide:

- exact extension manifest schema;
- exact extension permission UI;
- exact workspace trust UI;
- exact extension marketplace design;
- exact Git extension scope;
- exact GitHub connector permissions;
- exact Ideboard connector permissions;
- exact sync connector model;
- exact TODO/workplan/service-plan extension model;
- exact build/debug/toolchain extension model;
- exact AI connector API;
- exact installer/update strategy;
- exact Tauri project layout;
- exact desktop app packaging strategy;
- exact legal/license document for non-open-source freeware core;
- exact public/private repository split strategy;
- exact search behavior;
- exact recent files/projects behavior;
- exact settings UI;
- exact permanent delete UI;
- exact Trash/Recycle Bin integration implementation.
