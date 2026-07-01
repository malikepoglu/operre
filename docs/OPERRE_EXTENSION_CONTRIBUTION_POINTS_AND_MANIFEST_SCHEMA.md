# Operre Extension Contribution Points and Manifest Schema

Status: Accepted specification
Topic ID: OPR-SPEC-0038
Scope: Extension architecture, contribution points, manifest schema, extension runtime classes, marketplace bootstrap, local installation, private registry, sync planning, external toolchain control, device limits, and security boundaries.

## 1. Purpose

This document defines Operre's extension contribution model and first manifest schema direction.

Operre should support extensions without turning the core editor into an unsafe, slow, or dependency-heavy platform. The extension system must keep Operre small, fast, privacy-first, and ergonomic while still allowing future growth for language tooling, diagnostics, external runtimes, AI connectors, remote tools, and project-specific integrations.

The extension model must also support future use across Operre-related products and projects, including Ideboard-like integrations or other products that may embed Operre editor capabilities. Therefore the model must be product-family compatible, namespaced, capability-based, and not locked to one narrow application shell.

## 2. Core decision

The core extension model uses:

- declarative manifest;
- TypeScript or JavaScript control plane;
- sandboxed extension host;
- central command registry;
- declared contribution points;
- permission broker;
- audit logging;
- lazy activation;
- package identity and signature verification;
- device-class capability limits;
- optional future WASM support;
- optional future desktop-only external toolchain/runtime brokers.

The core extension system must not use C, C++, Python, native shared libraries, or arbitrary external process execution as the default extension runtime.

C, C++, Python, JavaScript runtimes, database tools, web technology tools, compilers, interpreters, simulators, emulators, linkers, executable builders, live runtime surfaces, package managers, and development servers may exist later as external toolchain or runtime integrations. They must be controlled by Operre through a brokered, permission-scoped, audited, Workspace-Trust-aware model.

Operre should act as a safe coordinator or remote-control surface for license-compatible external tools, not as an uncontrolled in-process native plugin host.

## 3. Design principles

Required principles:

- core stays small;
- default deny;
- no implicit file access;
- no implicit workspace access;
- no implicit network access;
- no implicit process execution;
- no implicit AI access;
- no implicit Logs, Output, Problems, Search Results, or Diagnostics access;
- open UI does not imply data access;
- user-visible permission grants;
- Workspace Trust gates risky capabilities;
- extension UI cannot shrink or corrupt core ergonomics;
- extension failure must not crash the core app;
- extensions must be lazy activated;
- extension actions must be auditable;
- phone and tablet capability is intentionally limited;
- desktop and workstation can support advanced capability later.

## 4. Comparison-derived model

### 4.1 VS Code lessons

Useful ideas to keep:

- manifest-driven contributions;
- activation events;
- commands;
- menus;
- views;
- language contributions;
- output channels;
- extension host separation;
- Marketplace-like distribution;
- extension API versioning.

Risk to avoid:

- overly broad runtime power;
- supply-chain dependency risk;
- too much default access;
- unbounded extension startup cost;
- hidden data access through UI state;
- weak separation between visible UI and readable data.

### 4.2 Browser extension lessons

Useful ideas to keep:

- manifest permissions;
- host-like scoped access;
- clear capability requests;
- install-time and runtime permission prompts;
- service-worker-like limited background behavior;
- strict separation between UI surfaces and privileged APIs.

Risk to avoid:

- making IDE capabilities too weak;
- pretending browser-like constraints can solve language toolchains alone.

### 4.3 JetBrains and Visual Studio lessons

Useful ideas to keep:

- deep extension points;
- advanced diagnostics;
- language tooling;
- project model integration;
- build/test/debug ecosystem direction.

Risk to avoid:

- heavy in-process plugin model;
- native or JVM-style plugin complexity in v1;
- deep plugins that can destabilize the core;
- excessive trust in marketplace identity alone.

### 4.4 Eclipse lessons

Useful ideas to keep:

- lifecycle concepts;
- extension points;
- dependency declaration.

Risk to avoid:

- heavy framework dependency;
- complex plugin classloading model;
- slow startup and high memory overhead.

## 5. Extension classes

Operre should classify extensions by capability and risk.

### 5.1 Low-risk classes

Examples:

- theme extension;
- icon theme extension;
- color customization;
- simple syntax grammar;
- snippets;
- readonly documentation helper.

Allowed early, with minimal permissions.

### 5.2 Medium-risk classes

Examples:

- UI contribution;
- command contribution;
- menu contribution;
- toolbar item;
- status bar item;
- panel view;
- formatter with explicit file access;
- search helper with scoped search access.

Requires manifest declaration and user-visible permission where data access is involved.

### 5.3 High-risk classes

Examples:

- language server connector;
- linter connector;
- diagnostics provider;
- file provider;
- remote workspace provider;
- output channel producer;
- logs or diagnostics contributor;
- network connector;
- AI connector.

Requires explicit permission, Workspace Trust where relevant, and audit logging.

### 5.4 Very-high-risk classes

Examples:

- compiler connector;
- interpreter connector;
- C toolchain connector;
- C++ toolchain connector;
- Python runtime connector;
- JavaScript runtime connector outside the sandbox;
- database server connector;
- web development server connector;
- simulator;
- emulator;
- linker;
- executable builder;
- package manager;
- live runtime;
- debugger;
- terminal-like process execution.

These must not be core extension v1 runtime features. They are later desktop/workstation-only external toolchain/runtime integrations.

## 6. Runtime architecture

### 6.1 Required components

The architecture should include:

- Operre Core;
- Extension Manager;
- Extension Registry Client;
- Extension Package Verifier;
- Extension Host;
- Permission Broker;
- Workspace Trust Broker;
- Contribution Registry;
- Command Registry;
- Device Capability Resolver;
- External Toolchain Broker later;
- Process Execution Broker later;
- Audit Log;
- Settings and Sync Resolver.

### 6.2 Extension Host

The first extension host should support TypeScript/JavaScript extension control logic.

The host must be isolated from the core UI. Extension code should not directly mutate core UI internals, read arbitrary state, or call private APIs.

The Extension Host should communicate with Operre Core through a narrow API bridge controlled by the Permission Broker.

### 6.3 WASM future option

WASM may be added later for safer compute-oriented extensions.

Possible uses:

- parsers;
- formatters;
- syntax tools;
- lightweight analysis;
- deterministic transforms.

WASM must still use declared permissions and must not bypass file, network, process, or secret restrictions.

### 6.4 External toolchain broker

External tools are not extension core runtime.

External tools are launched and controlled through a broker later.

The broker must control:

- executable path;
- working directory;
- arguments;
- environment variables;
- file access;
- network access;
- stdin;
- stdout;
- stderr;
- exit code;
- timeout;
- process tree termination;
- resource limits;
- output redaction;
- diagnostics correlation;
- audit logging.

The broker lets Operre coordinate tools without embedding unsafe native code into the core process.

## 7. C, C++, Python, JavaScript runtime, database, and web tooling

Operre may eventually coordinate many tool families:

- C compiler;
- C++ compiler;
- Python interpreter;
- JavaScript or Node runtime;
- TypeScript tools;
- database clients;
- database migration tools;
- web dev servers;
- package managers;
- linkers;
- simulators;
- emulators;
- executable builders;
- live runtime surfaces;
- REPL surfaces.

Rules:

- not in v0.1 core extension runtime;
- desktop/workstation only by default;
- Workspace Trust required;
- explicit user permission required;
- extension manifest must declare the tool;
- user or system must provide license-compatible tools;
- Operre must not silently bundle or download tools with unclear license terms;
- command lines must be previewable where practical;
- output must be redacted;
- secrets must not be exposed;
- resource limits must exist;
- audit log is required;
- phone and tablet do not get full local runtime execution by default.

## 8. Contribution points

### 8.1 Core contribution points

Required contribution point families:

- commands;
- menus;
- command palette;
- toolbar items;
- status bar items;
- activity entries;
- views;
- panels;
- themes;
- icon themes;
- syntax grammars;
- snippets;
- settings schema;
- keybinding defaults;
- problem sources;
- output channels;
- diagnostics summaries;
- logs summaries;
- safe file decorations;
- context menu items.

### 8.2 Later contribution points

Later contribution point families:

- language server connectors;
- debugger connectors;
- test adapters;
- build task providers;
- runtime session providers;
- terminal-like process providers;
- remote workspace providers;
- custom file system providers;
- AI connectors;
- toolchain connectors;
- simulator connectors;
- emulator connectors;
- database connectors;
- executable builder providers.

### 8.3 Contribution rules

Every contribution must declare:

- stable ID;
- title;
- owner extension;
- contribution point;
- activation condition;
- device support;
- required permissions;
- Workspace Trust requirement;
- default visibility;
- user-hideable behavior;
- accessibility label;
- security description where relevant.

Extensions cannot inject arbitrary UI. They can only contribute through declared contribution points.

## 9. Manifest schema direction

### 9.1 Manifest format

The first manifest format should be JSON or JSONC.

JSON is strict and simple. JSONC can improve author ergonomics with comments. The final decision can be made during implementation, but the schema must remain deterministic and machine-validated.

### 9.2 Required manifest sections

The manifest should include:

- manifestVersion;
- id;
- publisher;
- name;
- displayName;
- version;
- license;
- engines;
- kind;
- entrypoints;
- activationEvents;
- contributes;
- permissions;
- deviceSupport;
- workspaceTrust;
- dependencies;
- packageIntegrity;
- sync;
- privacy;
- security;
- support;
- repository.

### 9.3 Manifest example

Example direction:

    {
      "manifestVersion": 1,
      "id": "example.safe-markdown-tools",
      "publisher": "example",
      "name": "safe-markdown-tools",
      "displayName": "Safe Markdown Tools",
      "version": "0.1.0",
      "license": "MIT",
      "engines": {
        "operre": "^0.1.0"
      },
      "kind": ["ui", "syntax", "formatter"],
      "entrypoints": {
        "extensionHost": "dist/extension.js"
      },
      "activationEvents": [
        "onLanguage:markdown",
        "onCommand:markdown.formatSafe"
      ],
      "deviceSupport": {
        "desktop": "full",
        "tablet": "limited",
        "phone": "summary"
      },
      "workspaceTrust": {
        "required": false,
        "limitedMode": true
      },
      "contributes": {
        "commands": [],
        "menus": [],
        "views": [],
        "themes": [],
        "grammars": [],
        "settings": [],
        "statusBarItems": [],
        "problemSources": [],
        "outputChannels": []
      },
      "permissions": {
        "workspaceRead": "none",
        "workspaceWrite": "none",
        "network": "none",
        "processExecution": "denied",
        "logsRead": "denied",
        "diagnosticsRead": "denied",
        "aiAccess": "denied",
        "protectedPaths": "denied"
      },
      "sync": {
        "settings": "safe",
        "enabledState": true,
        "deviceOverride": true
      },
      "privacy": {
        "telemetry": false,
        "collectsFileContent": false,
        "collectsDiagnostics": false
      },
      "security": {
        "signatureRequired": true,
        "minimumTrustLevel": "default"
      }
    }

## 10. Permission model

Default permissions:

- no file read;
- no file write;
- no workspace tree read;
- no Search Results read;
- no Problems read;
- no Output read;
- no Logs read;
- no Diagnostics read;
- no secrets;
- no network;
- no process execution;
- no terminal;
- no AI;
- no protected paths;
- no environment variables.

Permission categories:

- workspace.read;
- workspace.write;
- file.read;
- file.write;
- search.read;
- problems.read;
- output.read;
- output.write;
- logs.read;
- diagnostics.read;
- network.access;
- process.execute;
- terminal.access;
- secrets.read;
- ai.access;
- protectedPaths.read;
- settings.read;
- settings.write;
- clipboard.read;
- clipboard.write.

Dangerous permissions require explicit approval and audit logging.

## 11. Workspace Trust

Workspace Trust is mandatory for risky extension operations.

Requires trust:

- process execution;
- build tasks;
- compiler tools;
- interpreters;
- linkers;
- executable builders;
- package managers;
- live runtime;
- debugger connectors;
- terminal-like execution;
- file writes outside safe scope;
- protected path access;
- external network access where project content may be transmitted.

Restricted Mode behavior must exist for extensions.

An extension must declare what it can still do in limited mode.

## 12. Extension lifecycle

Lifecycle states:

- discovered;
- installed;
- verified;
- disabled;
- enabled;
- activated;
- suspended;
- crashed;
- blocked;
- uninstalled;
- update available;
- update staged;
- revoked.

Activation must be lazy.

Activation triggers must be explicit:

- onCommand;
- onLanguage;
- onView;
- onFileOpen;
- onWorkspaceOpen;
- onStartup, restricted and discouraged;
- onToolchainSession, later;
- onDiagnosticsSession, later.

Startup activation is high risk and should be limited.

## 13. Dependency management

Dependencies must be declared.

Rules:

- no implicit install-time dependency download by default;
- no arbitrary postinstall scripts;
- packaged dependencies should be hashed;
- dependency lock metadata should be included;
- native dependencies require high-risk classification;
- optional dependencies must be explicit;
- extension updates must not silently add dangerous dependencies;
- dependency changes must be visible during update review.

JavaScript dependencies are allowed for extension packages, but the runtime must not run package manager install scripts inside the user workspace by default.

## 14. Package signing and integrity

Extension packages should have:

- package ID;
- version;
- publisher ID;
- manifest hash;
- package hash;
- signature;
- signing certificate or publisher key reference;
- timestamp;
- revocation status;
- minimum Operre version;
- target platform metadata;
- device support metadata.

client-side verification is required.

The registry server is not the only trust anchor. If the server is compromised, the client should still reject invalid or unsigned packages when signature policy requires signing.

## 15. Installation without public marketplace

A public marketplace is not required for early extension use.

Supported early install channels:

- local unpacked extension folder;
- local packaged extension file;
- development-mode extension path;
- private registry from one VPS;
- GitHub release or direct package URL, later and restricted;
- built-in bundled first-party extensions, if needed.

Development workflow:

- install from local folder;
- verify manifest;
- run in development mode;
- show requested permissions;
- allow temporary permission grants;
- write audit events;
- allow quick disable and reload.

User distribution before marketplace:

- signed package file;
- private registry download;
- organization registry;
- manual install with clear warning;
- versioned release metadata.

This allows extension testing and user delivery before a full marketplace exists.

## 16. Private registry and single VPS plan

A single VPS can support the first registry.

Initial registry can provide:

- user login later;
- publisher login later;
- extension metadata;
- version list;
- package download;
- hash metadata;
- signature metadata;
- compatibility metadata;
- device support metadata;
- update manifest;
- basic admin moderation;
- revocation list;
- private visibility;
- organization visibility later.

Possible stack later:

- Node.js or Rust service;
- PostgreSQL;
- filesystem package storage or object storage;
- HTTPS through reverse proxy;
- signed metadata;
- backup process;
- audit log;
- rate limiting.

A single VPS is acceptable for early private registry and controlled beta distribution.

A larger public marketplace later may require:

- object storage;
- CDN;
- malware scanning queue;
- static analysis;
- publisher verification;
- transparency log;
- staged rollout;
- reputation system;
- abuse handling.

## 17. Sync planning

Sync must not be one global dump.

Profiles:

- global user profile;
- device profile;
- machine-local profile;
- workspace profile;
- extension profile;
- secret vault.

Syncable by default or opt-in:

- theme;
- safe settings;
- keybindings;
- extension IDs;
- extension enabled state;
- extension version preference;
- safe extension settings.

Machine-local by default:

- UI scale;
- layout dimensions;
- panel size;
- sidebar width;
- touch mode;
- compact mode;
- window geometry;
- recent files;
- workspace trust;
- logs;
- diagnostics;
- secrets;
- local toolchain paths;
- runtime paths;
- external process configuration.

Extension sync must not blindly copy binaries.

Each machine must:

- check platform compatibility;
- check device support;
- verify signature;
- verify package hash;
- respect Workspace Trust;
- respect phone/tablet restrictions;
- apply safe settings only;
- keep secrets in local OS keyring or vault.

## 18. Phone and tablet limits

Phone and tablet extension support is intentionally limited.

Allowed early:

- themes;
- icon themes;
- simple syntax highlighting;
- snippets;
- safe command surface;
- limited Problems summaries;
- limited Search Results summaries;
- safe Diagnostics summaries;
- lightweight read-only helpers.

Not allowed by default:

- full local process execution;
- compiler execution;
- interpreter execution;
- C or C++ build;
- Python runtime;
- Node runtime outside sandbox;
- database server tooling;
- web development server;
- debugger;
- terminal;
- full Output streaming;
- unbounded Logs;
- dense diagnostics tables;
- local executable builders.

The goal is not to force phone or tablet hardware beyond ergonomic limits. A weak or cramped experience is worse than a deliberately limited experience.

## 19. Performance and ergonomics

Extensions must not make Operre feel heavy.

Required rules:

- lazy activation;
- activation time budget;
- memory budget;
- CPU budget where practical;
- no UI thread blocking;
- no unbounded background polling;
- no unbounded file watching;
- no hidden startup extension storm;
- extension host crash isolation;
- extension host restart policy;
- slow extension warning;
- user-visible disable action;
- safe mode disables third-party extensions where needed.

Extension UI contributions must follow Operre responsive and high-DPI rules.

Extensions cannot make menu, toolbar, status bar, or panel controls microscopic, clipped, overlapping, or unusable.

## 20. Audit and transparency

Operre must log extension actions safely.

Audit events should include:

- extension installed;
- extension enabled;
- extension disabled;
- extension updated;
- extension activated;
- extension crashed;
- permission requested;
- permission granted;
- permission denied;
- file read requested;
- file write requested;
- network access requested;
- process execution requested;
- external toolchain session started later;
- diagnostics access requested;
- AI access requested;
- protected path access denied.

Audit logs must not include secrets or full file contents by default.

## 21. Marketplace policy direction

Marketplace policy should include:

- publisher identity;
- package signing;
- manifest validation;
- dangerous permission review;
- version history;
- revocation;
- user reporting;
- security advisory process;
- license metadata;
- privacy metadata;
- device support metadata;
- compatibility metadata.

Marketplace existence must not weaken local user control. Users must still see what an extension asks for and what it can access.

## 22. v0.1 scope

Included in planning:

- manifest schema direction;
- contribution point list;
- TypeScript/JavaScript core extension host direction;
- default-deny permission model;
- local install plan;
- development-mode extension path;
- private registry direction;
- single VPS feasibility;
- sync planning;
- device limits;
- external toolchain broker direction;
- C, C++, Python, database, web, linker, simulator, emulator, and runtime tools classified as later brokered integrations.

Excluded from v0.1 implementation:

- public marketplace;
- native in-process plugins;
- Python as core extension runtime;
- C or C++ as core extension runtime;
- full external toolchain broker;
- process execution broker;
- debugger integration;
- terminal integration;
- phone full extension runtime;
- tablet full extension runtime;
- AI connector runtime;
- remote workspace provider.

## 23. Relationship with later topics

Next topic:

NEXT_TOPIC: Extension permission UI and approval flow

Likely later topics:

- Workspace Trust deep behavior;
- safe terminal and process execution model;
- toolchain and live runtime broker model;
- marketplace and package signing details;
- settings sync and account model;
- first implementation milestone freeze.

## Permission UI relationship

Extension manifest permissions are declarations, not automatic grants. OPR-SPEC-0039 defines install-time summaries, runtime critical prompts, scoped grants, duration choices, risk bars, update policy, local extension Developer Mode, phone/tablet disabled desktop-required capability display, revocation controls, Safe Mode, and audit logging.

## Workspace Trust relationship

Extension manifests must declare limited-mode behavior for untrusted or restricted workspaces. High-risk contribution points may be disabled until Workspace Trust and required permissions are granted. Desktop-only toolchain and live runtime contributions require Workspace Trust and later broker approval.

## Toolchain contribution relationship

Toolchain-related extension contribution points must be declarative.
They may describe profile templates, command templates, parser
capabilities, and limited-mode behavior. They must not grant execution
authority by themselves. Toolchain execution requires profile approval,
Workspace Trust, permissions, Resource Governor policy, and audit logs.
