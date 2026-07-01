# Operre Extension Permission UI and Approval Flow

Status: Accepted specification
Topic ID: OPR-SPEC-0039
Scope: Extension permission prompts, install-time summaries, runtime approval, permission duration, scoped grants, risk bars, update policy, local extension warnings, phone and tablet restrictions, sync behavior, revocation, Safe Mode, and audit behavior.

## 1. Purpose

This document defines how Operre asks for, explains, grants, denies, persists, revokes, audits, and displays extension permissions.

The permission UI must be more secure than a silent install model and more ergonomic than repeated technical popups. Users must understand what an extension wants, why it wants it, what data it can access, how long the permission lasts, what device or workspace it applies to, and how to revoke it later.

The permission system must protect Operre, the user's files, workspaces, logs, diagnostics, secrets, AI context, protected paths, and future external toolchain sessions.

## 2. Core decision

Operre uses a two-layer permission approval model:

- install-time permission summary;
- runtime critical permission prompts.

Install-time shows the extension's declared capabilities and risk summary.

Runtime prompts are required for critical actions such as file write, workspace read, protected path access, network access, process execution, external toolchain control, AI access, Logs access, Output access, Search Results access, Problems access, Diagnostics access, secrets access, and environment access.

The default permission model remains deny-by-default.

Open UI does not imply data access.

## 3. Permission prompt timing

### 3.1 Install-time summary

During installation, Operre must show:

- extension identity;
- publisher;
- signature status;
- package source;
- manifest version;
- extension version;
- risk class;
- requested permission categories;
- device support;
- Workspace Trust requirements;
- local or marketplace trust status;
- update policy impact;
- privacy summary;
- whether the extension can run in limited mode.

Install-time approval does not automatically grant every critical permission forever.

### 3.2 Runtime critical prompt

Runtime prompts are required when an extension first attempts a critical operation.

Examples:

- read a workspace folder;
- write a file;
- read Search Results;
- read Problems;
- create or read Output;
- read Logs;
- read Diagnostics;
- access AI context;
- access secrets;
- access protected paths;
- use network;
- start external process;
- start compiler, interpreter, linker, simulator, emulator, database tool, web server, package manager, executable builder, or live runtime.

Runtime prompts must show the exact requested action and scope.

## 4. Permission duration

Supported grant durations:

- deny;
- allow once;
- allow for this session;
- allow for this workspace;
- allow for this machine;
- allow until extension update;
- allow until revoked.

Risky permissions should default to allow once or allow for this session.

Very-high-risk permissions should make persistent grants harder to choose.

Examples of very-high-risk permissions:

- process execution;
- terminal-like access;
- compiler execution;
- interpreter execution;
- C or C++ build;
- Python runtime;
- Node runtime outside sandbox;
- debugger;
- secrets;
- protected paths;
- unrestricted network;
- AI data access;
- Logs read;
- Diagnostics read;
- environment variables.

## 5. Permission scope

Permission grants must support scoped approval.

Supported scope types:

- exact file;
- folder;
- workspace;
- workspace subfolder;
- file extension;
- glob pattern;
- language mode;
- command ID;
- panel ID;
- output channel;
- diagnostics session;
- problem source;
- search query/session;
- network domain;
- network URL pattern;
- executable path;
- toolchain profile;
- AI session;
- secret name, later and very restricted.

Examples:

- read this file only;
- read this folder only;
- read workspace files matching a glob;
- write only generated output folder;
- network only to a declared domain;
- run only a configured executable;
- read Diagnostics summary only;
- read Output channel owned by the same extension only.

Broad grants must be visibly more severe than narrow grants.

## 6. Risk levels

Risk levels:

- Low;
- Medium;
- High;
- Very High;
- Critical.

Examples:

- Low: theme, icon theme, snippets, syntax grammar.
- Medium: commands, menus, views, status item, simple formatter.
- High: file write, workspace search, diagnostics contribution, output channel contribution.
- Very High: process execution, network with workspace data, AI access, Logs read, Diagnostics read, protected path access.
- Critical: secrets access, unrestricted process execution, terminal-like access, debugger control, untrusted local extension with dangerous permissions, external toolchain execution in an untrusted workspace.

Risk must be shown in clear language, not only as an icon or color.

## 7. Risk bars and user-facing warnings

### 7.1 Placement

Important extension permission warnings must appear as a horizontal bar below the toolbar and above the editor or working surface.

This placement is intentional. The user should see the warning before continuing work, similar to an office-style security warning bar, without hiding the entire interface unless the situation is critical.

### 7.2 Severity bar types

Required bar types:

- Info bar;
- Warning bar;
- Critical alert bar.

Info bar behavior:

- used for low-risk informational state;
- blue-like default theme token;
- can be dismissed;
- remains available from status bar after dismissal when relevant.

Warning bar behavior:

- used for medium or high risk;
- yellow-like default theme token;
- requires clear user decision;
- must not auto-dismiss;
- close button only hides the bar after the user acknowledges the warning where required;
- status bar keeps a visible summary after dismissal.

Critical alert bar behavior:

- used for very-high-risk or critical actions;
- red-like default theme token;
- may block the action until the user explicitly confirms;
- must require an "I understand" style acknowledgement before dangerous continuation;
- must not disappear automatically;
- status bar keeps a persistent critical summary until resolved or revoked.

### 7.3 Accessibility and customization

Bars must not rely on color alone.

Each bar must include:

- severity label;
- icon;
- readable text;
- technical permission ID where relevant;
- user-friendly explanation;
- action buttons;
- accessible label;
- keyboard focus behavior;
- screen reader text;
- status bar fallback.

Colors must be user-customizable through theme or settings.

Custom colors must preserve contrast and accessibility requirements.

### 7.4 Close and persistence behavior

A permission risk bar must not silently vanish.

If dismissed:

- the decision must be recorded;
- the status bar must show a compact permission state;
- the user can reopen details;
- unresolved critical state remains visible;
- dismissed does not mean allowed;
- allowed does not mean unlimited.

## 8. Permission language

Permission UI must show both technical permission name and user-friendly explanation.

Required fields:

- extension name;
- publisher;
- permission ID;
- risk level;
- requested action;
- requested scope;
- requested duration;
- reason declared by extension;
- data that may be accessed;
- data that will not be accessed;
- whether Workspace Trust is required;
- whether the grant is synced;
- where to revoke later.

Example:

    Permission: workspace.read
    This extension wants to read files in the current workspace.
    Scope: /home/mak/dev/example-project/**/*.md
    Risk: Medium
    Duration: This workspace only
    Reason declared by extension: Format Markdown documents.
    Revoke later: Settings > Extensions > Permissions

## 9. Update permission policy

Extension updates must not silently gain dangerous new permissions.

Supported update policies:

- A: allow all update permission changes automatically;
- B: block or keep extension disabled when new permissions are requested until the user approves;
- C: allow low-risk permission changes automatically but require approval for risky changes;
- D: require manual approval for every update.

Default policy:

- B.

Extension update policy B is the default and recommended reset behavior.

Recommended default reset must restore policy B.

Policy A is not recommended and must show a warning before enabling.

Policy changes must be machine-local by default.

## 10. Permission sync

Extension list can sync later. Permission grants should not sync by default.

Syncable:

- extension ID;
- enabled or disabled state, if safe;
- version preference;
- theme;
- keybindings;
- safe extension settings.

Machine-local or workspace-local:

- file grants;
- folder grants;
- workspace grants;
- process execution grants;
- network grants;
- AI access grants;
- protected path grants;
- secrets grants;
- Logs grants;
- Diagnostics grants;
- local toolchain paths;
- executable paths;
- debugger paths;
- environment grants;
- Workspace Trust decisions.

Every machine should re-evaluate risky grants.

This prevents a permission approved on one desktop from silently becoming active on a laptop, tablet, phone, or shared machine.

## 11. Local and unpacked extension installation

Local or unpacked extension installation requires Developer Mode.

Local extension states:

- unpacked local folder;
- packaged local extension;
- signed local package;
- unsigned local package;
- development-mode path.

Rules:

- local unpacked extension is unverified by default;
- unsigned package must show a strong warning;
- local path must be visible;
- manifest diff must be reviewable;
- requested permissions must be shown;
- dangerous permissions require runtime confirmation;
- user can trust this local extension for this machine;
- local trust does not sync;
- local extension cannot silently become marketplace-trusted later.

Developer Mode must be clear but not painful for legitimate developers.

## 12. Phone and tablet permission UI

Phone and tablet support is intentionally limited.

Unsupported capabilities must remain visible as disabled items where useful.

Disabled items should show:

- capability name;
- disabled state;
- reason;
- "desktop required" label;
- short explanation.

Phone and tablet allowed early:

- theme;
- icon theme;
- syntax grammar;
- snippets;
- safe read-only helper;
- limited Problems summary;
- limited Search Results summary;
- safe Diagnostics summary.

Phone and tablet not allowed by default:

- process execution;
- terminal-like access;
- compiler execution;
- interpreter execution;
- linker;
- debugger;
- emulator;
- simulator;
- database server tools;
- web development server;
- executable builder;
- full Output streaming;
- unbounded Logs;
- unrestricted Diagnostics;
- secrets;
- protected path access.

Phone and tablet should not provide a degraded desktop experience. Unsupported high-risk actions should be clearly disabled rather than hidden or forced into a cramped UI.

## 13. Revocation and emergency controls

Operre must provide a full permission dashboard.

Required controls:

- view all permissions by extension;
- view all permissions by workspace;
- view all high-risk grants;
- revoke one grant;
- revoke all grants for an extension;
- disable extension;
- disable all third-party extensions;
- enter Safe Mode;
- reset extension permissions;
- block extension;
- uninstall extension;
- open audit log;
- export safe permission summary.

Safe Mode must disable third-party extensions where needed.

Crash loops or repeated suspicious permission requests can trigger automatic suspension.

## 14. Audit log

Permission audit events should include:

- permission requested;
- permission granted;
- permission denied;
- permission expired;
- permission revoked;
- permission scope changed;
- update requested new permission;
- local extension trusted;
- local extension blocked;
- extension disabled;
- Safe Mode enabled;
- process execution requested;
- network access requested;
- protected path access requested;
- AI access requested;
- Logs access requested;
- Diagnostics access requested;
- secrets access requested.

Audit logs must not include secrets, full file contents, full prompts, full responses, or unredacted protected paths by default.

## 15. Runtime enforcement

Permission UI is not the security boundary by itself.

Actual enforcement must happen through:

- Permission Broker;
- Extension Host API bridge;
- Workspace Trust Broker;
- Device Capability Resolver;
- Package Verifier;
- Process Execution Broker later;
- Toolchain Broker later;
- Audit Log.

Extensions cannot bypass permission prompts by using hidden UI state.

Extensions cannot treat visible panel content as readable data unless data permission is granted.

## 16. Settings

Recommended settings:

- extensions.permissions.updatePolicy;
- extensions.permissions.showInstallSummary;
- extensions.permissions.runtimePromptsEnabled;
- extensions.permissions.defaultDurationLowRisk;
- extensions.permissions.defaultDurationMediumRisk;
- extensions.permissions.defaultDurationHighRisk;
- extensions.permissions.defaultDurationVeryHighRisk;
- extensions.permissions.allowPersistentVeryHighRisk;
- extensions.permissions.syncGrants;
- extensions.permissions.localDeveloperMode;
- extensions.permissions.warnOnUnsignedLocalPackage;
- extensions.permissions.showDisabledDesktopRequiredCapabilities;
- extensions.permissions.showStatusBarSummary;
- extensions.permissions.showRiskBars;
- extensions.permissions.requireAcknowledgeForCritical;
- extensions.permissions.recommendedDefaultsProfile.

Recommended defaults:

- update policy B;
- runtime prompts enabled;
- show install summary enabled;
- sync grants disabled;
- Developer Mode disabled;
- unsigned package warning enabled;
- disabled desktop-required capabilities visible;
- status bar summary enabled;
- risk bars enabled;
- critical acknowledgement required.

## 17. Acceptance tests

Future implementation must test:

- install-time summary appears;
- runtime prompt appears for file read;
- runtime prompt appears for file write;
- runtime prompt appears for network;
- runtime prompt appears for process execution;
- runtime prompt appears for AI access;
- runtime prompt appears for Logs;
- runtime prompt appears for Diagnostics;
- runtime prompt appears for protected path;
- risk bar appears below toolbar and above editor;
- warning bar does not auto-dismiss;
- critical alert requires acknowledgement;
- dismissed warning leaves status bar summary;
- colors can be customized without losing contrast;
- update policy B blocks new permissions by default;
- update policy reset returns to B;
- local unpacked extension requires Developer Mode;
- unsigned local package shows warning;
- phone shows unsupported risky permissions as disabled desktop required;
- tablet shows unsupported risky permissions as disabled desktop required;
- revoke all permissions works;
- Safe Mode disables third-party extensions;
- audit log records permission events;
- open UI does not imply data access.

Failure conditions:

- extension gains new permission silently;
- dangerous permission persists without user choice;
- phone enables desktop-only process execution;
- tablet enables terminal-like execution by default;
- dismissed critical warning leaves no visible trace;
- color-only warning meaning;
- extension reads panel content without permission;
- permission grant syncs to another machine silently;
- unsigned local extension appears trusted;
- extension bypasses Permission Broker.

## 18. v0.1 scope

Included in planning:

- install-time permission summary;
- runtime critical prompts;
- risk classification;
- warning bars;
- critical alert bars;
- status bar summaries;
- permission duration model;
- scoped permission grants;
- update policy model;
- default update policy B;
- permission dashboard direction;
- local extension Developer Mode warning;
- phone and tablet disabled capability display;
- audit event model;
- sync restriction model.

Excluded from v0.1 implementation:

- public marketplace permission automation;
- full process execution UI;
- full Toolchain Broker UI;
- full AI connector permission UI;
- secrets manager UI;
- organization policy management;
- remote admin policy;
- enterprise policy;
- phone full extension permissions;
- tablet full extension permissions.

## 19. Relationship with later topics

Next topic:

NEXT_TOPIC: Workspace Trust deep behavior

Likely later topics:

- safe terminal and process execution model;
- toolchain and live runtime broker model;
- marketplace and package signing details;
- settings sync and account model;
- first implementation milestone freeze.

## Workspace Trust relationship

Extension permission prompts must respect Workspace Trust. A permission grant does not bypass Workspace Trust. Dangerous operations such as process execution, AI workspace access, protected path access, network access with workspace data, diagnostics access, and external toolchain sessions require both appropriate permission and appropriate trust state.

## Terminal permission relationship

Terminal and process execution permissions are separate from generic
extension permissions. Risky commands require runtime prompts, command
preview, duration choice, trust checks, output/log routing, and audit
logging. Sudo, administrator, root, package manager, debugger, live
runtime, and external toolchain permissions are high-risk or critical.

## Toolchain permission relationship

Toolchain permissions are scoped and role-specific. Python interpreter,
C compiler, C++ compiler, linker, package manager, database client,
NoSQL client, web server, migration tool, live runtime, simulator,
emulator, remote toolchain, and production action permissions must be
separate where risk differs.

## Diagnostics permission relationship

Diagnostics permissions should separate summary access, item access, raw
log access, raw output access, production diagnostic access, remote
diagnostic access, AI diagnostic access, and extension provider access.
Higher-risk categories require stronger prompts and clearer scope.

## Extension update permission diff relationship

Extension updates must show new, removed, and changed permissions,
contribution points, commands, toolchain templates, network requests,
file access requests, AI access requests, diagnostics access requests,
and package manager or toolchain risks. Updates with new permissions
become pending or disabled until approved.
