# Operre Extension Security Model

## Product vocabulary

Do not use "module" as the main product category.

Use:

- Core
- Built-in Features
- Extensions
- Connectors
- Services

The word "module" may be used internally in source code, but not as the main user/product category.

## Core

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

## Built-in Features

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

## Extensions

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

## Connectors

Connectors are extensions that connect Operre to external services or ecosystems.

Examples:

- GitHub Connector;
- Ideboard Connector;
- future GitLab Connector;
- local sync connector;
- WebDAV connector;
- cloud/self-hosted sync connector.

## Services

Services are Operre-side online services.

Examples:

- extension marketplace;
- update service;
- license service;
- account service;
- optional sync service later.

Services must not be required for local core usage.

## Ideboard / Git / GitHub classification

Ideboard:

- optional Connector Extension;
- not core;
- not required;
- not enabled by force.

Git:

- optional Extension;
- local source-control tooling.

GitHub:

- optional Connector Extension;
- external service connector.

Git and GitHub must be separated.

## VS Code-like but stricter

Operre extension system is inspired by VS Code but stricter.

Use:

- extension manifest;
- activation events;
- contribution points;
- extension host isolation;
- Workspace Trust;
- Publisher Trust;
- webview sandbox;
- secret vault;
- language/file scoped activation.

Unlike VS Code, Operre extensions must declare explicit permissions.

Default permission:

- deny all.

## Manifest requirements

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

- `operre-extension.json`

## Activation events

Extensions should lazy-load.

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

## Contributions

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

Extensions must not arbitrarily modify UI outside approved contribution points.

## Permission approval

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

## Permission groups

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

## Workspace Trust

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

## Publisher Trust

Publisher trust levels may include:

- Operre verified;
- community;
- unknown;
- blocked.

Unknown publisher extensions should have restricted permissions by default.

## Language scope rule

Language-specific features must not pollute other file types.

Examples:

- PHP files must not expose C++-specific commands.
- C++ files must not expose PHP-specific commands.
- SQL files must not expose Java-specific commands.

Command visibility rule:

- active language + workspace trust + permission + extension enabled.

## Webview security

Extension webviews must be:

- sandboxed;
- CSP controlled;
- message-schema validated;
- blocked from direct system access;
- blocked from network by default;
- blocked from arbitrary local file access.

## Secret storage

Operre needs a Secret Vault model.

Rules:

- no plaintext token files;
- OS keychain integration later;
- extension-scoped secrets;
- GitHub token visible only to GitHub Connector;
- Ideboard token visible only to Ideboard Connector;
- no sync by default for secrets.

## Marketplace-ready planning

Future marketplace requirements:

- package signing;
- malware scanning;
- static analysis;
- permission review;
- publisher verification;
- update integrity checks;
- rollback support;
- license metadata.

## Source 3 extension security baseline

The `3.odt` review confirms the extension security baseline.

Accepted principles:

- VS Code-like usability.
- Stricter-than-VS-Code security.
- Default deny permissions.
- Explicit permission declaration.
- Workspace Trust.
- Publisher Trust.
- Language/file scoped commands.
- Sandboxed webviews.
- Secret Vault.
- Marketplace-ready metadata.

Required manifest fields:

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

Possible extension host direction:

- ui-extension-host;
- workspace-extension-host;
- connector-extension-host.

This may be simplified in the first version, but the architecture must not block future isolation.

## Hidden/protected path extension baseline

Accepted extension behavior:

- Extensions cannot access hidden/protected paths by default.
- Extensions must request explicit permissions for hidden files, workspace metadata, Git metadata, Operre metadata, credentials, secrets, cache, and snapshot areas.
- `.git/` and `.operre/` access must be scoped and auditable.
- Default permission remains deny all.

## Search/compare extension access baseline

Accepted extension behavior:

- Extensions cannot receive search results by default.
- Extensions cannot receive compared file contents by default.
- Extensions require explicit scoped permission to contribute search providers, compare viewers, compare exporters, or external compare integrations.
- Sending search/compare data outside the machine requires separate network permission.

## Large file extension access baseline

Accepted extension behavior:

- Extensions cannot access large file content by default.
- Extensions need explicit permission for reading, indexing, comparing, exporting, or externally sending large file content.
- Large file extension operations must respect memory/cache budgets where practical.

## Recent history extension access baseline

Accepted extension behavior:

- Extensions cannot access recent history by default.
- Extensions require explicit scoped permission for reading, adding, syncing, exporting, or contributing recent-history UI.
- Sending recent history outside the machine requires separate network permission.

## Settings and extension security baseline

Accepted extension behavior:

- Extension settings must be namespaced.
- Extension settings cannot bypass permissions.
- Extension settings cannot grant network, workspace, credential, AI, or Git access by themselves.
- Extension settings are subject to Workspace Trust.
- Extension-provided settings should have schemas where practical.

## Keybindings and extension security baseline

Accepted extension behavior:

- Extensions may contribute commands and shortcuts.
- Extension commands and shortcuts must be namespaced.
- Extension shortcuts cannot silently override core shortcuts.
- Extension shortcuts cannot bypass permissions.
- Disabled extensions have inactive shortcuts.
- Extension uninstall may ask whether to remove related shortcuts/settings.

## Command Palette and extension command baseline

Accepted extension behavior:

- Extensions may contribute commands.
- Extension command IDs must be namespaced.
- Extension commands cannot bypass permissions.
- Extension commands cannot silently gain network, workspace, Git, AI, shell, or credential access.
- Extension command source should be visible where relevant.
- Disabled extensions have unavailable or disabled commands.

## Extension warning and problem baseline

Accepted extension behavior:

- Extension warnings must include permission requests, crashes, slow extensions, trust blocks, blocked network attempts, and blocked protected path access.
- Extension commands must not bypass warning/confirmation policy.
- Extension telemetry remains denied by default.
- Extension access to warning/error history is denied by default.

## Extension logs and diagnostics baseline

Accepted extension behavior:

- Extension logs may include extension ID, version, activation failure, command failure, permission denial, crash/slow warning, and blocked access summary.
- Extension logs must not include user file contents by default.
- Extension secrets must not be logged.
- Extension telemetry remains denied by default.
- Extension access to logs/diagnostics history is denied by default.

## Extension recovery boundary baseline

Accepted extension behavior:

- Extensions cannot access recovery content by default.
- Extensions cannot scan recovery storage by default.
- Extensions cannot export recovery content by default.
- Extension crash reports must not include recovery content by default.
- Extension APIs for recovery content, if ever added, require explicit permission.

## Extension save boundary baseline

Accepted extension behavior:

- Extensions cannot bypass save conflict handling.
- Extensions cannot bypass overwrite confirmations.
- Extensions cannot bypass protected path save warnings.
- Extensions cannot access backup/recovery content by default.
- Extension-triggered saves must report errors clearly.

## Extension watcher boundary baseline

Accepted extension behavior:

- Extensions cannot access watcher event history by default.
- Extension watcher access requires explicit permission later.
- Extension watcher scope must be limited to workspace scope.
- Protected paths are excluded from extension watcher access.
- High-volume watcher abuse must be rate-limited.

## Extension Explorer and navigation boundary baseline

Accepted extension behavior:

- Extensions cannot access Explorer tree by default.
- Extensions cannot access navigation history by default.
- Extension Explorer contributions require permission and Workspace Trust.
- Extension context menu items require permission.
- Extensions cannot bypass dangerous Explorer confirmations.
- Protected paths are excluded by default.

## View contribution and programming language toolchain extension constraints

Extension-contributed views must be explicit contribution points, not arbitrary UI injection. Extension views must declare stable IDs, titles, default locations, required permissions, and restricted states. Extensions cannot read Explorer state, Recent history, Search results, Problems, Logs, Diagnostics, layout state, or protected path indicators unless the permission model grants that exact scope.

Future programming language toolchain/runtime extensions may support compilers, interpreters, simulators, emulators, linkers, executable builders, package builders, live runtime/REPL surfaces, language servers, debuggers, build/test runners, problem matchers, formatters, linters, and language-specific project templates.

These capabilities require Workspace Trust, explicit process execution permissions, environment handling, secrets protection, resource limits, output limits, audit logging, and AI restrictions. They must never become required Operre core dependencies.

## Workbench chrome contribution constraints

Extension-contributed menu items, toolbar items, titlebar items, status bar items, and overflow actions must be declared contribution points. They must be permission-scoped, user-hideable, stable-ID based, and unable to bypass Workspace Trust. Extensions must not shrink core chrome into unusable sizes, leak protected paths, leak secrets, track users through chrome state, or add hidden automation through status items.

Runtime, compiler, interpreter, simulator, emulator, linker, executable builder, AI, Git, Terminal, Run, and Debug chrome must remain later optional extension surfaces with explicit permissions and audit logging.

## Panel contribution and diagnostic access constraints

Extensions may contribute Problems, Output channels, Logs summaries, and Diagnostics summaries only through declared contribution points and permission-scoped APIs. Extensions cannot read Problems, Search Results, Output, Logs, or Diagnostics by default. Open UI does not imply extension data access.

Build output, runtime output, compiler diagnostics, interpreter diagnostics, simulator diagnostics, emulator diagnostics, linker diagnostics, executable builder output, test output, terminal output, and debug output remain later extension or process-execution topics with Workspace Trust, explicit permissions, redaction, and audit logging.

## Extension manifest and runtime security baseline

Operre extensions must be manifest-driven, permission-scoped, and deny-by-default. TypeScript/JavaScript is the core extension control-plane direction. Extension code must run through a sandboxed extension host and must use the Permission Broker to access Operre APIs.

C, C++, Python, JavaScript runtimes outside the sandbox, database tools, web servers, compilers, interpreters, simulators, emulators, linkers, executable builders, package managers, live runtime surfaces, terminal-like tools, and debuggers are not core extension runtime features. They are later desktop/workstation-only brokered integrations requiring Workspace Trust, explicit permissions, resource limits, redaction, and audit logging.

Extensions must not read files, workspace trees, Search Results, Problems, Output, Logs, Diagnostics, secrets, protected paths, AI prompts, AI responses, or environment variables by default.

## Extension permission UI enforcement

Extension permission UI must use install-time summaries and runtime critical prompts. Dangerous permissions require scoped approval, duration choices, risk classification, Workspace Trust checks, and audit logging. Permission UI is not the security boundary by itself; enforcement belongs to the Permission Broker, Extension Host API bridge, Workspace Trust Broker, Device Capability Resolver, Package Verifier, future Process Execution Broker, future Toolchain Broker, and Audit Log.

Extension update policy B is the default: an extension requesting new permissions remains blocked or disabled until user approval. Local and unpacked extensions require Developer Mode. Phone and tablet must show unsupported risky capabilities as disabled with desktop required.

## Workspace Trust relationship

Extensions must respect Workspace Trust. Package verification, manifest permissions, user grants, and Workspace Trust are separate gates. Workspace Trust does not automatically grant extension permissions, and extension permission grants do not replace Workspace Trust. High-risk and very-high-risk extension actions require Workspace Trust where workspace data, process execution, AI access, diagnostics, logs, protected paths, or external tools are involved.

## Safe terminal and process execution relationship

Extensions cannot execute terminal commands directly. Extensions may
contribute commands, tasks, terminal providers, or toolchain profiles
only through declared contribution points and brokered execution. Process
Execution Broker and Toolchain Broker remain the enforcement surfaces.
