# Operre Extension Marketplace Package Signing and Update Distribution

Status: Accepted specification
Topic ID: OPR-SPEC-0045
Scope: Extension marketplace planning, local extension installation,
packaged extension installation, private registry, public marketplace
later, package format, package hashes, manifest hashes, signing,
publisher identity, extension identity, version channels, update
permission diff, manual update policy, rollback, quarantine, marketplace
UI, offline install, phone and tablet behavior, developer mode, review
and moderation later, extension data privacy, and first implementation
direction.

## 1. Purpose

This document defines how Operre distributes, installs, verifies, updates,
rolls back, quarantines, and presents extensions.

The goal is a powerful extension ecosystem that remains realistic to
build, secure by default, private by default, and ergonomic for users.

Public marketplace is planned later.

The first practical model is local, packaged, first-party, and private
registry friendly.

## 2. Core decision

Operre supports multiple extension sources:

- built-in first-party extensions;
- local unpacked extensions;
- local packaged extensions;
- private registry;
- direct package file import;
- GitHub release or URL import later with strong warnings;
- public marketplace later.

Public marketplace is required eventually, but it is not the first
implementation target.

The first implementation should focus on local packaged install,
developer mode, metadata validation, package hash, private registry
metadata skeleton, update diff model, rollback state, and quarantine
state.

## 3. Trust order

Recommended trust order:

- built-in first-party extension;
- local user-approved package;
- private trusted registry;
- signed public marketplace package later;
- unverified local unpacked developer extension;
- unknown URL import.

Unknown URL import is disabled by default.

Unverified sources are allowed only with clear warnings, visible source,
limited permissions, and user approval.

## 4. Package format

The canonical Operre extension package extension is `.oprx`.

The `.oprx` extension is short, recognizable, Operre-specific, and not
limited by old three-letter extension habits.

An `.oprx` package is a verifiable extension archive.

Package content may include:

- manifest.json;
- extension files;
- permission manifest;
- contribution manifest;
- package metadata;
- content hash list;
- signature file later;
- README;
- changelog;
- license;
- icon;
- screenshots later.

Package contents must be inspectable before installation.

Package preview is required before installation.

## 5. Package metadata and hashes

Packages should carry:

- package ID;
- publisher ID;
- extension ID;
- version;
- manifest hash;
- content hash list;
- package hash;
- signing key ID later;
- signature state;
- build timestamp;
- source registry;
- download URL, if any;
- previous version relation;
- update channel;
- package format version;
- minimum Operre version;
- target platform support;
- device support;
- permission summary;
- contribution summary.

Manifest hash and content hash checks are required planning concepts.

Operre should provide UI and internal validation for checking hashes.

Users should be able to inspect what changed before update.

## 6. Package signing

Package signing is planned from the beginning.

Initial implementation includes:

- signature fields reserved;
- package hash skeleton;
- manifest hash skeleton;
- trusted publisher concept;
- unverified package warning.

Later implementation may include:

- publisher key;
- package signature;
- registry signature;
- timestamping;
- revocation list;
- compromised key handling;
- signature chain;
- offline verification;
- key rotation.

Unsigned packages may be installed only as unverified packages.

Unverified packages require stronger warnings.

High-risk permissions from unverified packages require stronger approval.

Security must be strict around signing.

## 7. Publisher identity

Publisher identity fields include:

- publisher ID;
- display name;
- verified state;
- signing key IDs;
- registry source;
- website;
- support URL;
- privacy policy URL;
- trust state;
- blocked state;
- known compromise state;
- first seen time;
- last updated time.

Users may trust or block publishers.

Users may prefer first-party publishers or publishers they trust.

Blocked publishers cannot install or update extensions without explicit
review and unblock.

Known compromised publishers trigger quarantine behavior.

## 8. Extension identity

Extension ID is immutable.

Recommended ID form:

- publisher.extensionName.

Rules:

- extension ID does not change after publication;
- the same extension ID cannot come from a different publisher;
- display name may change;
- extension ID remains stable;
- name similarity warnings are required later;
- local extension ID conflict opens a conflict UI;
- version, install time, and last update time are visible.

Name collision and name imitation are known marketplace risks.

Operre must make identity clearer than display name alone.

## 9. Version and update channels

Versioning uses semantic versioning where possible.

Pre-release and build metadata are allowed.

Update channels include:

- stable;
- beta;
- dev;
- pinned;
- manual only.

The recommended default is manual updates only.

Auto-check may be allowed.

Auto-install is off by default.

High-risk extensions use manual approval.

Users can pin an extension.

Users can freeze all extension updates.

Yellow-bar update notices should explain available updates clearly.

## 10. Update permission diff

Update permission diff is mandatory.

Update UI must show:

- new permissions;
- removed permissions;
- changed permissions;
- new contribution points;
- new commands;
- new toolchain templates;
- new network or domain requests;
- new file access requests;
- new AI access requests;
- new diagnostics access requests;
- new package manager risks;
- new toolchain risks;
- changed device support;
- changed marketplace source;
- changed publisher state;
- changed signature state.

If an update requests new permissions, old grants do not silently cover
the new scope.

The default behavior from extension permission policy is preserved:
updates with new permissions become pending or disabled until approved.

## 11. Update security policy

Update policy options include:

- A: auto-update safe patch only with no new permission;
- B: notify and require approval for permission changes;
- C: manual updates only;
- D: freeze or pin extension.

The recommended default is C.

Manual updates only is safest and realistic for early Operre.

Yellow-bar update information should be clear, helpful, and not noisy.

Future virtual or sandboxed update inspection should be planned.

High-risk extensions require manual approval.

Production, remote, AI, diagnostics, package manager, and toolchain
related extensions require stronger update review.

## 12. Rollback

Rollback is required.

Rollback planning includes:

- previous version cache;
- rollback action;
- disable extension;
- Safe Mode launch;
- extension quarantine;
- rollback audit log;
- rollback reason;
- update failure diagnostics;
- broken update detection;
- user-visible rollback summary.

Rollback must not delete user data or secrets.

Rollback must not silently restore unsafe permissions.

Rollback should preserve enough state for diagnostics.

## 13. Quarantine

Extension quarantine is required.

Quarantine triggers may include:

- invalid signature;
- package tampering;
- publisher blocked;
- publisher compromise;
- marketplace revocation;
- permission abuse;
- crash loop;
- resource abuse;
- malicious behavior detected later;
- package hash mismatch;
- manifest hash mismatch;
- extension host safety violation.

In quarantine:

- extension does not run;
- contribution points are disabled;
- commands are disabled;
- toolchain templates are disabled;
- diagnostics providers are disabled;
- user sees the reason;
- rollback may be offered;
- remove may be offered;
- audit log is written.

Quarantine is a safety state, not only an uninstall suggestion.

## 14. Marketplace UI

Marketplace UI must be ergonomic and security-focused.

It should show:

- extension name;
- extension ID;
- publisher;
- verified or unverified state;
- version;
- install time, if installed;
- last updated time;
- rating later;
- installs later;
- permission summary;
- risk summary;
- device support;
- desktop support;
- phone support;
- tablet support;
- screenshots later;
- changelog;
- license;
- privacy notes;
- package signature state;
- source registry;
- install button;
- update button;
- remove button;
- rollback button where available;
- quarantine state where applicable.

Risky permissions use clear warning bars.

Critical risks use stronger visual treatment.

The UI should remain simple enough for normal users.

## 15. Private registry

Private registry is the first realistic network distribution model.

Private registry may provide:

- metadata API;
- package download;
- version manifest;
- publisher metadata;
- signature metadata later;
- update channel;
- admin upload;
- disabled package list;
- revoked package list;
- simple authentication later;
- audit events later.

A single VPS can be enough for early private registry.

The model must be secure enough to evolve into a professional registry.

Private registry does not remove package verification requirements.

## 16. Offline and air-gapped install

Offline package install is supported.

Rules:

- package hash is shown;
- manifest is shown;
- permissions are shown;
- signature is verified when available;
- unsigned package shows unverified warning;
- source is recorded as local package;
- update auto-check is disabled or unavailable;
- permission preview is required;
- install audit log is written.

Offline install must not bypass permissions.

## 17. Phone and tablet marketplace behavior

Phone and tablet marketplace support should be useful but safe.

Allowed by default:

- browse marketplace;
- view extension details;
- view permission summary;
- view update status;
- view safe summary;
- request safe install later;
- disable extension;
- read changelog;
- read license;
- read privacy notes.

Not allowed by default:

- approve high-risk permission;
- install desktop-only toolchain extension;
- approve local executable or toolchain;
- approve production extension;
- sideload unverified package;
- run extension developer mode;
- approve remote execution extension.

Mobile should not become useless.

Mobile should expose safe can-do actions and clearly disabled risky
actions.

## 18. Developer Mode

Local unpacked extension requires Developer Mode.

Developer Mode includes:

- separate setting;
- clear warning;
- status bar indicator;
- machine-level or session-level control;
- extension path visible;
- no marketplace trust;
- no signature;
- limited permissions by default;
- disable all developer extensions action;
- Safe Mode disables developer extensions;
- audit logging;
- obvious UI state.

Developer Mode must balance power, security, and ergonomics.

## 19. Review and moderation later

Public marketplace review is later.

Planned review capabilities include:

- automated checks;
- manifest validation;
- malware scan later;
- permission review;
- signature check;
- publisher verification;
- policy violation detection;
- takedown;
- revocation;
- user report;
- admin review;
- name imitation review;
- suspicious update review.

This must be planned but not allowed to block early implementation.

Operre must stay realistic to build.

## 20. Extension data privacy

Marketplace and extension systems must not mix with private user data by
default.

Data that must not upload by default:

- extension install list;
- usage telemetry;
- crash reports;
- diagnostics;
- AI prompts;
- AI responses;
- workspace names;
- file paths;
- toolchain profiles;
- project names;
- production target labels.

Recommended defaults:

- telemetry off;
- usage upload off;
- crash upload off;
- diagnostics upload off;
- prompt and response upload off;
- marketplace search and download use minimum metadata;
- privacy note visible.

Privacy must remain a product principle.

## 21. Settings

Recommended settings include:

- extensions.marketplace.enabled;
- extensions.marketplace.publicEnabled;
- extensions.marketplace.privateRegistryEnabled;
- extensions.marketplace.unknownUrlImportEnabled;
- extensions.package.format;
- extensions.package.requirePreview;
- extensions.package.verifyHashes;
- extensions.package.requireSignatureForHighRisk;
- extensions.signing.enabledLater;
- extensions.publisher.trustEnabled;
- extensions.publisher.blockEnabled;
- extensions.update.policy;
- extensions.update.autoCheck;
- extensions.update.autoInstall;
- extensions.update.requirePermissionDiff;
- extensions.update.showYellowBar;
- extensions.rollback.enabled;
- extensions.quarantine.enabled;
- extensions.developerMode.enabled;
- extensions.developerMode.sessionOnly;
- extensions.offlineInstall.enabled;
- extensions.phone.safeMarketplaceMode;
- extensions.tablet.safeMarketplaceMode;
- extensions.privacy.telemetryUpload;
- extensions.privacy.crashUpload;
- extensions.privacy.usageUpload;
- extensions.review.enabledLater.

Recommended defaults:

- public marketplace disabled until ready;
- private registry skeleton allowed later;
- unknown URL import disabled;
- package format is `.oprx`;
- package preview required;
- hash verification enabled where available;
- signature fields reserved;
- high-risk unsigned packages require stronger warning;
- update policy is manual only;
- auto-install disabled;
- permission diff required;
- rollback enabled;
- quarantine enabled;
- Developer Mode disabled by default;
- telemetry, usage upload, crash upload, and diagnostics upload off.

## 22. Acceptance tests

Future implementation must test:

- `.oprx` package can be previewed before install;
- package hash is visible;
- manifest hash is visible;
- content hash list is visible where available;
- unsigned package shows unverified warning;
- publisher identity is visible;
- publisher can be blocked;
- extension ID conflict shows conflict UI;
- version is visible;
- install time is visible;
- last updated time is visible;
- update channel is visible;
- update permission diff is visible;
- update with new permission becomes pending or disabled;
- manual update policy is default;
- auto-install is off by default;
- rollback state exists;
- quarantine state exists;
- invalid signature triggers quarantine later;
- hash mismatch blocks or quarantines package;
- Developer Mode is required for local unpacked extension;
- Safe Mode disables developer extensions;
- phone shows safe marketplace summary;
- tablet shows safe marketplace summary;
- unverified sideload is blocked on phone by default;
- telemetry upload is off by default;
- crash upload is off by default;
- diagnostics upload is off by default.

Failure conditions:

- extension installs without preview;
- update grants new permissions silently;
- unknown URL import is enabled silently;
- unsigned high-risk package installs without strong warning;
- extension identity is based only on display name;
- publisher block is ignored;
- quarantined extension runs;
- rollback deletes user data;
- developer extension runs without Developer Mode;
- mobile approves high-risk permission by default;
- marketplace uploads workspace paths by default;
- telemetry turns on silently.

## 23. v0.1 scope

Included in planning:

- extension package metadata schema skeleton;
- `.oprx` package format plan;
- package hash skeleton;
- manifest hash skeleton;
- content hash list skeleton;
- manifest validation skeleton;
- local packaged install flow skeleton;
- local unpacked Developer Mode skeleton;
- private registry metadata skeleton;
- marketplace UI placeholder;
- update permission diff model;
- manual update policy default;
- quarantine state skeleton;
- rollback state skeleton;
- publisher identity model;
- extension immutable ID model;
- offline install planning;
- phone and tablet safe marketplace behavior;
- privacy defaults;
- no public marketplace yet;
- no auto-install;
- no auto-update;
- no signature enforcement yet;
- signature fields reserved.

First implementation should be realistic and buildable.

The system should become stronger while users actually use it.

## 24. Relationship with later topics

Next topic:

NEXT_TOPIC: Settings sync account and device profile behavior

Likely later topics:

- first implementation milestone freeze.

Telemetry, usage upload, crash upload, and diagnostics upload are off by default.

## Account and sync relationship

Marketplace login does not grant workspace data access, AI access,
extension permissions, toolchain permissions, or sync permissions.
Extension sync is suggestion-oriented. Extension binaries, local unpacked
paths, Developer Mode state, permission grants, trust grants, executable
approvals, secrets, local data, and quarantine overrides must not sync
silently.
