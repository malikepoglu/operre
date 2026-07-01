# Operre External Toolchain and Live Runtime Broker Model

Status: Accepted specification
Topic ID: OPR-SPEC-0042
Scope: External toolchain broker, live runtime broker, toolchain profiles,
toolchain discovery, Python, C, C++, JavaScript, TypeScript, Node,
database tools, NoSQL tools, web development servers, package managers,
REPL sessions, simulators, emulators, model runtimes, outputs, logs,
artifacts, resource governance, sandbox planning, toolchain installation,
extension contributions, AI assistance, phone and tablet behavior,
diagnostics integration, production guards, remote toolchains, sync
rules, per-project dashboards, and safe reset behavior.

## 1. Purpose

This document defines how Operre coordinates external development tools
without turning the core editor into an uncontrolled process runner.

Operre should become a powerful development platform for real projects,
including future work on systems such as LogisticSearch, Ideboard,
Chessci, and other user projects.

External tools must be powerful, ergonomic, performant, observable, and
safe.

Operre must protect:

- the core app;
- user files;
- workspace content;
- protected paths;
- secrets;
- environment variables;
- logs;
- diagnostics;
- AI context;
- production systems;
- remote systems;
- package supply chain boundaries;
- database credentials;
- generated artifacts.

## 2. Core decision

External toolchain execution is brokered.

Toolchain Broker is a separate security and coordination layer.

Toolchain Broker works with:

- Permission Broker;
- Workspace Trust Broker;
- Process Execution Broker;
- Resource Governor;
- Output router;
- Problems router;
- Diagnostics router;
- Logs system;
- Audit Log;
- Package Verifier later;
- Secret Broker later;
- Remote Execution Broker later.

No external toolchain, live runtime, extension, AI feature, task, panel,
or command may bypass these brokers.

## 3. Toolchain Broker responsibility

Toolchain Broker knows:

- which tool is being used;
- which profile describes it;
- which workspace or root owns the action;
- which extension or user requested it;
- which permissions are required;
- which trust state applies;
- which files may be read;
- which files may be written;
- which output channel is used;
- which log file is used;
- which artifacts are created;
- which network or port scope is requested;
- which environment variables are allowed;
- which secrets are mapped;
- which resource limits apply;
- how the process starts;
- how the process stops;
- how failure is reported;
- how diagnostics are produced;
- how audit records are written.

Toolchain Broker is not only a command launcher. It is the policy and
coordination layer for external development capability.

## 4. Toolchain scope

The model covers:

- compiler;
- interpreter;
- linker;
- formatter;
- linter;
- test runner;
- debugger adapter later;
- package manager;
- database client;
- NoSQL database client;
- migration tool;
- seed tool;
- schema diff tool;
- backup and restore tool;
- web development server;
- REPL;
- live runtime;
- simulator;
- emulator;
- executable builder;
- model runtime later;
- deployment helper later;
- monitoring helper later;
- remote toolchain later.

The scope is intentionally broad.

Each tool type must still receive separate risk classification,
permission category, output policy, and audit handling.

## 5. Toolchain profile model

A toolchain profile is the safe identity card for an external tool.

Operre must not treat a random executable path as an approved toolchain.

A profile describes what the tool is, where it is, what it can do, which
workspace it can work with, how it is approved, what it can read or
write, how it logs, and how it is stopped.

### 5.1 Identity fields

Profile identity fields include:

- profile ID;
- display name;
- profile type;
- language or technology;
- tool role;
- tool family;
- provider;
- source;
- owner extension, if any;
- created by user, extension, discovery, or import;
- created time;
- last modified time;
- last verified time;
- profile schema version;
- profile description;
- help link;
- license summary, if known.

Tool roles include:

- compiler;
- interpreter;
- linker;
- formatter;
- linter;
- test runner;
- debugger adapter;
- package manager;
- database client;
- migration tool;
- seed tool;
- web development server;
- REPL;
- live runtime;
- simulator;
- emulator;
- model runtime;
- deployment helper;
- monitoring helper.

### 5.2 Executable fields

Executable fields include:

- executable path;
- resolved real path;
- symlink state;
- file owner;
- file permissions;
- version command;
- detected version;
- version requirement;
- executable hash, optional;
- signature state, later;
- package source, if known;
- blocked path state;
- protected path state;
- missing executable state;
- last verification result.

Executable hash is not mandatory for every profile.

High-risk and production-related profiles may require stronger
verification.

### 5.3 Workspace fields

Workspace fields include:

- allowed workspace;
- allowed root;
- allowed working directory;
- multi-root behavior;
- symlink behavior;
- protected path behavior;
- external workspace behavior;
- Operre-managed project behavior;
- allowed project type;
- output folder policy;
- artifact folder policy;
- log folder policy.

### 5.4 Permission fields

Permission fields include:

- required Workspace Trust;
- required permission IDs;
- required network permission;
- required file read scope;
- required file write scope;
- required environment permission;
- required secret mapping;
- required elevated execution, if any;
- phone capability state;
- tablet capability state;
- production guard state;
- remote execution state.

### 5.5 Environment fields

Environment fields include:

- sanitized environment enabled;
- allowed environment keys;
- blocked environment keys;
- redacted environment keys;
- secret mapping list;
- inherit user shell environment setting;
- workspace environment file handling;
- `.env` handling;
- virtual environment activation behavior;
- path mutation behavior;
- locale behavior;
- home directory exposure policy.

Environment inheritance should be restricted by default.

Raw environment access must not be given to extensions or AI by default.

### 5.6 Output and log fields

Output and log fields include:

- stdout channel;
- stderr channel;
- output parser;
- problem matcher;
- diagnostics parser;
- log ID policy;
- log path;
- log retention policy;
- log redaction policy;
- artifact output path;
- max output bytes;
- max visible lines;
- max log size;
- output spool policy;
- artifact retention policy.

### 5.7 Risk and approval fields

Risk and approval fields include:

- risk level;
- approval state;
- approval scope;
- approval duration;
- approved by;
- approved at;
- last review reason;
- review needed state;
- block reason;
- quarantine reason;
- safe reset action;
- recommended default;
- unsafe setting badge;
- production warning state.

### 5.8 Resource fields

Resource fields include:

- timeout;
- idle timeout;
- maximum concurrent sessions;
- restart limit;
- process tree kill behavior;
- output limit;
- log limit;
- CPU limit later;
- memory limit later;
- disk write quota later;
- network limit later;
- battery awareness later;
- thermal awareness later.

### 5.9 UX fields

UX fields include:

- show in Command Palette;
- show in toolbar;
- show in Run menu;
- show in status bar;
- show in project dashboard;
- quick action label;
- warning text;
- help link;
- setup guide link;
- reset-to-default action;
- open profile action;
- open log action;
- open output action;
- open artifact action.

## 6. Profile states

Toolchain profile states include:

- discovered;
- pending review;
- approved;
- approved for workspace;
- approved for machine;
- blocked;
- quarantined;
- review needed;
- deprecated;
- missing.

Profile state must be visible in the per-project Toolchains dashboard.

Profile state changes must be audited.

A missing profile must not silently fall back to another executable.

A quarantined profile cannot run.

A review-needed profile cannot run dangerous actions until reviewed.

## 7. Toolchain install modes

Toolchain install modes are:

- A: detect only;
- B: detect and guide;
- C: user-approved install helper;
- D: curated installer later.

The recommended default is A plus B.

Operre should detect and explain tools by default, not silently install
them.

C and D require explicit user settings, risk explanations, and audit
logging.

System package manager installation is critical risk.

Every risky installation setting must offer reset to recommended default.

## 8. Discovery model

Toolchain discovery has three layers.

### 8.1 Passive discovery

Passive discovery checks known paths, PATH entries, workspace files, and
metadata without running external commands when possible.

Examples:

- known Python locations;
- known Node locations;
- known compiler paths;
- known package manager paths;
- project configuration files;
- lock files;
- CMake files;
- Makefiles;
- package manifests.

Passive discovery must not grant trust.

### 8.2 Verified discovery

Verified discovery may run version commands.

Examples:

- python --version;
- node --version;
- gcc --version;
- clang --version;
- cmake --version;
- psql --version.

Verified discovery is still process execution.

It must respect Workspace Trust, permission policy, command preview where
required, output limits, and audit logging.

### 8.3 Project discovery

Project discovery may inspect project files.

Examples:

- pyproject.toml;
- requirements.txt;
- package.json;
- package lock files;
- CMakeLists.txt;
- Makefile;
- compile_commands.json;
- docker-compose files;
- migration folders;
- database config examples;
- `.env.example`.

Secrets and real `.env` files must not be silently read.

Discovery results show:

- executable path;
- version;
- source;
- risk;
- approve;
- ignore;
- block;
- review later.

Auto discovery suggests profiles. It does not approve them.

## 9. Operre-managed Works root

Operre-managed projects use a configurable Works root.

The setting name should be:

- operre.worksRoot.

New Operre-managed projects may use:

- Works root;
- project folder;
- `.operre`;
- src;
- outputs;
- logs;
- artifacts;
- tmp.

Recommended structure:

- Works/ProjectName/.operre;
- Works/ProjectName/src;
- Works/ProjectName/outputs;
- Works/ProjectName/logs;
- Works/ProjectName/artifacts;
- Works/ProjectName/tmp.

Language and tool folders may include:

- outputs/python;
- outputs/node;
- outputs/cpp;
- outputs/web;
- outputs/database;
- artifacts/build;
- artifacts/release;
- logs/toolchain;
- logs/runtime.

The Works root must be user-configurable.

The Works root setting must have reset to recommended default.

## 10. External workspace write policy

External workspaces must not be modified with outputs, logs, or
artifacts folders by default.

For external workspaces, Operre should use app-local spool and log
storage by default.

Operre may suggest a project-local outputs folder, but the user must
approve writing it.

The UI must show:

- proposed folder;
- write scope;
- owner toolchain profile;
- cleanup policy;
- retention policy;
- risk summary.

External workspace behavior must be respectful and non-invasive.

External workspaces must not be modified with outputs, logs, or artifacts folders by default.

## 11. Python model

Python should prefer project-local isolation.

Interpreter preference order:

- workspace `.venv`;
- Operre-managed project venv;
- user-selected venv;
- system Python with warning;
- install or download only with explicit approval.

Python profile fields include:

- interpreter path;
- venv path;
- Python version;
- package manager relationship;
- pip policy;
- requirements file;
- pyproject file;
- lock file;
- test runner;
- formatter;
- linter;
- diagnostics parser;
- output policy;
- artifact policy.

Global Python package installation is high risk.

pip install is package manager execution.

requirements, pyproject, and lock changes should be logged.

stdout and stderr route to structured Output channels.

Python diagnostics can later feed Problems and Diagnostics.

## 12. C and C++ model

C and C++ support must be strong but separated by role.

Profile families include:

- compiler profile;
- linker profile;
- build system profile;
- run profile;
- debug profile later;
- artifact profile.

Supported tools may include:

- gcc;
- g++;
- clang;
- clang++;
- cmake;
- make;
- ninja;
- gdb later;
- lldb later.

C and C++ rules:

- compiler path is visible;
- compiler version is visible;
- build output scope is visible;
- executable artifact path is visible;
- run requires separate permission;
- debug is higher risk;
- generated files are separated;
- clean and rebuild may be destructive;
- compile_commands integration is allowed later;
- linker diagnostics are separate from compiler diagnostics.

Build, run, debug, test, live runtime, and REPL are separate permission
categories.

## 13. JavaScript, TypeScript, and Node model

Node and JavaScript tooling are powerful but supply-chain sensitive.

Profile types include:

- Node runtime profile;
- TypeScript compiler profile;
- npm profile;
- pnpm profile;
- yarn profile;
- test runner profile;
- formatter profile;
- linter profile;
- dev server profile.

Rules:

- package manager execution is high-risk or very-high-risk;
- install scripts are flagged;
- postinstall scripts are flagged;
- lockfile diff should be shown when possible;
- dev server requires port and network policy;
- node_modules should not be blindly scanned;
- global install is high risk;
- npx or remote package execution is very-high-risk;
- output goes through structured Output;
- package diagnostics may feed Diagnostics.

## 14. Database and NoSQL tools

MongoDB and NoSQL database tools are in scope.

Database tool categories include:

- embedded database;
- local database client;
- remote database client;
- migration tool;
- seed tool;
- schema diff tool;
- backup tool;
- restore tool;
- monitoring query;
- admin query.

Technologies may include:

- SQLite;
- PostgreSQL;
- MySQL;
- MariaDB;
- MongoDB;
- Redis;
- Elasticsearch;
- OpenSearch;
- ClickHouse;
- DuckDB;
- Neo4j later;
- vector databases later.

Rules:

- connection strings are secrets;
- passwords are not placed in raw environment by default;
- OS keyring or secret vault is later;
- read-only local query is lower risk;
- remote query is higher risk;
- write query is higher risk;
- migration is high-risk;
- destructive migration is critical;
- production database is critical by default;
- backup and restore require special approval;
- database output must be redacted;
- logs must not store secrets.

Production system guard is required for production-like targets.

## 15. Web development server model

Web development servers are live runtime sessions.

Rules:

- port is visible;
- bind address is visible;
- localhost is the default;
- LAN bind requires warning;
- public bind is high-risk or critical;
- network permission is required;
- browser open action is separate permission;
- process lifecycle is visible;
- output routes through structured Output;
- port conflict is handled ergonomically;
- phone and tablet show safe status only by default.

Web server profiles may include:

- command template;
- port policy;
- environment policy;
- browser open policy;
- output parser;
- health check later;
- restart policy;
- idle policy.

## 16. Live runtime model

Live runtime is a persistent session, not a simple short process.

Examples:

- Python REPL;
- Node REPL;
- web development server;
- notebook-like runtime later;
- local model runtime later;
- simulator;
- emulator;
- database shell;
- long-running watcher.

Live runtime states include:

- created;
- pending approval;
- starting;
- warm;
- running;
- idle;
- restarting;
- stopping;
- crashed;
- quarantined;
- stopped.

Every live runtime has:

- session ID;
- log ID;
- output channel;
- resource limits;
- idle timeout;
- restart policy;
- stop action;
- kill action;
- audit trail;
- diagnostics relationship;
- owner profile;
- owner workspace;
- trust state.

Live runtime cannot hide behind an ordinary output panel.

## 17. Output, logs, and artifacts

Toolchain output is separated.

Surfaces:

- raw stdout and stderr go to Output;
- parsed errors go to Problems;
- deep compiler, test, runtime, package, and environment data go to
  Diagnostics;
- process records go to Logs;
- generated files go to Artifacts later.

Operre-managed projects may use organized folders.

External workspaces use app-local spool by default unless the user
approves project-local output.

Every output-producing session must have:

- session ID;
- log ID;
- output channel;
- retention policy;
- redaction state;
- owner profile;
- owner workspace.

## 18. Resource Governor

Resource Governor is a separate concept.

Resource Governor controls:

- timeout;
- idle timeout;
- maximum output bytes;
- maximum visible lines;
- maximum log size;
- maximum concurrent processes;
- maximum restart count;
- process tree cleanup;
- runaway process detection;
- stuck process warnings;
- long-running process badge;
- per-workspace process quota later;
- per-extension process quota later;
- per-toolchain process quota later;
- CPU limit later;
- memory limit later;
- disk write quota later;
- network bandwidth limit later;
- battery awareness later;
- thermal awareness later;
- low-resource mode later.

Risky toolchains should start with stricter limits.

The editor core must stay responsive while toolchains run.

## 19. Sandbox model

Sandboxing is layered.

Layer 1: broker-level sandbox.

- permission;
- trust;
- scope;
- environment;
- output;
- logging;
- audit.

Layer 2: process-level control.

- process tree;
- timeout;
- working directory;
- environment;
- output limits;
- log limits.

Layer 3: file-scope control.

- write folders;
- protected path block;
- artifact scope;
- temporary path scope.

Layer 4: network-scope control.

- domain;
- port;
- bind address;
- localhost;
- LAN;
- public exposure.

Layer 5: platform sandbox later.

- Linux namespace, cgroup, and seccomp;
- Windows Job Object and AppContainer later;
- macOS sandbox later.

First implementation may start with layers 1 and 2, plan layers 3 and 4,
and leave layer 5 as later platform work.

## 20. Toolchain installation

Operre does not silently download or install toolchains by default.

Default behavior:

- detect;
- explain;
- guide;
- profile create;
- verify path;
- version check;
- log.

Later user-approved behavior may include:

- install helper;
- first-party curated installer;
- signed package;
- hash verification;
- license display;
- rollback;
- uninstall helper;
- repair helper.

System package manager installation is critical risk.

Every install-related setting must provide:

- current value;
- recommended default;
- risk explanation;
- reset to recommended default;
- reset all toolchain safety settings;
- export settings;
- import settings;
- compare with recommended defaults;
- unsafe setting badge.

## 21. Extension toolchain contribution

Extensions may contribute:

- toolchain profile template;
- command template;
- diagnostics parser;
- problem matcher;
- output parser;
- recommended settings;
- required permissions;
- limited mode behavior;
- setup guide;
- profile validation rule;
- safe command category.

Extensions must not:

- force executable paths;
- run hidden commands;
- read raw environment;
- read secrets;
- install packages without approval;
- run before profile approval;
- bypass Toolchain Broker;
- bypass Process Execution Broker;
- bypass Workspace Trust;
- bypass audit logging.

Extension contributions are templates and integrations, not execution
authority.

## 22. AI toolchain assistance

Initial implementation keeps AI in advisory mode.

AI may help with:

- profile suggestion;
- setup explanation;
- command explanation;
- risk summary;
- build plan;
- test plan;
- diagnostics summary, if allowed;
- log analysis, if allowed;
- compiler error explanation;
- test failure analysis;
- migration risk explanation;
- safer command suggestion;
- rollback plan;
- resource issue diagnosis.

AI does not directly execute toolchains by default.

Future AI-assisted execution requires:

- explicit setting;
- Workspace Trust;
- permission grant;
- command preview;
- user approval;
- audit logging;
- no sudo by default;
- no secrets by default;
- no protected paths by default;
- production guard where relevant.

AI should begin as a powerful advisor, not an autonomous operator.

## 23. Phone and tablet behavior

Phone and tablet support safe toolchain visibility.

Allowed by default:

- profile viewing;
- process status summary;
- safe logs summary;
- diagnostics summary;
- command plan view;
- safe command copy;
- safe issue summary;
- remote job status later;
- stop request later, with strong controls.

Not allowed by default:

- local compiler;
- local interpreter;
- package install;
- full terminal;
- live runtime;
- debugger;
- dev server bind;
- sudo;
- administrator elevation;
- root shell.

Unsupported risky actions are shown as disabled with desktop required.

Future mobile-local toolchain planning can be a later topic.

## 24. Diagnostics integration

Diagnostics are a project control surface, not only an error list.

Toolchain diagnostics categories include:

- syntax diagnostics;
- compiler diagnostics;
- linker diagnostics;
- runtime diagnostics;
- test diagnostics;
- package diagnostics;
- dependency diagnostics;
- security diagnostics;
- performance diagnostics;
- migration diagnostics;
- environment diagnostics;
- resource diagnostics;
- port diagnostics;
- network diagnostics;
- crash diagnostics;
- flaky test diagnostics.

Each diagnostics item should include:

- source;
- severity;
- confidence;
- file;
- line;
- column;
- toolchain profile;
- process session ID;
- log ID;
- suggested fix;
- risk;
- AI access state;
- extension access state;
- workspace trust state;
- permission state.

Parser extensions require appropriate data access permission.

## 25. Production system guard

Production system guard is required for production-like targets.

Production-like targets include:

- production workspace;
- production database;
- production SSH target;
- production deployment;
- production migration;
- production secret;
- production destructive command;
- production backup;
- production restore;
- production remote toolchain;
- production monitoring command.

Production guard requires:

- critical warning;
- explicit target label;
- command preview;
- user acknowledgement;
- audit logging;
- log ID;
- rollback plan when possible;
- no silent AI execution;
- no silent extension execution;
- no default sync of approvals.

This protects all users, not only the original Operre projects.

## 26. Remote toolchain planning

Remote toolchain support is planned for later and disabled by default.

Possible remote targets:

- local desktop;
- VPS;
- Raspberry Pi;
- staging server;
- production server;
- remote container;
- remote development box;
- CI runner later.

Remote toolchain requires future broker work:

- Remote Execution Broker;
- remote identity;
- host trust;
- SSH or transport policy;
- credential handling;
- network policy;
- remote output routing;
- remote process lifecycle;
- remote audit log;
- production guard.

Remote execution must never be silently enabled.

## 27. Sync behavior

Toolchain profile sync is limited.

Profile templates may sync.

Executable approvals must not sync silently.

Executable paths must be machine-specific by default.

Secrets must not sync through toolchain profiles.

Production approvals must not sync silently.

Machine-local verification state stays machine-local.

Safe recommended settings may sync later.

Workspace and profile risk overrides require careful device-aware design.

Profile templates may sync, but executable approvals, paths, secrets, and
production approvals must not sync silently.

Profile templates may sync, but executable approvals, paths, secrets, and production approvals must not sync silently.

## 28. Per-project Toolchains dashboard

Operre should provide a per-project Toolchains dashboard.

The dashboard should show:

- Python profile;
- Node profile;
- C profile;
- C++ profile;
- database profile;
- web server profile;
- package manager profile;
- live runtime sessions;
- last run;
- current status;
- missing tools;
- setup guide;
- profile state;
- approval state;
- risk level;
- logs;
- diagnostics;
- outputs;
- artifacts;
- resource use;
- production guard state;
- blocked profiles;
- review-needed profiles;
- safe reset actions.

Per-project Toolchains dashboard is required for ergonomics.

The dashboard should help users fix setup problems without switching to
another editor.

## 29. Safe reset

Safe reset is mandatory.

Risky settings and profiles must provide:

- reset this setting;
- reset profile to safe default;
- reset workspace toolchains;
- reset all toolchain safety settings;
- disable all toolchain execution;
- disable all elevated execution;
- disable all package manager execution;
- disable all remote toolchain execution;
- disable all production actions;
- restore recommended defaults;
- compare with recommended defaults.

Safe reset prevents advanced settings from turning the system into an
unsafe or unusable configuration.

## 30. Settings

Recommended settings include:

- operre.worksRoot;
- toolchains.enabled;
- toolchains.discovery.enabled;
- toolchains.discovery.passive;
- toolchains.discovery.verified;
- toolchains.install.mode;
- toolchains.install.allowHelper;
- toolchains.install.allowCuratedInstaller;
- toolchains.requireProfileApproval;
- toolchains.requireWorkspaceTrust;
- toolchains.requireCommandPreview;
- toolchains.allowProfileTemplateSync;
- toolchains.syncExecutableApprovals;
- toolchains.syncExecutablePaths;
- toolchains.syncSecrets;
- toolchains.productionGuard.enabled;
- toolchains.remote.enabled;
- toolchains.dashboard.enabled;
- toolchains.safeReset.enabled;
- resourceGovernor.enabled;
- resourceGovernor.defaultTimeoutSeconds;
- resourceGovernor.defaultIdleTimeoutSeconds;
- resourceGovernor.maxOutputBytes;
- resourceGovernor.maxLogBytes;
- resourceGovernor.maxConcurrentProcesses;
- resourceGovernor.restartLimit;
- sandbox.fileScope.enabled;
- sandbox.networkScope.enabled;
- sandbox.platformSandbox.enabledLater;
- python.preferProjectVenv;
- cpp.requireSeparateRunApproval;
- node.warnOnInstallScripts;
- database.productionGuardDefault;
- webServer.defaultBindAddress;
- ai.toolchainAdvisoryOnly.

Recommended defaults:

- toolchains enabled for planning;
- execution guarded;
- install mode A plus B;
- profile approval required;
- Workspace Trust required;
- command preview required;
- executable approvals not synced;
- executable paths not synced;
- secrets not synced;
- production guard enabled;
- remote toolchains disabled;
- safe reset enabled;
- AI advisory only;
- platform sandbox later disabled until implemented.

## 31. Acceptance tests

Future implementation must test:

- a random executable cannot run without profile approval;
- discovery creates suggestions, not approval;
- verified discovery is logged;
- profile states are visible;
- missing profile does not silently fall back;
- quarantined profile cannot run;
- install mode default is A plus B;
- Works root is configurable;
- external workspace is not modified by default;
- Python prefers project-local venv;
- system Python shows warning;
- pip install is high risk;
- C and C++ run require separate approval;
- Node install scripts are flagged;
- npx remote execution is very-high-risk;
- MongoDB and NoSQL tools are recognized as database tools;
- production database action triggers production guard;
- web server localhost is default;
- public bind requires warning;
- live runtime has session ID and log ID;
- Resource Governor applies timeout and output limits;
- sandbox file scope blocks protected path writes;
- extension cannot force executable path;
- AI cannot directly execute toolchain by default;
- phone shows desktop required for local toolchain;
- tablet shows desktop required for local toolchain;
- diagnostics include toolchain profile and log ID;
- profile templates may sync;
- executable approvals do not sync silently;
- safe reset restores recommended defaults.

Failure conditions:

- toolchain runs without profile;
- extension bypasses Toolchain Broker;
- AI executes toolchain silently;
- production migration runs without production guard;
- secret appears in log;
- external workspace is polluted without approval;
- global package install happens silently;
- remote toolchain is enabled silently;
- profile approval syncs to another machine silently;
- output grows without limit;
- live runtime has no stop or kill action;
- Resource Governor is bypassed.

## 32. v0.1 scope

Included in planning:

- Toolchain Broker model;
- toolchain profile schema;
- profile states;
- install modes;
- discovery model;
- Works root model;
- external workspace write policy;
- Python model;
- C and C++ model;
- JavaScript, TypeScript, and Node model;
- database and NoSQL model;
- web development server model;
- live runtime model;
- outputs, logs, and artifacts model;
- Resource Governor;
- sandbox layers;
- extension contribution rules;
- AI advisory model;
- phone and tablet limits;
- production guard;
- remote toolchain planning;
- sync limits;
- per-project Toolchains dashboard;
- safe reset.

First implementation direction:

- profile schema skeleton;
- manual profile creation skeleton;
- discovery result list skeleton;
- no auto install;
- no uncontrolled run;
- process session model;
- output, log, and session ID model;
- broker API shape;
- trust and permission connections;
- ergonomic setup guidance before heavy execution features.

Real toolchains should be added step by step after the safety skeleton.

## 33. Relationship with later topics

Next topic:

NEXT_TOPIC: Managed Works projects templates and project dashboard behavior

Likely later topics:

- diagnostics dashboard deep behavior;
- marketplace and package signing details;
- settings sync and account model;
- first implementation milestone freeze.

## Managed Works project relationship

Managed Works projects provide the organized project structure used by
Toolchain Broker for outputs, logs, artifacts, project dashboards,
profile summaries, safe setup guidance, and non-invasive external
workspace behavior. Toolchain execution still requires profile approval,
Workspace Trust, permissions, Resource Governor policy, and audit logs.

## Deep diagnostics relationship

Toolchain Broker, live runtime sessions, Resource Governor, package
managers, database tools, web development servers, production guard, and
future remote toolchains may feed Diagnostics Dashboard. Each diagnostic
must reference source, severity, confidence, profile, session, log, and
permission state where applicable.
