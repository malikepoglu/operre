# Operre Diagnostics Dashboard Deep Behavior

Status: Accepted specification
Topic ID: OPR-SPEC-0044
Scope: Diagnostics Dashboard, diagnostics item schema, categories,
severity, confidence, sources, AI access, extension providers, visual
layout, filtering, grouping, lifecycle, fix actions, noise control,
retention, privacy, production diagnostics, remote diagnostics planning,
phone and tablet behavior, and first implementation direction.

## 1. Purpose

This document defines Diagnostics Dashboard as a deep project health and
technical control surface.

Diagnostics Dashboard is required.

Diagnostics must help users understand what is happening in a project
without drowning them in raw output, noisy logs, or disconnected errors.

Diagnostics is an interpreted project health surface, not only an error list.

## 2. Surface separation

Operre keeps these surfaces distinct:

- Problems;
- Output;
- Logs;
- Diagnostics;
- Project Dashboard.

Problems is the fast file-oriented issue list.

Output is raw or semi-structured process output.

Logs are event and process records.

Diagnostics is interpreted project health and technical state.

Project Dashboard shows friendly summaries and drill-down entry points.

Diagnostics Dashboard must not become only a larger Problems panel.

## 3. Diagnostics categories

Diagnostics categories include:

- syntax diagnostics;
- compiler diagnostics;
- linker diagnostics;
- runtime diagnostics;
- test diagnostics;
- package diagnostics;
- dependency diagnostics;
- security diagnostics;
- performance diagnostics;
- memory diagnostics;
- CPU diagnostics;
- disk diagnostics;
- network diagnostics;
- port diagnostics;
- database diagnostics;
- migration diagnostics;
- environment diagnostics;
- configuration diagnostics;
- permission diagnostics;
- Workspace Trust diagnostics;
- extension diagnostics;
- AI diagnostics;
- resource diagnostics;
- crash diagnostics;
- flaky test diagnostics;
- production guard diagnostics;
- remote diagnostics later.

The category list may expand as Operre grows.

New categories must remain understandable and not create visual clutter.

## 4. Diagnostics item schema

Each diagnostics item should be structured.

Fields include:

- diagnostic ID;
- title;
- summary;
- details;
- severity;
- category;
- source;
- confidence;
- status;
- first seen;
- last seen;
- count;
- affected file;
- line;
- column;
- workspace root;
- project ID;
- toolchain profile ID;
- process session ID;
- log ID;
- output channel ID;
- related artifact;
- related task;
- related extension;
- related permission;
- related Workspace Trust state;
- related production guard state;
- suggested fix;
- fix risk;
- safe action availability;
- AI access state;
- extension access state;
- redaction state.

Diagnostics items must carry severity and confidence.

The schema may be implemented gradually.

The model must be strong enough to support future real sources.

## 5. Severity model

Severity values include:

- info;
- hint;
- warning;
- error;
- critical;
- blocked;
- security;
- production-critical.

Color may help, but color is not the only meaning.

Every visible item must include:

- icon;
- text;
- severity label;
- accessible label.

Security and production-critical items require stronger visual treatment.

Production-critical items require production guard behavior.

## 6. Confidence model

Confidence values include:

- confirmed;
- likely;
- possible;
- heuristic;
- unknown.

Diagnostics must be honest about certainty.

Compiler errors are usually confirmed.

Dependency age warnings may be likely.

Performance cause guesses may be possible.

Heuristic and unknown diagnostics must not pretend to be facts.

The closer diagnostics are to evidence, the more trustworthy Operre feels.

## 7. Source attribution

Every diagnostics item must show its source.

Sources may include:

- Problems parser;
- Output parser;
- Logs parser;
- Toolchain Broker;
- Resource Governor;
- Workspace Trust Broker;
- Permission Broker;
- extension host;
- AI advisory layer, if allowed;
- build runner;
- test runner;
- package manager;
- database client;
- web development server;
- live runtime session;
- OS platform check;
- remote target later;
- production guard later.

A diagnostic without source attribution is not acceptable.

Source identity helps trust, filtering, debugging, and permission review.

## 8. AI relationship

AI cannot read Diagnostics by default.

AI access requires:

- explicit user permission;
- Workspace Trust where workspace data is involved;
- item-level or category-level scope;
- redaction;
- separate permission for raw logs;
- separate permission for raw output;
- audit logging;
- prompt and response logging off by default.

AI may help with:

- summary;
- cause analysis;
- risk explanation;
- fix suggestion;
- rollback plan;
- test plan;
- setup guidance;
- failure analysis.

AI advisory output is separate from the diagnostic item itself.

Future AI-assisted fix application is a target, but it requires stronger
settings, preview, diff review, command preview, permissions, and audit.

AI must not apply fixes silently.

## 9. Extension diagnostics

Extensions may contribute diagnostics only through declared providers and permissions.

Extensions may contribute:

- diagnostic provider;
- parser;
- category;
- problem matcher;
- safe fix action;
- dashboard card;
- summary provider;
- setup health provider;
- test health provider;
- package health provider.

Extensions must not:

- read other extension diagnostics without permission;
- read raw logs without permission;
- read raw output without permission;
- read secrets;
- spam critical severity;
- create production-critical items without special approval;
- execute commands through diagnostics;
- bypass Toolchain Broker;
- bypass Process Execution Broker;
- bypass Workspace Trust;
- bypass audit logging.

Extension diagnostics are contributions, not unrestricted authority.

## 10. Visual layout

Diagnostics Dashboard should combine:

- health summary;
- cards;
- table;
- detail panel;
- timeline later.

Main areas may include:

- active criticals;
- security issues;
- build status;
- test status;
- toolchain status;
- runtime status;
- dependency status;
- database status;
- migration status;
- resource status;
- recent regressions;
- resolved items;
- ignored items;
- snoozed items.

The detail panel should show:

- explanation;
- source;
- evidence;
- log link;
- output link;
- affected files;
- suggested fix;
- risk;
- history;
- related diagnostics;
- access state;
- redaction state.

The UI must be powerful without becoming confusing.

## 11. Filtering and grouping

Diagnostics Dashboard must provide strong filtering.

Filters include:

- severity;
- category;
- source;
- workspace root;
- file;
- toolchain profile;
- process session;
- time range;
- status;
- confidence;
- production guard;
- extension;
- AI-readable state;
- resolved state;
- snoozed state;
- ignored state.

Grouping includes:

- by category;
- by severity;
- by file;
- by toolchain;
- by session;
- by source;
- by project area;
- by time.

Filtering and grouping must be ergonomic.

Users should not need to fight a wall of noise.

## 12. Lifecycle

Diagnostics lifecycle states include:

- new;
- active;
- acknowledged;
- in progress;
- snoozed;
- ignored;
- resolved;
- reappeared;
- blocked;
- quarantined.

Ignore should be scoped or time-limited when possible.

Critical and production-critical items should not be easy to ignore.

Resolved history may be retained according to privacy and retention
settings.

Reappeared diagnostics should show previous history.

## 13. Fix actions

Diagnostics should help users act safely.

Fix actions may include:

- open file;
- open log;
- open output;
- open settings;
- open toolchain profile;
- open Workspace Trust review;
- open permission review;
- open dependency file;
- create issue later;
- copy command;
- propose command;
- run safe check later;
- apply code fix later;
- rollback suggestion.

Fix actions must not run hidden commands.

Risky fix actions require command preview or diff preview.

Code changes require diff preview.

Command actions require command preview.

Production fixes require production guard.

AI must not directly apply fixes by default.

## 14. Noise control

Diagnostics must control noise.

Noise control includes:

- deduplication;
- grouping;
- rate limits;
- flapping detection;
- flaky test grouping;
- repeated error collapse;
- noisy source warning;
- per-source mute;
- per-category snooze;
- show important only mode;
- beginner mode;
- expert mode.

Poor diagnostics noise creates poor user experience.

Operre should surface what matters first.

## 15. Retention and privacy

Diagnostics history is useful and sensitive.

Default behavior:

- app-local diagnostics history;
- project-local diagnostics only with approval;
- secrets redacted;
- log excerpts limited;
- raw logs require separate permission;
- raw output requires separate permission;
- diagnostics summary export allowed;
- redacted bundle export allowed;
- secrets are never exported by default;
- AI access is separate;
- extension access is separate;
- detailed diagnostics sync is off by default.

Retention settings should be understandable.

Users must be able to clear diagnostics safely.

## 16. Production diagnostics

Production diagnostics are a special class.

Production diagnostics require production guard.

Production diagnostics may include:

- production-critical severity;
- red warning bar;
- explicit target label;
- redaction by default;
- guarded export;
- no AI access by default;
- no extension access by default;
- no command action without approval;
- no destructive fix without multi-step confirmation;
- audit logging;
- rollback guidance when possible.

Production diagnostics must be powerful and conservative.

Production targets must never be treated like local test projects.

## 17. Remote diagnostics planning

Remote diagnostics are planned, disabled by default, and must not be forgotten.

Remote diagnostics later may include:

- remote target trust;
- host identity;
- transport policy;
- remote log redaction;
- remote command separation;
- remote health summary;
- remote resource status;
- remote service status;
- remote database status;
- remote deployment status.

Remote diagnostics skeletons may exist in disabled form.

No remote diagnostics source is active by default.

No remote fix action is allowed by default.

Production guard applies when the remote target is production-like.

## 18. Phone and tablet behavior

Phone and tablet diagnostics should be useful but safe.

Allowed by default:

- health summary;
- critical count;
- safe diagnostic summary;
- redacted details;
- status timeline;
- safe suggested next steps;
- copy issue summary;
- remote status summary later.

Not allowed by default:

- raw logs;
- secret-bearing output;
- run fix;
- run command;
- production action;
- permission grant;
- executable approval.

Phone and tablet UI must be readable, responsive, and not cramped.

Unsupported risky actions show disabled with desktop required.

## 19. Relationship with Project Dashboard

Project Dashboard summarizes diagnostics.

Diagnostics Dashboard provides deep analysis.

Dashboard visibility does not grant access to raw logs, raw output,
secrets, AI context, extension context, or production details.

Open UI does not imply data access.

## 20. Relationship with toolchains

Toolchain diagnostics must reference:

- toolchain profile;
- process session ID;
- log ID;
- output channel ID;
- Resource Governor state;
- permission state;
- Workspace Trust state;
- production guard state where relevant.

Build, run, debug, test, package manager, database, web server, and live
runtime diagnostics remain separate where risk differs.

## 21. Settings

Recommended settings include:

- diagnostics.enabled;
- diagnostics.dashboard.enabled;
- diagnostics.dashboard.defaultOpenMode;
- diagnostics.dashboard.showHealthSummary;
- diagnostics.dashboard.showCriticals;
- diagnostics.dashboard.showSecurity;
- diagnostics.dashboard.showToolchains;
- diagnostics.dashboard.showRuntime;
- diagnostics.dashboard.showResources;
- diagnostics.dashboard.showResolved;
- diagnostics.filters.persist;
- diagnostics.grouping.defaultMode;
- diagnostics.noiseControl.enabled;
- diagnostics.noiseControl.deduplicate;
- diagnostics.noiseControl.flappingDetection;
- diagnostics.noiseControl.showImportantOnly;
- diagnostics.retention.enabled;
- diagnostics.retention.maxAgeDays;
- diagnostics.retention.maxItems;
- diagnostics.retention.appLocalHistory;
- diagnostics.retention.projectLocalHistory;
- diagnostics.privacy.redactionEnabled;
- diagnostics.privacy.rawLogAccessRequiresPermission;
- diagnostics.privacy.rawOutputAccessRequiresPermission;
- diagnostics.ai.readEnabled;
- diagnostics.ai.defaultScope;
- diagnostics.extensions.providersEnabled;
- diagnostics.productionGuard.enabled;
- diagnostics.remote.enabled;
- diagnostics.mobile.safeSummaryMode.

Recommended defaults:

- Diagnostics Dashboard enabled;
- source attribution required;
- confidence shown;
- redaction enabled;
- app-local history;
- project-local detailed history off by default;
- AI diagnostics read off by default;
- extension provider access permission-gated;
- production guard enabled;
- remote diagnostics disabled;
- mobile safe summary mode enabled.

## 22. Acceptance tests

Future implementation must test:

- Diagnostics Dashboard can open;
- diagnostics item schema exists;
- severity is visible;
- confidence is visible;
- source is visible;
- category is visible;
- Problems, Output, Logs, and Diagnostics remain separate;
- AI cannot read Diagnostics by default;
- extension cannot read raw logs by default;
- fix action cannot run hidden command;
- production diagnostics require production guard;
- remote diagnostics remain disabled by default;
- phone shows safe summary;
- tablet shows safe summary;
- raw logs require separate permission;
- raw output requires separate permission;
- redacted export hides secrets;
- grouping works;
- filtering works;
- snooze is scoped;
- ignored critical item remains visible enough;
- noisy source warning works;
- resolved item history is retained only by policy.

Failure conditions:

- diagnostic has no source;
- diagnostic has no severity;
- diagnostic has no confidence;
- AI reads diagnostics silently;
- extension reads diagnostics silently;
- fix runs command silently;
- raw log is exposed on mobile;
- production action runs from diagnostics without guard;
- remote diagnostics activate silently;
- secrets appear in diagnostics export;
- dashboard visibility grants data access.

## 23. v0.1 scope

Included in planning:

- diagnostics item schema skeleton;
- Diagnostics Dashboard skeleton;
- sample diagnostics source for UI testing;
- Problems integration placeholder;
- Output link placeholder;
- Log link placeholder;
- severity model;
- category model;
- confidence model;
- source attribution;
- filter skeleton;
- grouping skeleton;
- lifecycle model;
- redaction model;
- AI access disabled;
- extension provider disabled or permission-gated;
- production diagnostics model;
- remote diagnostics disabled skeleton;
- phone and tablet safe summary model.

First implementation starts with diagnostics schema and dashboard skeleton.

Real toolchain parsing, AI access, extension diagnostics, production
actions, and remote diagnostics should be added later behind the
security model.

## 24. Relationship with later topics

Next topic:

NEXT_TOPIC: Extension marketplace package signing and update distribution behavior

Likely later topics:

- settings sync and account model;
- first implementation milestone freeze.
