# Operre Source Review: 3.odt

This document records decisions and useful planning extracted from `3.odt`.

Source position:

- file: `3.odt`
- processing order: 3 / 5
- topic range: storage/log paths, privacy/telemetry, extension terminology, VS Code-like extension system, explicit permission model, Workspace Trust, Publisher Trust, webviews, secret vault, AI agent connector model, AI logging, prompt/response logging, `.operre/` hybrid Git model, workspace folder structure.

## 1. Logs and audit paths

Accepted global log/audit paths:

Linux:

- `~/.local/state/operre/logs/`

Windows:

- `%LOCALAPPDATA%\Operre\logs\`

macOS:

- `~/Library/Logs/Operre/`

These paths may hold:

- app logs;
- crash logs;
- extension audit logs;
- security events;
- global AI connector/system logs.

## 2. Crash report and telemetry policy

Accepted default privacy mode:

- Strict Privacy.

Defaults:

- crash upload: OFF;
- telemetry: OFF;
- diagnostics upload: OFF;
- local safe logs: ON;
- user-reviewed diagnostics export: allowed.

Crash reports and telemetry are separate concepts.

Crash reports are technical failure diagnostics.

Telemetry is usage/behavior/performance data and is more sensitive.

## 3. Acceptable crash diagnostic fields

If the user explicitly opts in later, acceptable crash diagnostic fields may include:

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

## 4. Forbidden default upload/log content

The following must not be uploaded by default:

- source code;
- `.txt`, `.md`, `.cpp`, `.php`, `.sql`, or other document contents;
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

## 5. Telemetry restrictions

Telemetry is OFF by default.

If telemetry is ever added, it must be opt-in.

Forbidden telemetry examples:

- which files were opened;
- which project was used;
- what the user typed;
- source code;
- words in documents;
- repo URL;
- GitHub account;
- full folder path;
- which extension processed which sensitive file.

## 6. Local logs

Local logs must be safe by default.

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

## 7. Extension telemetry

Extension telemetry is denied by default.

An extension requesting telemetry must explicitly show:

- destination;
- data categories;
- frequency;
- reason.

No extension telemetry is allowed without explicit user permission.

## 8. Product architecture categories

Do not use "module" as the main product category.

Use:

- Core;
- Built-in Features;
- Extensions;
- Connectors;
- Services.

The word "module" may be used internally in source code only, but not as the main product/user category.

## 9. Ideboard, GitHub, and Git classification

Ideboard:

- optional Connector Extension;
- not core;
- not required;
- not enabled by force.

GitHub:

- optional Connector Extension;
- not core;
- external service connector.

Git:

- optional Extension;
- local source-control tooling.

Git and GitHub must be separated.

## 10. VS Code-like but stricter extension system

Accepted direction:

- Operre extension system is inspired by VS Code but stricter.
- Operre should remain practical like VS Code.
- Operre security must be tighter than VS Code.
- Default permission is deny all.
- Extensions must declare explicit permissions.
- Sensitive actions require explicit user approval.

Operre should take from VS Code:

- extension manifest;
- activation events;
- contribution points;
- extension host;
- workspace trust;
- extension kind/location concept;
- webview model;
- secret storage;
- marketplace metadata;
- lazy loading;
- language-scoped activation.

Operre should change from VS Code:

- permission model;
- telemetry;
- network access;
- process execution;
- file access scope;
- publisher trust;
- extension webview security.

Operre should not take:

- extension host with the same broad permission as the app;
- broad file/network/process access by default;
- easy telemetry enablement;
- vague permission prompts.

## 11. Extension manifest

Possible manifest file name:

- `operre-extension.json`

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

## 12. Extension host model

VS Code has local/web/remote extension hosts.

Operre may later support separated hosts such as:

- ui-extension-host;
- workspace-extension-host;
- connector-extension-host.

First version may use a simpler host, but architecture must be ready for stronger isolation.

## 13. Activation events

Extensions should lazy-load.

Possible activation events:

- onStartup;
- onFileOpen pattern;
- onFileOpen:*.md;
- onFileOpen:*.cpp;
- onLanguage;
- onLanguage:markdown;
- onCommand;
- onCommand:git.status;
- onWorkspaceOpen;
- onConnectorLogin;
- onConnectorLogin:github;
- onDiagramOpen;
- onSettingChanged.

Rule:

- no extension should load unnecessarily.

## 14. Contribution points

Extensions must contribute through controlled contribution points.

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

Extensions must not arbitrarily modify the UI outside approved contribution points.

## 15. Extension types

Possible extension types:

- feature-extension;
- connector-extension;
- language-extension;
- theme-extension;
- toolchain-extension;
- renderer-extension;
- service-extension.

Examples:

- Git = feature-extension;
- GitHub = connector-extension;
- Ideboard = connector-extension;
- C++ tools = language/toolchain-extension;
- Markdown = built-in feature, later extendable;
- Diagrams = renderer-extension.

## 16. Permission groups

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

Default:

- deny all.

## 17. Workspace Trust

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

## 18. Publisher Trust

Publisher trust levels may include:

- Operre verified;
- community;
- unknown;
- blocked.

Unknown publisher extensions should have restricted permissions by default.

## 19. Language/file scope rule

Language-specific features must not pollute other file types.

Examples:

- PHP files must not expose C++-specific commands.
- C++ files must not expose PHP-specific commands.
- SQL files must not expose Java-specific commands.

Command visibility rule:

- active language + workspace trust + permission + extension enabled.

Example:

C++ build command appears only if:

- active file is C/C++ related;
- C++ tooling extension is enabled;
- workspace is trusted;
- compiler/process permission is granted.

## 20. Webview security

Extension webviews must be:

- sandboxed;
- CSP controlled;
- message-schema validated;
- blocked from direct system access;
- blocked from network by default;
- blocked from arbitrary local file access.

Webview use cases may include:

- Markdown preview;
- diagrams;
- TODO panels;
- Ideboard connector panels;
- extension-specific UIs.

## 21. Secret Vault

Operre needs a Secret Vault model.

Rules:

- no plaintext token files;
- OS keychain integration later;
- Tauri/Rust secure storage adapter later;
- extension-scoped secrets;
- GitHub token visible only to GitHub Connector;
- Ideboard token visible only to Ideboard Connector;
- no sync by default for secrets.

## 22. Marketplace-ready planning

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

## 23. AI agent connector model

AI agents are optional Connector Extensions.

Examples:

- Codex-like connector;
- Claude-like connector;
- local LLM connector;
- custom API connector;
- self-hosted agent connector.

AI agents are not core.

AI must be possible later, but safe.

## 24. AI default restrictions

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

## 25. AI allowed access

AI agents may access only:

- selected files;
- selected folders;
- selected project context;

and only after explicit scoped permission.

## 26. AI edit rule

All AI-made edits must be shown as diff before apply.

AI must not silently change anything.

AI cannot approve its own diff.

## 27. AI audit logging

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

## 28. AI prompt/response logging

Prompt/response logging:

- default: OFF;
- optional: ON per project/per agent;
- preferred mode: redacted;
- full mode: explicit warning required.

Reason:

- prompt/response may contain source code, secrets, or private information.

## 29. AI log storage

Project-related AI actions:

- `~/Operre/Works/Projects/<project>/.operre/audit/ai-agents/`

Global AI connector/system logs:

Linux:

- `~/.local/state/operre/logs/ai-agents/`

Windows:

- `%LOCALAPPDATA%\Operre\logs\ai-agents\`

macOS:

- `~/Library/Logs/Operre/ai-agents/`

## 30. AI audit format

Preferred format:

- JSON Lines for event logs;
- `.diff` files for proposed edits;
- optional redacted prompt/response Markdown if user enables it.

AI agent should not write arbitrary audit logs directly.

Rule:

- AI logs must go through Operre Core Audit API.

## 31. `.operre/` hybrid Git model

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

## 32. Default workspace structure

Accepted workspace structure:

- `~/Operre/Works/Notes/`
- `~/Operre/Works/Projects/`
- `~/Operre/Works/Diagrams/`
- `~/Operre/Works/Cad/`
- `~/Operre/Works/Exports/`
- `~/Operre/Works/Scratch/`
- `~/Operre/Works/Templates/`

Rules:

- Diagrams and CAD are separate.
- Work data is separate from installed extension code.
- Local/cache/audit/secrets are not mixed with normal user documents.

## 33. 3.odt accepted decisions summary

Accepted decisions extracted from `3.odt`:

- global logs/audit paths accepted;
- default privacy mode is Strict Privacy;
- crash upload, telemetry, diagnostics upload are OFF by default;
- local safe logs are ON;
- extension telemetry is denied by default;
- main categories are Core, Built-in Features, Extensions, Connectors, Services;
- Ideboard and GitHub are optional Connector Extensions;
- Git is optional Extension;
- extension system is VS Code-like but stricter;
- default extension permission is deny all;
- extension manifest must declare activation/contribution/capability/permission/language scope/type;
- Workspace Trust controls risky actions;
- Publisher Trust is needed;
- language/file-scope must prevent cross-language command pollution;
- extension webviews must be sandboxed;
- Secret Vault is required;
- AI agents are optional Connector Extensions;
- AI access is selected/scope-based only;
- AI edits require diff before apply;
- AI actions must be logged one by one;
- prompt/response logging is OFF by default but can be enabled explicitly;
- `.operre/` uses hybrid Git model;
- `.operre/shared/` may be tracked;
- audit/secrets/cache/local-state/snapshots are always ignored.
