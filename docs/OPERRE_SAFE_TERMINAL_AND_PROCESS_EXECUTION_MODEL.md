# Operre Safe Terminal and Process Execution Model

Status: Accepted specification
Topic ID: OPR-SPEC-0041
Scope: Terminal capability modes, process execution broker,
shell handling, command approval, command preview, logs,
environment variables, working directories, output routing,
process lifecycle, sudo/admin/root behavior, package managers,
build/run/debug/test/live runtime separation, AI command limits,
phone/tablet limits, performance, and audit behavior.

## 1. Purpose

This document defines how Operre may provide terminal and process
execution power without turning the editor into an uncontrolled shell.

Operre should become powerful enough that users do not need to switch to
another editor only for terminal, build, run, debug, Python, C, C++,
Node, package manager, database, web server, live runtime, REPL,
simulator, emulator, linker, or executable builder workflows.

At the same time, Operre must protect the core app, user data,
workspace content, secrets, protected paths, diagnostics, logs,
AI context, and the operating system.

## 2. Core decision

Terminal and process execution are brokered capabilities.

No extension, AI feature, panel, command, task, toolchain, or runtime
may directly execute a shell command without passing through:

- Permission Broker;
- Workspace Trust Broker;
- Process Execution Broker;
- Toolchain Broker, when applicable;
- Output, Problems, and Diagnostics routers;
- Audit Log.

The terminal surface can be visible in the core workbench, but process
execution must remain broker-controlled.

## 3. Terminal capability modes

Operre supports selectable terminal capability modes.

Required modes:

- A: no terminal;
- B: output-only or read-only process surfaces;
- C: basic guarded terminal;
- D: full guarded terminal.

The recommended default is A plus B.

This means the safe default has no unrestricted interactive shell, while
Output and Diagnostics surfaces can still exist.

Terminal mode D is full guarded terminal with per-action approval.

Users may change terminal mode through settings.

Mode changes must be logged.

Mode D must never mean uncontrolled execution.

Mode D still requires Workspace Trust, Permission Broker approval,
command preview, environment sanitation, audit logging, and dangerous
operation confirmation.

## 4. First implementation direction

The first implementation may include a simple terminal surface only if it
remains guarded and development-friendly.

The first milestone should prefer:

- no unrestricted terminal by default;
- output-only surfaces available;
- basic guarded terminal surface optional;
- command model prepared;
- command preview prepared;
- process sessions prepared;
- audit IDs prepared;
- settings prepared.

A simple terminal can exist early so the system can grow quickly, but it
must not bypass the broker model.

## 5. Core versus extension ownership

Terminal UI is a hybrid feature.

Core may provide:

- terminal panel shell;
- session list;
- output viewer;
- command preview UI;
- status indicators;
- stop and kill buttons;
- log links;
- permission prompt integration.

Execution is controlled by brokers.

Extensions may contribute terminal providers or toolchain profiles later,
but they cannot execute commands directly.

First-party providers are still subject to the same trust, permission,
preview, logging, and lifecycle rules.

## 6. Shell defaults

Shell detection may use platform defaults.

Possible defaults:

- Linux: user shell or bash;
- macOS: user shell or zsh;
- Windows: PowerShell, with cmd available as a profile.

Detected shell path must be visible before use.

Shell arguments must be visible before use.

The first shell launch requires Workspace Trust and user approval.

Shell profile changes must be logged.

Silent shell launch is forbidden.

## 7. Command approval

Commands are classified by risk.

Low risk examples:

- pwd;
- directory listing;
- git status;
- readonly metadata command.

Medium risk examples:

- linter;
- formatter;
- readonly test discovery;
- local analysis command.

High risk examples:

- build command;
- test command that writes artifacts;
- compiler invocation;
- interpreter run;
- database migration preview;
- file generation.

Very high risk examples:

- package manager install;
- network upload;
- shell script execution;
- Docker privileged mode;
- SSH;
- protected path access;
- secret access;
- environment export;
- recursive chmod;
- recursive delete.

Critical examples:

- sudo;
- administrator elevation;
- root shell;
- destructive system command;
- unrestricted script from untrusted workspace;
- command touching protected paths without explicit scope.

Low risk can use reduced prompting in trusted workspaces.

Medium risk prompts on first use or profile change.

High risk requires command profile approval.

Very high risk requires red critical bar and command preview.

Critical is blocked by default unless the user enables the relevant
advanced setting and confirms the exact operation.

## 8. Command preview

Command preview is required before risky commands.

Preview must show:

- command ID;
- command path;
- arguments;
- working directory;
- workspace root;
- trust state;
- extension owner, if any;
- toolchain profile, if any;
- process mode;
- environment summary;
- redacted secret summary;
- expected file write scope;
- expected network scope;
- output destination;
- log ID;
- log file path;
- timeout;
- resource limits;
- reason declared by extension or tool profile;
- permission grant duration.

The working directory path must be clickable.

Clicking the path should open the directory in the operating system file
explorer.

The log file path must be clickable.

Clicking the log file should open the log in Operre.

Command preview must be recorded in the audit log.

## 9. Environment variables

Environment variables are powerful and dangerous.

They can contain tokens, API keys, database passwords, SSH agent data,
cloud credentials, cookies, sessions, and other secrets.

Default process environment must be sanitized.

Extensions cannot read raw environment variables by default.

AI cannot read raw environment variables by default.

Secrets are not injected automatically.

User-approved secret mapping may inject a specific secret into a
specific process session.

Environment preview must redact dangerous keys.

Dangerous key patterns include:

- token;
- key;
- secret;
- password;
- passwd;
- auth;
- credential;
- cookie;
- session;
- bearer;
- private;
- certificate;
- ssh.

Environment changes must be logged.

## 10. Working directory

The default managed workspace location for new Operre projects should be
a user-configurable Works root.

Suggested pattern:

- Operre Works root;
- project folder;
- language or tool folders when useful;
- output and log folders managed by Operre.

For existing opened workspaces, the default working directory is the
trusted workspace root or a selected trusted root.

For multi-root workspaces, the user must select the root.

Untrusted roots cannot be used for execution.

Protected paths cannot be used without separate approval.

Symlink and special file state must be visible when relevant.

Extensions cannot silently force a working directory.

Toolchain profiles may suggest a working directory, but the user must be
able to inspect it.

## 11. Output routing

The canonical visible output surface is the structured Output panel.

Each process session gets a session ID.

stdout and stderr must be tracked separately.

Output channels must identify the owner.

Output can be routed to:

- Output panel;
- Problems parser later;
- Diagnostics session later;
- log file;
- managed artifact folder;
- user-approved project output folder.

Large output must use limits.

Recommended controls:

- output ring buffer;
- file spool;
- max visible lines;
- max retained bytes;
- redaction;
- collapse repeated lines;
- downloadable safe summary later.

For managed Operre projects, output files may use a project-local
organized folder.

Suggested pattern:

- Works root;
- project name;
- outputs;
- tool or language;
- session ID.

For external workspaces, Operre may use app-local spool storage by
default and offer an explicit project output folder setting.

Phone and tablet must not expose full unbounded terminal output.

## 12. Logging

Every process session must have a log ID.

Every process session should have a log file path.

The UI should show:

- log ID;
- log file path;
- session ID;
- command profile;
- start time;
- end time;
- exit code;
- trust state;
- permission decision;
- redaction state.

The log ID should be copyable.

The log file path should be clickable.

Clicking the log path opens the log in Operre.

Clicking the working directory opens the directory in the operating
system file explorer.

Logging options must be user-configurable.

Log settings should include:

- enable process logs;
- log command preview;
- log stdout;
- log stderr;
- log redacted environment summary;
- log permission decisions;
- log working directory;
- log duration;
- log exit code;
- log file path;
- max log size;
- log retention days;
- redact protected paths;
- redact secrets;
- export safe log summary.

Logs must not store secrets by default.

## 13. Process lifecycle

Required lifecycle states:

- created;
- permission pending;
- trust pending;
- approved;
- starting;
- running;
- stopping;
- exited;
- failed;
- timed out;
- killed;
- blocked;
- quarantined.

Required controls:

- stop process;
- kill process tree;
- timeout;
- maximum output size;
- maximum runtime;
- concurrent process limit;
- restart with approval;
- open log;
- open output;
- copy command preview;
- report failure.

Future controls:

- memory limit;
- CPU limit;
- network limit;
- file write quota;
- sandbox profile.

## 14. Sudo, admin, and root

Sudo, administrator, and root operations are supported only as an
advanced user-controlled capability.

Default state:

- disabled;
- blocked;
- not recommended.

Users may enable elevated execution settings.

Elevated execution must require:

- Workspace Trust;
- explicit setting enabled;
- red critical bar;
- exact command preview;
- separate approval for each operation;
- operating system authentication where applicable;
- no stored sudo password;
- no extension auto-sudo;
- no AI auto-sudo;
- audit logging;
- clear exit status;
- visible log ID;
- visible log file path.

Linux sudo may ask for the operating system password.

Operre must not store that password.

Every elevated action must be approved separately unless a later,
explicit, short-lived, user-controlled policy says otherwise.

## 15. Package managers

Package managers are high-risk or very-high-risk.

Examples:

- npm;
- pnpm;
- yarn;
- pip;
- pipx;
- poetry;
- cargo;
- go;
- maven;
- gradle;
- apt;
- dnf;
- pacman;
- brew;
- choco;
- winget.

Rules:

- blocked in untrusted workspaces;
- network permission required;
- command preview required;
- lockfile changes should be shown when possible;
- install scripts should be flagged;
- postinstall scripts should be flagged;
- system package managers are critical risk;
- package manager logs must be stored;
- package manager output must be redacted.

Package manager execution must be easy enough for real development but
never silent.

## 16. Build, run, debug, test, and live runtime

These are separate permission categories.

Build means process execution plus possible file writes.

Run means process execution plus runtime output.

Debug means process execution plus attach or control capability.

Test means process execution plus output parsing.

Live runtime means persistent execution session.

REPL means interactive execution session.

Each category needs separate permission, trust, logging, and audit
metadata.

Debug and live runtime are higher risk than simple build.

Attach-to-process is very-high-risk or critical.

## 17. AI command behavior

AI cannot directly execute commands by default.

AI may suggest:

- command plan;
- command explanation;
- risk summary;
- expected file changes;
- expected network access;
- safer alternative;
- dry-run command;
- rollback plan.

User approval is required before execution.

Future AI-assisted execution can be added only with:

- explicit setting;
- Workspace Trust;
- permission grant;
- command preview;
- audit logging;
- dry-run where practical;
- no sudo by default;
- no secrets by default;
- no protected paths by default;
- red critical prompt for dangerous commands.

AI must never hide command execution behind natural language.

## 18. Phone and tablet behavior

Phone and tablet support is limited but useful.

Allowed:

- safe output summaries;
- process status summaries;
- stopped or completed job summaries;
- safe logs summary;
- safe diagnostics summary;
- command preview read-only;
- remote job status later;
- copy safe command;
- open safe log excerpt.

Not allowed by default:

- full terminal;
- local process execution;
- compiler execution;
- interpreter execution;
- package manager install;
- sudo;
- administrator elevation;
- root shell;
- debugger;
- live runtime;
- full unbounded output.

Unsupported actions should be visible as disabled with desktop required.

Phone and tablet must remain secure and ergonomic, not powerless and not
dangerous.

## 19. Performance

Terminal and process execution must not slow the editor core.

Performance rules:

- no terminal startup during normal editor startup;
- lazy process session creation;
- output virtualization;
- output ring buffer;
- bounded log size;
- bounded process count;
- broker isolation;
- no UI thread blocking;
- process tree cleanup;
- crash isolation;
- slow process warnings;
- background job status.

The core editor must stay usable while processes run.

## 20. Security invariants

Required invariants:

- no silent execution;
- no bypass around Permission Broker;
- no bypass around Workspace Trust;
- no raw environment leak;
- no secret injection without explicit approval;
- no hidden shell profile changes;
- no extension auto-sudo;
- no AI auto-sudo;
- no protected path write without approval;
- no untrusted workspace process execution;
- no phone or tablet full local terminal by default;
- no unrestricted output memory growth;
- no unlogged elevated command.

Open UI does not imply data access.

Visible terminal output does not grant AI or extension read access unless
permission allows it.

## 21. Settings

Recommended settings:

- terminal.mode;
- terminal.availableModes;
- terminal.defaultProfile.linux;
- terminal.defaultProfile.macos;
- terminal.defaultProfile.windows;
- terminal.requireWorkspaceTrust;
- terminal.requireCommandPreview;
- terminal.confirmLowRisk;
- terminal.confirmMediumRisk;
- terminal.confirmHighRisk;
- terminal.confirmVeryHighRisk;
- terminal.confirmCritical;
- terminal.allowElevatedExecution;
- terminal.allowSudo;
- terminal.allowAdmin;
- terminal.allowRootShell;
- terminal.allowAiSuggestedCommands;
- terminal.allowAiApprovedExecution;
- terminal.sanitizeEnvironment;
- terminal.redactEnvironment;
- terminal.log.enabled;
- terminal.log.stdout;
- terminal.log.stderr;
- terminal.log.commandPreview;
- terminal.log.environmentSummary;
- terminal.log.retentionDays;
- terminal.log.maxSize;
- terminal.output.maxVisibleLines;
- terminal.output.maxBytes;
- terminal.process.maxConcurrent;
- terminal.process.defaultTimeoutSeconds;
- terminal.showLogLinks;
- terminal.showWorkingDirectoryLinks;
- terminal.phone.showSafeSummaries;
- terminal.tablet.showSafeSummaries.

Recommended defaults:

- terminal.mode is A plus B profile;
- full terminal disabled by default;
- command preview enabled;
- Workspace Trust required;
- environment sanitation enabled;
- elevated execution disabled;
- sudo disabled;
- admin disabled;
- root shell disabled;
- AI direct execution disabled;
- process logs enabled;
- secret redaction enabled;
- phone and tablet full execution disabled.

## 22. Acceptance tests

Future implementation must test:

- default mode has no unrestricted terminal;
- output-only surface can exist without shell launch;
- user can select A, B, C, or D terminal mode;
- mode D still requires guarded execution;
- first shell launch requires approval;
- shell path is visible;
- arguments are visible;
- command preview appears for risky command;
- log ID is visible;
- log file path is clickable;
- working directory path is clickable;
- environment preview is redacted;
- secrets are not injected automatically;
- untrusted root cannot execute process;
- multi-root trust is enforced;
- stdout and stderr are separated;
- large output is bounded;
- process timeout works;
- process tree kill works;
- sudo is disabled by default;
- sudo requires separate approval;
- sudo password is not stored;
- package manager install requires approval;
- AI cannot execute command directly by default;
- phone shows desktop required for full terminal;
- tablet shows desktop required for full terminal;
- audit log records command lifecycle.

Failure conditions:

- extension executes process directly;
- AI executes command silently;
- command runs without preview when preview is required;
- root command runs without critical confirmation;
- sudo password is stored;
- environment leaks secrets;
- untrusted workspace runs compiler;
- package manager runs in untrusted workspace;
- phone runs local compiler;
- tablet runs local package manager;
- output grows without limit;
- process has no log ID;
- elevated command is unlogged.

## 23. v0.1 scope

Included in planning:

- terminal mode model;
- brokered execution model;
- safe default A plus B profile;
- optional basic guarded terminal direction;
- full guarded terminal as user-selectable future capability;
- shell profile visibility;
- command preview;
- environment sanitation;
- working directory policy;
- output routing;
- log ID and log path behavior;
- process lifecycle;
- sudo/admin/root policy;
- package manager policy;
- build/run/debug/test/live runtime category model;
- AI command restrictions;
- phone/tablet safe summaries.

Possible early implementation:

- output-only panel;
- basic guarded terminal shell surface;
- no unrestricted execution;
- command preview skeleton;
- log ID skeleton;
- process session model skeleton;
- settings skeleton.

Excluded from first implementation unless explicitly unlocked later:

- unrestricted terminal;
- silent shell execution;
- AI automatic execution;
- sudo by default;
- root shell by default;
- package manager automation;
- debugger attach;
- full live runtime;
- phone full terminal;
- tablet full terminal.

## 24. Relationship with later topics

Next topic:

NEXT_TOPIC: External toolchain and live runtime broker model

Likely later topics:

- marketplace and package signing details;
- settings sync and account model;
- first implementation milestone freeze.

## External toolchain broker relationship

Terminal and process execution are the lower-level execution surface.
Toolchain Broker adds profile identity, tool role, workspace policy,
output policy, diagnostics policy, Resource Governor policy, production
guard, remote planning, and per-project dashboard behavior. External
toolchains must not bypass the process execution model.
