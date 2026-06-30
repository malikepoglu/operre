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
