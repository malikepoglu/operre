# Operre Problems, Search Results, Output, Logs, and Diagnostics Panel Behavior

Status: Accepted specification
Topic ID: OPR-SPEC-0037
Scope: Problems panel, Search Results panel, Output panel, Logs panel, Diagnostics panel, structured diagnostics, safe output channels, device-specific capability limits, privacy, redaction, and future Visual Studio-grade diagnostic depth.

## 1. Purpose

This document defines detailed behavior for the Problems, Search Results, Output, Logs, and Diagnostics panel family.

Operre must not treat these panels as simple text dump areas. These panels are operational surfaces. They can guide the user, help troubleshoot issues, reveal security state, explain extension failures, and later support build, test, runtime, and debugging workflows.

They are also high-risk privacy surfaces. They may contain paths, snippets, errors, command output, extension messages, stack traces, environment summaries, crash metadata, build output, diagnostic bundles, and later compiler or runtime data. Therefore these panels must be designed with structure, redaction, permission boundaries, and device-specific limits from the beginning.

## 2. Product direction

Operre should learn from useful VS Code behavior:

- Problems panel for structured errors and warnings;
- Search Results panel with grouped matches;
- Output channels;
- Logs and diagnostics commands;
- problem matchers;
- extension-contributed diagnostics;
- command palette integration.

Operre should go further than VS Code in privacy and diagnostic clarity, and may approach Visual Studio-like depth on desktop/workstation platforms over time:

- structured output sessions;
- build/test/runtime diagnostic sessions;
- correlated logs, problems, output, and diagnostics;
- safe diagnostic bundles;
- timeline views;
- issue snapshots;
- redaction previews;
- local-first troubleshooting profiles;
- richer problem source metadata;
- future build and test summary dashboards;
- future extension and runtime health reports.

This extra depth is not for every device. Phone and tablet modes must remain limited and safe.

## 3. Platform capability tiers

### 3.1 Desktop and workstation tier

Desktop and workstation platforms may support the full future model:

- Problems;
- Search Results;
- Output channels;
- Logs;
- Diagnostics;
- diagnostic sessions;
- build/test/runtime output later;
- structured problem matching later;
- local diagnostic bundles;
- extension diagnostics;
- future Visual Studio-like diagnostic depth.

This tier is appropriate for Linux desktop, Windows desktop, macOS desktop, large laptops, and external monitor setups.

### 3.2 Laptop and MacBook tier

Laptop and MacBook behavior should be close to desktop, but more density-aware:

- panels can be tabbed or stacked;
- vertical space must be conserved;
- trackpad ergonomics matter;
- MacBook safe area and native chrome constraints must be respected;
- panel toolbar controls must scale with UI scale.

### 3.3 Tablet tier

Tablet support must be limited and ergonomic:

- Problems can show safe summaries and syntax-like issues;
- Search Results can show limited grouped results;
- Logs can show safe summaries only by default;
- Diagnostics can show a restricted health summary;
- Output streaming, build output, runtime output, debug console, terminal output, and unbounded logs are not v0.1 tablet features;
- panels can become drawers, full-screen sheets, or stacked routes;
- touch targets must be large;
- on-screen keyboard must not hide filter inputs.

Tablet can later connect to a trusted desktop or remote development host, but local tablet core must not pretend to be a full workstation.

### 3.4 Phone tier

Phone support is future-facing and very limited:

- no full desktop panel grid;
- no full Output panel by default;
- no build/run/debug/runtime output by default;
- Problems may show a compact card list;
- syntax validation and lightweight file warnings may be allowed;
- Search Results may show limited file-level matches;
- Diagnostics may show local app health and safe summary only;
- logs are summarized and redacted;
- advanced diagnostic bundle generation is desktop/workstation only unless explicitly designed later.

Phone UI must avoid tables, tiny columns, pixel-perfect tapping, and dense toolbar controls.

## 4. Problems panel

### 4.1 Purpose

Problems panel answers:

- what is wrong;
- where it is wrong;
- how severe it is;
- whether it blocks work;
- whether it is a security or privacy issue;
- which command or setting can fix it;
- whether the details are redacted.

### 4.2 Problem sources

v0.1 sources:

- settings validation;
- keybindings validation;
- workspace trust restrictions;
- file open/save/reload failures;
- external file change conflicts;
- protected path restrictions;
- search and replace warnings;
- large file mode warnings;
- diagnostics collection warnings;
- logs and diagnostics export warnings;
- extension shell problems where safe.

Later sources:

- compiler diagnostics;
- interpreter diagnostics;
- linter diagnostics;
- type checker diagnostics;
- test failures;
- build failures;
- runtime exceptions;
- debugger issues;
- AI action problems;
- remote development issues.

### 4.3 Problem record model

A problem record should include:

- stable problem ID;
- source;
- source kind;
- severity;
- title;
- safe message;
- detailed message, optional and redacted;
- file identity, optional;
- path display form;
- range, optional;
- related command ID;
- related setting key, optional;
- related extension ID, optional;
- timestamp;
- session ID;
- correlation ID;
- privacy classification;
- redaction state;
- trust requirement;
- fix availability;
- copy-safe details.

### 4.4 Severity model

Required severities:

- Error;
- Warning;
- Info;
- Hint;
- Security;
- Privacy.

Security and Privacy severities must not be hidden by ordinary filters unless the user explicitly chooses to hide them. Dangerous hiding should require clear wording.

### 4.5 Fix actions

Problems may expose fix actions:

- open setting;
- reset setting;
- open file;
- reveal in Explorer;
- show File Info;
- show Workspace Trust;
- open Logs;
- open Diagnostics;
- copy safe details;
- ignore once, where safe;
- ignore source, where safe.

Fix actions must use the central command registry.

## 5. Search Results panel

### 5.1 Purpose

Search Results panel shows current file and workspace search results.

It must respect hidden file, protected path, binary file, generated file, large file, and permission policy.

### 5.2 Search result model

Search result entries should include:

- query ID;
- search scope;
- file identity;
- path display form;
- match range;
- preview text, redacted where needed;
- line number;
- match count;
- file match count;
- stale state;
- restriction state;
- large file state;
- generated/binary exclusion reason;
- source of result.

### 5.3 Result states

Required states:

- complete;
- partial;
- streaming;
- canceled;
- truncated;
- restricted;
- stale;
- failed;
- redacted.

### 5.4 Large result handling

Search Results must support:

- virtualized lists;
- grouped results;
- result count limits;
- preview length limits;
- cancellation;
- rerun;
- collapse all;
- expand all;
- copy safe summary;
- no unbounded DOM rendering;
- no full secret dump in previews.

### 5.5 Replace relationship

Replace in files must require:

- preview;
- confirmation;
- file count summary;
- match count summary;
- protected path exclusion by default;
- clear undo/recovery relationship where practical;
- no silent overwrite of dirty buffers.

## 6. Output panel

### 6.1 Purpose

Output panel is a structured channel surface, not an unrestricted text dump.

It may later support Visual Studio-like richness on desktop/workstation platforms, including build output, test output, extension output, runtime output, debugger-adjacent output, task output, and structured run sessions.

### 6.2 v0.1 Output scope

v0.1 Output panel should be basic and safe:

- core operation summaries;
- safe internal channel messages;
- diagnostics collection summaries;
- extension shell messages, when permission-scoped;
- no terminal output;
- no build output;
- no runtime output;
- no debugger output;
- no compiler output unless later extension model exists.

### 6.3 Future desktop/workstation Output capabilities

Future Output panel may support:

- named output channels;
- channel ownership;
- structured build sessions;
- structured test sessions;
- runtime sessions;
- extension output channels;
- task output channels;
- problem matcher integration;
- correlation with Problems;
- correlation with Logs;
- correlation with Diagnostics;
- timestamped output;
- severity-tagged output lines;
- output folding;
- output filtering;
- output search;
- output pinning;
- output snapshots;
- output export with redaction;
- output retention limits;
- output size limits;
- channel-level permissions;
- output clear policies;
- auto-scroll policies;
- pause/resume streaming;
- slow-output protection;
- unresponsive output producer detection.

### 6.4 Visual Studio-like future direction

On desktop/workstation platforms, Operre may eventually support capabilities similar to Visual Studio's richer diagnostic ecosystem:

- build session overview;
- test session overview;
- error list correlation;
- output channel grouping;
- diagnostic timeline;
- runtime event summaries;
- structured exception summaries;
- build phase grouping;
- test failure grouping;
- task and tool execution history;
- performance summary, local-only;
- extension health report;
- environment summary, redacted;
- reproducibility snapshot;
- local issue bundle creation.

These capabilities must remain optional, local-first, permission-scoped, and redacted by default.

### 6.5 Output privacy rules

Output must not automatically include:

- full file contents;
- secrets;
- tokens;
- passwords;
- private keys;
- environment variables;
- unredacted command lines with secrets;
- protected path content;
- full AI prompts;
- full AI responses;
- huge unbounded output;
- binary blobs;
- crash dump contents.

If output may contain sensitive content, Operre must mark it, redact it where practical, and restrict AI/extension access.

### 6.6 Output channel model

Output channels should include:

- channel ID;
- display name;
- owner;
- permission scope;
- trust requirement;
- retention policy;
- max buffer size;
- redaction policy;
- visibility state;
- last activity time;
- source session ID;
- copy-safe mode.

Output channels must be user-clearable and user-hideable where safe.

## 7. Logs panel

### 7.1 Purpose

Logs panel exposes local application logs safely.

Logs are not diagnostics upload. Logs are not telemetry. Logs are not file content history.

### 7.2 Log categories

Recommended categories:

- app;
- file;
- settings;
- keybindings;
- workspace trust;
- extension;
- security;
- privacy;
- diagnostics;
- search;
- recovery;
- storage;
- AI audit later;
- process execution later;
- runtime later.

### 7.3 Logs safety rules

Logs must be:

- local-only by default;
- rotated;
- retention-limited;
- clearable;
- exportable only by user action;
- redacted for secrets;
- redacted or summarized for protected paths;
- separated by category where useful;
- inaccessible to AI and extensions by default.

Logs must not contain full user file contents by default.

## 8. Diagnostics panel

### 8.1 Purpose

Diagnostics panel helps users understand Operre's health and collect safe troubleshooting information.

Diagnostics must be local-first and user-controlled.

### 8.2 Defaults

Required defaults:

- diagnostics upload OFF;
- crash upload OFF;
- telemetry OFF;
- include file contents OFF;
- include AI prompts OFF;
- include AI responses OFF;
- include secrets OFF;
- include protected paths OFF or redacted;
- preview before export ON;
- local export allowed;
- remote upload requires explicit later feature and explicit consent.

### 8.3 Diagnostics content model

Diagnostics may include safe summaries:

- app version;
- platform;
- OS summary;
- runtime summary;
- active feature flags;
- settings validation counts;
- extension count and safe status;
- workspace trust status;
- recent crash recovery summary;
- log sizes;
- diagnostics collection result;
- redaction summary;
- performance summary, local-only and coarse;
- memory pressure summary;
- large file mode summary;
- panel state summary, coarse;
- safe error counts;
- safe problem counts.

Diagnostics must not include by default:

- file contents;
- unsaved buffers;
- recovery contents;
- secrets;
- full paths without redaction;
- protected path details;
- AI prompts;
- AI responses;
- environment variables;
- shell history;
- raw crash dumps;
- unbounded logs.

### 8.4 Visual Studio-like future diagnostics

On desktop/workstation platforms, Diagnostics may later support richer local analysis:

- diagnostic session creation;
- issue snapshot;
- timeline of safe events;
- component health view;
- extension health view;
- build/test/runtime session summaries;
- correlation between Problems, Output, Logs, and Diagnostics;
- performance counters, local-only;
- slow operation summaries;
- stuck operation detection;
- file watcher health;
- storage/cache health;
- recovery health;
- redaction preview;
- safe support bundle;
- compare diagnostic sessions;
- reproduce issue checklist.

These features must not turn into telemetry. They are local tools first.

### 8.5 Diagnostic bundle workflow

Export workflow must be:

1. collect safe metadata;
2. apply redaction;
3. show preview summary;
4. show included categories;
5. show excluded categories;
6. allow user to remove categories;
7. create local export;
8. require separate action for any upload, if upload ever exists;
9. log the export event without logging sensitive contents.

### 8.6 Redaction summary

Diagnostics must show:

- how many secrets were redacted;
- how many paths were redacted;
- whether file contents were excluded;
- whether AI prompts/responses were excluded;
- whether protected paths were excluded;
- whether environment variables were excluded;
- whether crash dumps were excluded.

The exact redacted values must not be revealed.

## 9. Cross-panel correlation

Desktop/workstation versions may correlate:

- Problem -> Output session;
- Problem -> Log event;
- Problem -> Diagnostic summary;
- Search result -> File Info;
- Output line -> Problem matcher result;
- Extension problem -> Extension details;
- Settings problem -> Settings UI;
- Workspace Trust problem -> Trust UI.

Correlation must use safe IDs and permissions. AI and extensions must not gain cross-panel access by default.

## 10. AI and extension access

Default access:

| Surface | AI default | Extension default |
| --- | --- | --- |
| Problems | denied | denied |
| Search Results | denied | denied |
| Output | denied | denied |
| Logs | denied | denied |
| Diagnostics | denied | denied |
| Safe summaries | scoped permission required | scoped permission required |
| Protected details | denied or redacted | denied or redacted |
| Secrets | denied | denied |

Open UI does not imply data access.

AI may summarize panels only when the user explicitly grants scoped access to that panel, that session, and that content type.

Extensions may contribute diagnostics only through declared contribution points and permission-scoped APIs.

## 11. Device-specific limits

### 11.1 Desktop/workstation

Allowed:

- full Problems panel;
- full Search Results panel;
- Output channels;
- Logs panel;
- Diagnostics panel;
- local diagnostic bundles;
- future build/test/runtime session summaries;
- future Visual Studio-like diagnostic depth.

### 11.2 Tablet

Allowed by default:

- Problems safe list;
- syntax-like checks;
- limited Search Results;
- Diagnostics health summary;
- redaction summary;
- safe local logs summary.

Not allowed by default:

- full build output;
- runtime output;
- debugger output;
- terminal output;
- unbounded logs;
- large diagnostic bundles;
- raw environment details;
- compiler toolchain output unless explicitly designed as a trusted remote or extension workflow later.

### 11.3 Phone

Allowed by default:

- compact Problems cards;
- lightweight syntax or file warnings;
- limited Search Results;
- local app health summary;
- safe diagnostic status.

Not allowed by default:

- full Output panel;
- full Logs panel;
- build/run/debug output;
- terminal output;
- runtime sessions;
- large export bundles;
- multi-column diagnostic tables.

Phone surfaces should prefer full-screen sheets, cards, safe summaries, and command actions.

## 12. Responsive and high-DPI ergonomics

All panels must respect OPR-SPEC-0036 rules:

- no microscopic toolbar icons;
- no unreadable filter text;
- no tiny panel tabs;
- no clipped problem titles;
- no pixel-perfect tapping;
- no inaccessible overflow;
- no hover-only controls on touch;
- panel filter input must remain visible with on-screen keyboard where practical;
- virtualized lists for large data;
- card/list layout on phone;
- drawer or stacked layout on tablet;
- table layout only where enough width exists.

## 13. Command IDs

Required command IDs:

- problems.focus;
- problems.clear;
- problems.copySafeDetails;
- problems.revealSource;
- problems.filterBySeverity;
- problems.showSecurityProblems;
- problems.showPrivacyProblems;

- searchResults.focus;
- searchResults.clear;
- searchResults.rerun;
- searchResults.cancel;
- searchResults.expandAll;
- searchResults.collapseAll;
- searchResults.copySafeSummary;
- searchResults.showRestrictedSummary;

- output.focus;
- output.clear;
- output.selectChannel;
- output.copySafeSelection;
- output.toggleAutoScroll;
- output.pauseStreaming;
- output.resumeStreaming;
- output.exportRedacted;
- output.showChannelPermissions;

- logs.focus;
- logs.openFolder;
- logs.clear;
- logs.exportSafe;
- logs.filter;
- logs.copySafeSelection;
- logs.showRetentionPolicy;
- logs.showRedactionSummary;

- diagnostics.focus;
- diagnostics.collect;
- diagnostics.previewExport;
- diagnostics.exportLocal;
- diagnostics.clearCollected;
- diagnostics.showRedactionSummary;
- diagnostics.showIncludedCategories;
- diagnostics.showExcludedCategories;
- diagnostics.showHealthSummary;
- diagnostics.compareSessionsLater.

All actions must use the central command registry.

## 14. Settings

Recommended settings:

- problems.defaultSeverityFilter;
- problems.showSecurityProblems;
- problems.showPrivacyProblems;
- problems.compactMode;

- searchResults.maxResults;
- searchResults.maxPreviewLength;
- searchResults.virtualizeLargeResults;
- searchResults.showRestrictedSummary;
- searchResults.includeHiddenDefault;

- output.maxBufferSize;
- output.redactSecrets;
- output.autoScroll;
- output.defaultChannel;
- output.enableDesktopAdvancedSessions;
- output.enableTabletLimitedMode;
- output.enablePhoneSummaryMode;

- logs.retentionDays;
- logs.maxSizeMB;
- logs.redactPaths;
- logs.redactSecrets;
- logs.openPanelOnError;

- diagnostics.uploadEnabled;
- diagnostics.crashUploadEnabled;
- diagnostics.includeFileContents;
- diagnostics.includeAIPrompts;
- diagnostics.includeAIResponses;
- diagnostics.includeEnvironmentVariables;
- diagnostics.includeProtectedPaths;
- diagnostics.redactPaths;
- diagnostics.previewBeforeExport;
- diagnostics.localExportOnly;
- diagnostics.enableDesktopAdvancedSessions;
- diagnostics.enableTabletLimitedMode;
- diagnostics.enablePhoneSummaryMode.

Privacy-first defaults are required.

## 15. Acceptance tests

Future implementation must test:

- 10,000 Problems records without UI freeze;
- 100,000 Search Results entries with virtualization;
- very long paths;
- symlink display paths;
- redacted protected paths;
- secret-like strings in logs;
- secret-like strings in output;
- diagnostics export redaction;
- diagnostics preview before export;
- 4K high-DPI panel controls;
- tablet portrait filter input with on-screen keyboard;
- tablet landscape drawer panel;
- phone portrait Problems cards;
- phone compact Diagnostics summary;
- extension denied access to Logs by default;
- AI denied access to Search Results by default;
- Output max buffer enforcement;
- log retention enforcement;
- diagnostic session local export only;
- Workspace Trust restricted state visible.

Failure conditions:

- unredacted secret in export;
- unbounded output memory growth;
- panel UI freeze on large lists;
- phone/tablet showing desktop-only dense tables;
- AI reads panel content without permission;
- extension reads logs without permission;
- Diagnostics upload enabled by default;
- crash upload enabled by default;
- file contents included by default.

## 16. v0.1 scope

Included:

- Problems panel;
- Search Results panel;
- basic Output panel shell;
- basic Logs panel;
- basic Diagnostics panel;
- Settings Problems integration;
- severity filters;
- search grouping;
- search cancel and rerun;
- log clear and open folder;
- diagnostics local export preview;
- redaction baseline;
- protected path redaction baseline;
- responsive panel layout;
- high-DPI panel controls;
- command IDs;
- desktop/workstation full panel readiness;
- tablet limited mode;
- phone summary mode.

Excluded or later:

- compiler diagnostics;
- runtime output;
- build output;
- test output;
- terminal output;
- debug console;
- AI audit panel;
- Visual Studio-like advanced sessions;
- extension marketplace diagnostics;
- cloud diagnostics upload;
- remote support upload;
- phone full Output panel;
- tablet full Output panel.

## 17. Relationship with later topics

Next topic:

NEXT_TOPIC: Extension contribution points and manifest schema

Likely later topics:

- extension permission UI and approval flow;
- Workspace Trust deep behavior;
- safe terminal and process execution model;
- programming language toolchain and live runtime extension model;
- first implementation milestone freeze.

## Workspace Trust relationship

Problems, Search Results, Output, Logs, and Diagnostics must respect Workspace Trust. In untrusted workspaces, safe summaries can remain visible, but unrestricted panel reads, diagnostic bundles, logs access, output access, and AI summarization remain locked unless both trust and scoped permissions allow them.
