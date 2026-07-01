# Operre Workspace Trust Deep Behavior

Status: Accepted specification
Topic ID: OPR-SPEC-0040
Scope: Workspace Trust timing, trust scope, identity, restricted mode,
multi-root behavior, extension relationship, external toolchain trust,
live runtime trust, device limits, trust review, warning bars, status bar
state, security, performance, and ergonomics.

## 1. Purpose

This document defines Operre's deep Workspace Trust behavior.

Workspace Trust protects users from unsafe workspace content, unsafe
extensions, unsafe local packages, unsafe external tools, accidental code
execution, data exfiltration, protected path exposure, secret exposure,
and unsafe AI or diagnostic access.

Workspace Trust must not make the editor unusable. Basic editing should
continue in restricted mode. Dangerous operations should remain locked
until the user grants scoped trust.

## 2. Core decision

Workspace Trust is scoped, explainable, revocable, device-local,
workspace-aware, extension-aware, and toolchain-aware.

Workspace Trust uses both opening-time trust bars and runtime prompts for
dangerous operations.

Trust is not a single global yes-or-no switch.

Trust must be visible, understandable, scoped, revocable, and enforced by
brokers. A visible UI state alone is not the security boundary.

## 3. Trust timing

Operre uses both opening-time and runtime trust decisions.

When a workspace opens, Operre may show a trust bar below the toolbar and
above the editor or working surface.

The user can keep working in restricted mode.

When a dangerous action is attempted, Operre must ask again through a
runtime trust prompt if required.

Examples of dangerous actions:

- process execution;
- terminal-like access;
- build;
- run;
- debug;
- compiler execution;
- interpreter execution;
- package manager execution;
- external toolchain action;
- live runtime session;
- AI workspace read;
- protected path access;
- secrets access;
- network access with workspace data;
- untrusted local extension activation.

## 4. Trust scope

Trust decisions must be granular.

Supported scopes:

- this file;
- this folder;
- this workspace;
- one root in a multi-root workspace;
- this extension in this workspace;
- this toolchain profile;
- this executable path;
- this machine, with strong warning;
- global trust, unavailable by default or strongly discouraged.

Global trust is unavailable by default or strongly discouraged.

Broad trust must be visually riskier than narrow trust.

## 5. Untrusted workspace behavior

Untrusted workspaces keep basic editing available while code execution,
data exfiltration, AI workspace access, and external toolchain actions
remain locked.

Allowed in restricted mode:

- open file;
- read visible file;
- edit file;
- save file;
- syntax highlighting;
- safe find;
- safe search with restricted scope;
- safe Problems summary;
- safe File Info;
- safe Markdown preview with scripts and network disabled;
- low-risk theme, icon, syntax, and snippet extensions.

Locked in restricted mode:

- terminal;
- process execution;
- build;
- run;
- debug;
- compiler;
- interpreter;
- linker;
- package manager;
- simulator;
- emulator;
- executable builder;
- database tool;
- web development server;
- live runtime;
- AI workspace read;
- extension workspace scan;
- extension file tree read;
- protected path access;
- secrets access;
- unrestricted diagnostics;
- Logs read;
- Output read;
- network access with project data;
- automatic tasks;
- automatic code execution.

## 6. Trust identity

Workspace identity should use:

- canonical path;
- workspace roots;
- optional repository remote summary;
- local workspace ID;
- device-local trust record;
- root folder list;
- symlink state;
- protected path state;
- owner and permission summary;
- last seen safety metadata.

Trust identity must not require hashing all files by default.

Full workspace hashing is expensive, privacy-sensitive, and unnecessary
for the default model.

## 7. Trust states

Required trust states:

- trusted;
- untrusted;
- restricted;
- trust review needed;
- partially trusted;
- revoked;
- blocked.

Trust review needed can appear when meaningful risk changes occur.

Examples:

- new extension requests risky permission;
- local extension path changes;
- package signature changes;
- workspace roots change;
- repository remote changes;
- symlink or protected path state changes;
- toolchain profile changes;
- executable path changes;
- project config starts requesting process execution;
- diagnostics or AI access scope changes.

Trust review needed should show a bar and status bar state.

## 8. Multi-root workspace behavior

Multi-root workspaces track trust per root.

Trusting one root does not trust other roots.

Example behavior:

- one root can be trusted;
- one root can be restricted;
- one root can be blocked;
- one root can require review.

Cross-root operations must respect the least trusted involved root.

An extension cannot use a trusted root to read an untrusted root.

## 9. Extension relationship

Extension trust depends on several checks:

- extension package verification;
- extension identity;
- extension signature;
- extension requested permissions;
- workspace trust state;
- extension limited-mode declaration;
- user permission grants;
- device capability;
- audit state.

Low-risk extensions may run in restricted mode with limited capability.

Medium-risk extensions may contribute UI but cannot read data without a
permission grant.

High-risk and very-high-risk extensions require Workspace Trust where
workspace data, process execution, AI access, diagnostics, logs, protected
paths, or external tools are involved.

Workspace Trust does not automatically grant all extension permissions.

Extension permission grants do not replace Workspace Trust.

## 10. External toolchain and live runtime trust

External toolchain and live runtime require:

- workspace trust;
- verified extension;
- approved toolchain profile;
- approved executable path;
- argument review;
- sanitized environment;
- output redaction;
- resource limits;
- timeout;
- process tree termination;
- audit logging;
- visible trust state;
- user-visible failure state.

This applies to:

- C compiler;
- C++ compiler;
- Python interpreter;
- JavaScript or Node runtime;
- TypeScript tools;
- database tools;
- web development server;
- package manager;
- linker;
- simulator;
- emulator;
- executable builder;
- live runtime;
- REPL;
- debugger later.

Operre should act as a safe coordinator or remote-control surface for
license-compatible external tools.

Operre must not become an uncontrolled execution shell.

## 11. Trust bars and status state

Workspace trust warnings can use red critical, yellow warning, and
light-blue info bars.

Trust bars appear below the toolbar and above the editor or working
surface.

Required bar types:

- info trust bar;
- warning trust bar;
- critical trust bar.

Bars must include:

- severity label;
- icon;
- readable text;
- short reason;
- trust scope;
- current state;
- action buttons;
- accessible label;
- keyboard focus support;
- status bar fallback.

Bars must not rely on color alone.

Colors must be user-customizable but must preserve contrast.

Dismissing a bar does not grant trust.

Dismissing a bar leaves status bar summary where relevant.

Critical trust states require acknowledgement before dangerous
continuation.

## 12. Manage Workspace Trust panel

Operre should provide a Manage Workspace Trust view.

It should show:

- current workspace trust state;
- root trust states;
- extension trust effects;
- locked capabilities;
- allowed capabilities;
- pending trust reviews;
- toolchain trust state;
- local extension trust state;
- permission relationship;
- revoke actions;
- reset trust action;
- audit summary.

The panel should explain why a feature is locked.

## 13. Phone and tablet limits

Phone and tablet trust behavior is stricter.

Unsupported risky trust actions are shown as disabled with desktop
required.

Phone and tablet should not enable:

- local process execution;
- terminal-like access;
- compiler execution;
- interpreter execution;
- C or C++ build;
- Python runtime;
- Node runtime outside sandbox;
- debugger;
- full Output streaming;
- unbounded Logs;
- unrestricted Diagnostics;
- external toolchain sessions;
- live runtime sessions;
- executable builders.

Phone and tablet may allow:

- safe editing;
- safe syntax features;
- safe theme and snippets;
- limited Problems summary;
- limited Search Results summary;
- safe Diagnostics summary.

Phone and tablet must not force a cramped desktop trust UI.

## 14. Sync behavior

Trust decisions must not sync by default.

Workspace Trust is machine-local.

Reasons:

- paths differ across machines;
- same path can contain different content;
- shared machines need separate decisions;
- phone and tablet have different risk limits;
- trust on one device must not silently authorize another device.

Sync can later remember safe preferences, but not risky trust grants.

Enterprise or organization policy is a later topic.

## 15. Performance rules

Workspace Trust must be fast.

Required performance rules:

- no full workspace hash scan by default;
- lazy trust review;
- cheap identity checks first;
- file watcher changes summarized;
- root trust state cached locally;
- no blocking editor startup on deep scans;
- no recursive protected path scan unless required;
- trust review should explain what changed.

The editor must remain usable while trust state is evaluated.

## 16. Data protection rules

Workspace Trust must protect:

- user files;
- unsaved buffers;
- secrets;
- protected paths;
- logs;
- diagnostics;
- AI prompts;
- AI responses;
- output;
- search results;
- Problems records;
- external tool output;
- environment variables.

Open UI does not imply data access.

Visible workspace content does not grant extension or AI access.

## 17. Revocation and emergency behavior

Required controls:

- revoke workspace trust;
- revoke root trust;
- revoke extension trust effect;
- revoke toolchain profile trust;
- block executable path;
- reset workspace trust;
- enter Restricted Mode;
- enter Safe Mode;
- disable third-party extensions;
- stop pending toolchain sessions;
- open audit log.

Revocation must take effect before new dangerous actions continue.

Running external processes must be stopped or isolated according to the
later process execution model.

## 18. Audit behavior

Audit events should include:

- workspace opened;
- trust bar shown;
- trust granted;
- trust denied;
- trust revoked;
- trust review needed;
- root trust changed;
- extension limited mode used;
- risky operation blocked;
- dangerous operation approved;
- toolchain profile approved;
- executable path approved;
- AI workspace access blocked;
- protected path access blocked;
- Safe Mode entered;
- Restricted Mode entered.

Audit logs must not include secrets or full file contents by default.

## 19. Settings

Recommended settings:

- workspace.trust.enabled;
- workspace.trust.showOpeningBar;
- workspace.trust.promptOnDangerousAction;
- workspace.trust.defaultState;
- workspace.trust.allowMachineTrust;
- workspace.trust.allowGlobalTrust;
- workspace.trust.syncTrust;
- workspace.trust.showStatusBarState;
- workspace.trust.showReviewNeeded;
- workspace.trust.showDisabledDesktopRequired;
- workspace.trust.requireAcknowledgeForCritical;
- workspace.trust.redactPathsInWarnings;
- workspace.trust.recheckOnRootChange;
- workspace.trust.recheckOnRemoteChange;
- workspace.trust.recheckOnToolchainChange.

Recommended defaults:

- enabled;
- opening bar enabled;
- runtime prompt enabled;
- global trust disabled;
- sync disabled;
- status bar state enabled;
- review needed enabled;
- desktop-required disabled capabilities visible;
- critical acknowledgement required.

## 20. Acceptance tests

Future implementation must test:

- opening untrusted workspace shows trust bar;
- dangerous action triggers runtime prompt;
- basic editing works in restricted mode;
- process execution is locked in untrusted mode;
- AI workspace read is locked in untrusted mode;
- protected path access is locked;
- extension workspace scan is locked;
- trusted root does not trust another root;
- trust review needed appears after root change;
- trust review needed appears after toolchain path change;
- status bar keeps trust state;
- dismissed bar does not grant trust;
- trust revocation blocks later dangerous actions;
- phone shows desktop-required disabled actions;
- tablet shows desktop-required disabled actions;
- no trust decision syncs silently;
- external toolchain requires full approval chain;
- open UI does not imply data access.

Failure conditions:

- global trust silently enabled;
- extension reads untrusted root through trusted root;
- toolchain starts without workspace trust;
- AI reads workspace without trust;
- trust grant syncs to another machine silently;
- dismissed warning removes all visible state;
- untrusted local extension runs dangerous code;
- phone enables desktop-only toolchain action;
- editor startup blocks on full workspace hashing.

## 21. v0.1 scope

Included in planning:

- trust timing;
- trust scope;
- trust identity;
- restricted mode;
- multi-root trust;
- extension relationship;
- external toolchain trust chain;
- trust bars;
- status bar trust state;
- phone and tablet limits;
- no trust sync default;
- trust review needed;
- revocation and Safe Mode relationship;
- audit event model.

Excluded from v0.1 implementation:

- full terminal implementation;
- full process execution broker;
- full toolchain broker;
- full live runtime broker;
- enterprise policy;
- organization trust policy;
- public marketplace trust automation;
- remote workspace provider trust.

## 22. Relationship with later topics

Next topic:

NEXT_TOPIC: Safe terminal and process execution model

Likely later topics:

- toolchain and live runtime broker model;
- marketplace and package signing details;
- settings sync and account model;
- first implementation milestone freeze.

## Safe terminal relationship

Terminal and process execution require Workspace Trust when workspace
data, external tools, build, run, debug, package managers, live runtime,
or elevated execution are involved. Trust does not execute anything by
itself. Execution still requires permission, command preview, broker
approval, audit logging, and process lifecycle control.

## External toolchain trust relationship

External toolchains require Workspace Trust when workspace data, file
writes, network, secrets, protected paths, production targets, remote
targets, or live runtime sessions are involved. Trust alone does not
approve a toolchain profile. Toolchain profile approval, permissions,
Resource Governor policy, and audit logging are still required.
