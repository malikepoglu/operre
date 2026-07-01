# Operre Managed Works Projects Templates and Dashboard

Status: Accepted specification
Topic ID: OPR-SPEC-0043
Scope: Managed Works projects, external workspaces, Works root,
project folder structure, `.operre` boundaries, templates, template
security, project dashboard, toolchain dashboard relationship, outputs,
logs, artifacts, cleanup, retention, template sharing, project identity,
phone and tablet behavior, safe reset, and first implementation direction.

## 1. Purpose

This document defines how Operre manages projects without becoming a
messy folder writer.

Operre must support both structured Operre-managed projects and existing
external workspaces.

The goal is a powerful, ergonomic, secure, visually clear, and habit
forming project experience.

Managed projects and external workspaces are separate modes.

## 2. Core decision

Operre uses two project modes:

- Operre-managed project;
- external workspace.

Operre-managed projects are created and organized by Operre.

External workspaces are existing user folders or repositories that Operre
opens respectfully.

External workspaces are not modified by default.

Managed projects can use standard structure, templates, dashboards,
toolchain profiles, outputs, logs, artifacts, and project-level settings.

External workspaces use app-local state by default unless the user
approves project-local writes.

## 3. Managed project necessity

Managed projects are required.

They provide:

- predictable structure;
- clear outputs;
- clear logs;
- clear artifacts;
- safer toolchain binding;
- clearer dashboards;
- easier cleanup;
- better snapshots later;
- better diagnostics;
- better AI boundaries later;
- better mobile summaries;
- better user habits.

Operre should not be only a folder opener.

It should also be a structured project platform.

## 4. Works root

The managed Works root setting is:

- operre.worksRoot.

The Works root is user-configurable.

The default should be platform-aware.

The setting must provide reset to recommended default.

The setting must be visible in Settings and project creation flows.

The Works root must not be silently changed by extensions, templates, AI,
or sync.

The Works root may be used by:

- managed project creation;
- project templates;
- output policy;
- log policy;
- artifact policy;
- dashboard discovery;
- project search later.

## 5. Managed project folder structure

Recommended managed project structure:

- ProjectName/.operre;
- ProjectName/src;
- ProjectName/docs;
- ProjectName/outputs;
- ProjectName/logs;
- ProjectName/artifacts;
- ProjectName/tmp.

Folders should not all be created blindly.

Folder creation behavior uses C plus B.

This means:

- template creates required folders;
- other folders are created when needed.

C plus B is the default folder creation behavior.

Users may choose a more explicit behavior in settings.

Template-driven and need-driven creation reduce clutter while preserving
ergonomics.

## 6. Optional structured subfolders

Optional output subfolders include:

- outputs/python;
- outputs/node;
- outputs/cpp;
- outputs/web;
- outputs/database;
- outputs/reports;
- outputs/exports.

Optional log subfolders include:

- logs/app;
- logs/toolchain;
- logs/runtime;
- logs/audit;
- logs/diagnostics;
- logs/security.

Optional artifact subfolders include:

- artifacts/build;
- artifacts/release;
- artifacts/reports;
- artifacts/exports;
- artifacts/packages.

Optional temporary subfolders include:

- tmp/toolchain;
- tmp/runtime;
- tmp/import;
- tmp/export.

These folders are created only when the template or a user-approved
action needs them.

## 7. The `.operre` boundary

The `.operre` folder is protected by default.

Recommended `.operre` structure:

- .operre/project.json;
- .operre/workspace.json;
- .operre/shared;
- .operre/toolchains;
- .operre/tasks;
- .operre/dashboards;
- .operre/cache;
- .operre/local-state;
- .operre/audit;
- .operre/snapshots;
- .operre/secrets.

The `.operre` protected local shared boundaries are required.

The boundary model:

- shareable low-risk metadata;
- explicit shared area;
- local-only state;
- cache-only state;
- audit state;
- snapshots;
- secrets.

`.operre/project.json` may store low-risk project metadata.

`.operre/shared` may store explicit shared project metadata.

`.operre/local-state` is local-only.

`.operre/cache` is local-only.

`.operre/audit` is local-only by default.

`.operre/secrets` is protected, local-only, and never tracked.

Secret files must not be created, read, or synced silently.

## 8. External workspace behavior

External workspaces are existing user projects.

Rules:

- do not create outputs by default;
- do not create logs by default;
- do not create artifacts by default;
- do not create `.operre` by default;
- use app-local spool by default;
- request approval before project-local writes;
- show proposed write scope;
- show cleanup policy;
- show retention policy;
- show owner action;
- show safety impact.

External workspace writes require explicit approval.

External workspace behavior must be respectful and non-invasive.

## 9. Project templates

Project templates are planned from the beginning.

Template categories may include:

- blank text project;
- notes project;
- documents project;
- Python project;
- Node project;
- TypeScript project;
- C project;
- C++ project;
- web app project;
- database project;
- mixed full-stack project;
- documentation project;
- research project;
- AI or ML project later;
- Operre extension project later;
- remote monitored project later.

Templates may become powerful over time.

Templates must remain understandable, previewable, and safe.

## 10. Template security

Templates are declarative and do not execute commands.

Templates may propose:

- folder structure;
- starter files;
- project metadata;
- dashboard layout;
- toolchain profile templates;
- output policy;
- log policy;
- artifact policy;
- recommended settings;
- documentation files;
- setup guide.

Templates must not:

- install packages;
- run commands;
- create secrets;
- open remote connections;
- approve executables;
- approve production profiles;
- approve remote targets;
- change Workspace Trust;
- grant extension permissions;
- bypass safe reset;
- hide generated files.

Template preview is required before creation.

Template application should show:

- folders to be created;
- files to be created;
- settings to be suggested;
- toolchain profiles to be suggested;
- risks;
- rollback or cleanup option where possible.

## 11. Template sharing

Template sharing is later.

Supported planning modes:

- built-in templates;
- local templates;
- first-party templates;
- imported template file;
- private registry later;
- marketplace later.

Shared templates require:

- preview;
- no execution;
- no secrets;
- no install;
- version metadata;
- source metadata;
- trust state;
- signature later;
- safe disable action.

Marketplace templates must be signed later.

Imported templates are untrusted until reviewed.

## 12. Project Dashboard

Project Dashboard is a central project control surface.

The dashboard is the ergonomic front door for a project.

Dashboard sections may include:

- Project Overview;
- Files;
- recent activity;
- Toolchains;
- Tasks;
- Outputs;
- Logs;
- Diagnostics;
- Problems;
- Artifacts;
- Security;
- Workspace Trust;
- Permissions;
- Production Guard;
- Remote Targets later;
- Resource Usage;
- Safe Reset;
- AI assistance later;
- Git later.

Dashboard must remain visually clear.

Dashboard must not become a noisy control wall.

The first view should summarize state and reveal detail progressively.

## 13. Dashboard default behavior

Dashboard default behavior is C plus B.

This means:

- show dashboard on first project open;
- keep dashboard accessible from sidebar or status bar later.

Users may change this behavior in settings.

Possible modes:

- show every time;
- show first time only;
- show when issues exist;
- sidebar access only;
- status bar access only;
- command palette only.

C plus B is the recommended default.

## 14. Dashboard security summary

Dashboard should include a security summary.

It should show:

- Workspace Trust state;
- permission summary;
- toolchain approvals;
- blocked profiles;
- review-needed profiles;
- production guard state;
- remote target state;
- secrets state, redacted;
- risky settings;
- safe reset actions.

Security summary must be understandable.

Security summary must not expose secrets.

Security summary must not imply data access for AI or extensions.

## 15. Project identity

Managed project identity includes:

- project ID;
- project name;
- Works root;
- canonical path;
- local project ID;
- optional repo remote;
- project type;
- template ID;
- created time;
- last opened time;
- device-local state;
- safety metadata;
- dashboard layout profile;
- project capability profile.

External workspace identity includes:

- canonical path;
- workspace roots;
- optional repo remote;
- local workspace ID;
- safety metadata;
- trust state;
- external workspace marker;
- device-local state.

Project identity must support future sync without silently syncing unsafe
approvals.

## 16. Project Dashboard and Toolchains Dashboard

Project Dashboard shows a Toolchains summary.

The detailed Toolchains Dashboard remains a separate surface.

Example summary states:

- Python approved;
- Node review needed;
- C++ missing;
- database blocked;
- web server idle;
- package manager disabled;
- production guard active.

Selecting the summary opens Toolchains Dashboard.

Project Dashboard must not hide dangerous toolchain state.

Toolchains Dashboard remains the deeper tool-specific control surface.

## 17. Outputs, logs, and artifacts UI

Dashboard should show output, log, and artifact state.

It may show:

- latest output;
- latest log;
- latest artifact;
- failed runs;
- large output warnings;
- cleanup actions;
- open folder action;
- open log action;
- open artifact action;
- export summary action;
- pinned artifacts;
- retention state.

Output, log, and artifact UI must be visual, safe, and friendly.

Clicking a path must not grant AI or extension read access.

Open UI does not imply data access.

## 18. Cleanup and retention

Cleanup and retention policy is required.

Settings may include:

- max log age;
- max log size;
- max output size;
- max artifact age;
- max app-local spool size;
- cleanup old temp;
- cleanup failed sessions;
- keep pinned artifacts;
- warn before large cleanup;
- never delete user files without approval.

App-local spool may be cleaned automatically according to policy.

Project artifacts are not deleted without user approval.

Pinned artifacts are protected.

User files must never be deleted silently.

## 19. Phone and tablet behavior

Phone and tablet project views must be useful but safe.

Allowed:

- project overview;
- dashboard summary;
- safe logs summary;
- safe diagnostics summary;
- toolchain status summary;
- outputs summary;
- artifacts summary;
- security summary;
- read-only template preview;
- safe reset preview;
- copy safe command later;
- remote status later.

Not allowed by default:

- local full toolchain execution;
- package install;
- production actions;
- secret reveal;
- full terminal;
- dangerous cleanup;
- executable approval.

Unsupported actions show disabled with desktop required.

Mobile UI must not be cramped.

Mobile UI must not be powerless.

## 20. Public project naming

Special project names stay out of public specification.

Public docs should describe user projects, external systems, staging,
production, databases, monitoring, deployments, and dashboards in generic
terms.

Specific private or strategic project names should remain in private
planning, source review, or user memory unless explicitly approved later.

This protects strategy while keeping the specification useful for all
users.

## 21. Project-level safe reset

Project-level safe reset is mandatory.

Safe reset actions include:

- reset project dashboard layout;
- reset project toolchain settings;
- disable project toolchain execution;
- disable project package managers;
- disable project remote targets;
- disable project production actions;
- reset project trust review state;
- reset risky dashboard settings;
- cleanup app-local spool;
- restore recommended defaults;
- compare with recommended defaults.

Safe reset must keep user files safe.

Safe reset must explain what will change.

Safe reset must not delete user files silently.

## 22. Project dashboard visual ergonomics

Dashboard must create useful habits.

Design requirements:

- readable cards;
- clear status labels;
- no color-only meaning;
- keyboard accessible;
- screen-reader accessible;
- compact mode support;
- high-DPI support;
- phone and tablet layouts;
- progressive disclosure;
- quick actions;
- safe defaults;
- visible risk;
- visible next steps.

Dashboard should help users understand what to do next.

Dashboard should reduce dependency on other editors by making setup,
status, logs, outputs, toolchains, and diagnostics easy to find.

## 23. Settings

Recommended settings include:

- operre.worksRoot;
- projects.defaultMode;
- projects.createManagedByDefault;
- projects.externalWritePolicy;
- projects.folderCreationMode;
- projects.dashboard.defaultOpenMode;
- projects.dashboard.showOnFirstOpen;
- projects.dashboard.sidebarAccess;
- projects.dashboard.statusBarAccess;
- projects.dashboard.showSecuritySummary;
- projects.dashboard.showToolchainsSummary;
- projects.dashboard.showOutputsSummary;
- projects.dashboard.showLogsSummary;
- projects.dashboard.showArtifactsSummary;
- projects.dashboard.showResourceSummary;
- projects.dashboard.showSafeReset;
- projects.templates.enabled;
- projects.templates.allowLocalTemplates;
- projects.templates.allowImportedTemplates;
- projects.templates.allowMarketplaceTemplatesLater;
- projects.templates.requirePreview;
- projects.cleanup.enabled;
- projects.cleanup.maxLogAgeDays;
- projects.cleanup.maxLogBytes;
- projects.cleanup.maxOutputBytes;
- projects.cleanup.maxSpoolBytes;
- projects.cleanup.protectPinnedArtifacts;
- projects.safeReset.enabled;
- projects.mobile.safeSummaryMode.

Recommended defaults:

- managed projects enabled;
- external workspace write policy is ask-first;
- folder creation mode is C plus B;
- dashboard default is C plus B;
- template preview required;
- template execution disabled;
- external workspace `.operre` creation disabled by default;
- app-local spool enabled;
- project artifact deletion requires approval;
- safe reset enabled;
- mobile safe summary mode enabled.

## 24. Acceptance tests

Future implementation must test:

- managed project can be created under Works root;
- Works root can reset to recommended default;
- template creates only required folders;
- need-driven folder creation works;
- external workspace is not modified by default;
- external workspace write requires approval;
- `.operre/secrets` is protected;
- `.operre/local-state` is local-only;
- `.operre/shared` is explicit shared area;
- template preview shows files and folders;
- template cannot execute commands;
- template cannot install packages;
- template cannot approve executables;
- dashboard opens on first project open;
- dashboard remains accessible later;
- security summary hides secrets;
- Toolchains summary links to Toolchains Dashboard;
- outputs summary opens safe output view;
- log path opens in Operre;
- artifact cleanup does not delete pinned artifacts;
- project safe reset restores recommended defaults;
- project safe reset does not delete user files;
- phone shows safe dashboard summary;
- tablet shows safe dashboard summary;
- disabled desktop-required actions are visible;
- public docs do not expose private project names.

Failure conditions:

- external workspace is polluted silently;
- template runs a command;
- template installs a package;
- template grants trust or permissions;
- template creates a secret silently;
- dashboard exposes secrets;
- safe reset deletes user files;
- artifact cleanup deletes pinned artifacts;
- mobile UI allows production action by default;
- extension changes Works root silently;
- AI changes project structure silently.

## 25. v0.1 scope

Included in planning:

- managed project mode;
- external workspace mode;
- operre.worksRoot;
- folder creation C plus B;
- `.operre` boundary;
- template categories;
- template security;
- Project Dashboard;
- Toolchains summary;
- outputs, logs, and artifacts UI;
- cleanup and retention;
- public project naming restraint;
- project-level safe reset;
- phone and tablet safe summaries;
- first implementation direction.

First implementation direction:

- Works root setting;
- create managed project skeleton;
- open external workspace metadata safely;
- basic Project Dashboard skeleton;
- basic Toolchains summary placeholder;
- basic Outputs placeholder;
- basic Logs placeholder;
- basic Diagnostics placeholder;
- no template execution;
- no package install;
- no real toolchain execution yet;
- safe reset placeholder;
- ergonomic setup guidance.

The first implementation should create useful project habits without
violating earlier security rules.

## 26. Relationship with later topics

Next topic:

NEXT_TOPIC: Diagnostics dashboard deep behavior

Likely later topics:

- marketplace and package signing details;
- settings sync and account model;
- first implementation milestone freeze.
