# Operre Settings Sync Account and Device Profile Behavior

Status: Accepted specification
Topic ID: OPR-SPEC-0046
Scope: Optional account, optional sync, local-first behavior, safe sync
categories, risky sync categories, never-silent-sync categories, device
profiles, per-device settings, synced settings, Workspace Trust sync
policy, permission grant sync policy, extension sync model, marketplace
account separation, provider-independent sync, encryption-aware sync,
conflict resolution, sync audit, device management later, settings
profiles, safe reset, phone and tablet sync behavior, privacy defaults,
and first implementation direction.

## 1. Purpose

This document defines account, sync, settings profiles, and device
profiles for Operre.

The goal is to make Operre useful across desktop, laptop, tablet, phone,
large monitors, high-DPI monitors, touch devices, and low-power devices
without weakening privacy, security, or local-first use.

Account and sync are optional.

Operre must remain usable without cloud services.

## 2. Core decision

Account is optional for core local use.

Sync is off by default.

Operre remains local-first.

Cloud sync, account login, marketplace login, private registry login,
license login, and AI provider login are separate capabilities and must
not imply workspace access.

Core editing, local projects, local settings, local extensions, local
files, and local dashboards must work without an account.

## 3. Account model

Account may be used later for:

- safe settings sync;
- marketplace account;
- private registry access;
- license state;
- device list;
- account recovery;
- paid features later;
- private server features later.

Account must not be required for:

- opening files;
- editing text;
- opening folders;
- creating managed projects;
- local settings;
- local extension development;
- local packaged extension install;
- local diagnostics;
- local dashboards;
- local export and import.

Account login does not grant AI access.

Account login does not grant extension access.

Account login does not grant workspace data access.

## 4. Sync default

Sync is off by default.

Users may enable sync explicitly.

The first sync UI should explain categories before enabling anything.

A safe sync preset may include:

- theme;
- safe UI settings;
- editor preferences;
- keyboard shortcuts;
- safe snippets;
- safe extension list.

Risky sync categories require stronger review.

Sensitive categories never sync silently.

## 5. Sync categories

Sync categories are divided into:

- safe sync candidates;
- risky sync candidates;
- never-silent-sync categories.

This prevents all-or-nothing sync from becoming a security problem.

## 6. Safe sync candidates

Safe sync candidates include:

- theme;
- accent color;
- editor font settings;
- editor preferences;
- safe UI settings;
- keyboard shortcuts;
- safe snippets;
- language preferences;
- safe project templates;
- safe extension list;
- safe marketplace preferences;
- safe dashboard preferences;
- safe non-path editor behavior;
- safe accessibility preferences.

Safe sync still requires user opt-in.

Safe sync must be explainable.

## 7. Risky sync candidates

Risky sync candidates include:

- workspace list;
- recent files;
- project names;
- layout state;
- task definitions;
- terminal profiles;
- diagnostics summaries;
- logs summaries;
- extension settings;
- AI settings;
- marketplace preferences tied to account state;
- private registry metadata;
- dashboard state;
- device names.

Risky categories require separate toggles and clear warnings.

Risky categories may be disabled on phone or tablet by default.

## 8. Never-silent-sync categories

Never-silent-sync categories include:

- secrets;
- tokens;
- API keys;
- SSH keys;
- database connection strings;
- production target labels;
- raw logs;
- raw outputs;
- AI prompts;
- AI responses;
- diagnostic details;
- Workspace Trust grants;
- permission grants;
- executable approvals;
- toolchain executable paths;
- local file paths;
- protected path access state;
- extension local data;
- extension secrets;
- quarantine overrides;
- developer mode state.

These items must not sync silently.

Most of them should not sync at all in early Operre.

## 9. Device profiles

Device profiles are required.

Device profiles are needed because different devices cannot safely and
ergonomically share the same UI and capability model.

Device profile examples:

- desktop-large;
- desktop-small;
- laptop;
- tablet;
- phone;
- high-DPI-monitor;
- touch-first;
- keyboard-mouse;
- low-power-device;
- remote-view-only.

Device profile affects:

- UI scale;
- layout;
- dashboard density;
- sidebar behavior;
- panel behavior;
- touch mode;
- command availability;
- marketplace capability;
- toolchain capability;
- diagnostics detail level;
- AI context policy;
- safe summary mode;
- warning density;
- menu density;
- toolbar density.

Device profiles should solve real differences between desktop, laptop,
tablet PC, phone, high-DPI, small screen, and touch devices.

## 10. Per-device settings

Per-device settings include:

- UI scale;
- DPI behavior;
- monitor layout;
- window size;
- panel placement;
- touch mode;
- phone layout;
- tablet layout;
- local file paths;
- local executable paths;
- local toolchain approvals;
- local Workspace Trust;
- local extension install path;
- local cache;
- local logs;
- local diagnostics history;
- local output paths;
- local developer mode state;
- local resource limits;
- local terminal profile paths.

Per-device settings are not synced by default.

## 11. Synced settings

Synced settings may include:

- theme choice;
- safe editor preferences;
- editor tab behavior;
- keybindings;
- safe snippets;
- safe extension preference;
- marketplace preference;
- selected safe profile templates;
- safe dashboard preferences;
- safe accessibility preferences.

Synced settings may still have local overrides.

Local overrides must be visible.

## 12. Workspace Trust sync policy

Workspace Trust must not sync by default.

Workspace Trust is:

- device-local;
- path-local;
- workspace-local;
- revocable;
- explainable;
- tied to local identity.

The same project name or folder name can have different risk on another
device.

Syncing Workspace Trust silently is unsafe.

## 13. Permission grant sync policy

Permission grants must not sync by default.

This includes:

- extension permission grants;
- AI permission grants;
- toolchain permission grants;
- diagnostics access grants;
- raw log access grants;
- raw output access grants;
- production action grants;
- remote target grants;
- package manager grants;
- executable approval grants.

Permission grants depend on device, workspace, extension version,
package source, publisher state, trust state, path, and local risk.

## 14. Extension sync model

Extension sync is preference-oriented, not binary sync.

Sync may include:

- extension ID;
- desired version;
- desired channel;
- enabled or disabled preference for low-risk extensions;
- marketplace source preference;
- safe extension settings.

Sync must not include:

- extension binary;
- package file;
- local unpacked path;
- developer mode state;
- permission grants;
- trust grants;
- executable approvals;
- extension secrets;
- extension local data;
- quarantine override;
- local toolchain bindings.

On a new device, synced extension list is an installation suggestion.

It is not automatic trust.

It is not automatic installation.

## 15. Marketplace and account separation

Marketplace account may use the general account system later.

Local Operre use does not require marketplace login.

Private registry may use separate credentials.

Marketplace login does not grant workspace data access.

Marketplace login does not grant AI provider access.

Marketplace login does not grant extension permissions.

Marketplace login does not grant toolchain permissions.

## 16. Sync provider model

Sync provider model should be provider-independent.

Possible providers:

- no sync;
- local export and import;
- file-based profile backup;
- self-hosted sync later;
- private server later;
- Operre cloud later.

First implementation should provide local export and import skeletons.

Cloud sync is later.

Account is later.

Self-hosted sync is later.

## 17. Encryption-aware sync

Sync design must be encryption-aware from the beginning.

Rules:

- transport encryption is required for network sync;
- sensitive sync categories require stronger protection;
- secrets sync is disabled by default;
- secret sync, if ever added, requires end-to-end encryption;
- local export bundle encryption may be added later;
- recovery key may be added later;
- no silent upload of sensitive state;
- no silent downgrade of encrypted sync;
- clear warnings for unencrypted export.

Security must be strict.

## 18. Conflict resolution

Conflict UI is required.

Conflict options include:

- keep local;
- use remote;
- merge if safe;
- compare diff;
- reset to recommended;
- duplicate profile;
- device-specific override.

High-risk settings must not auto-merge.

DPI, screen size, monitor layout, window layout, toolbar density, panel
placement, touch mode, and phone or tablet layout conflicts need special
care.

UI conflicts should be ergonomic and understandable.

## 19. Sync audit

Sync audit is required.

Audit events include:

- sync enabled;
- sync disabled;
- category enabled;
- category disabled;
- item uploaded;
- item downloaded;
- conflict occurred;
- conflict resolved;
- device linked;
- device unlinked;
- account signed in;
- account signed out;
- provider changed;
- sync reset;
- remote wipe requested later;
- export bundle created;
- import bundle applied;
- risky category blocked;
- sensitive category rejected.

Audit logs must not contain raw secrets.

Audit logs must not expose protected path data by default.

## 20. Device management later

Device management is planned later.

Device management may include:

- device list;
- device name;
- device type;
- last sync;
- sync categories;
- device profile;
- trust state;
- revoke device;
- unlink device;
- remote wipe later;
- lost device mode later;
- device capability summary;
- phone and tablet restriction state.

Device management is not required for v0.1.

It must be planned so account and sync do not become unsafe later.

## 21. Settings profiles

Settings profiles are required.

Profile examples:

- Default;
- Safe Mode;
- Work;
- Mobile;
- Tablet;
- Minimal;
- Expert;
- Presentation;
- High-DPI;
- Low-power;
- Development;
- AI-disabled;
- Extension-dev;
- Remote-view-only.

Settings profiles may sync if safe.

Local overrides remain local.

Risky profile settings require warnings.

Profile switching must not silently grant permissions.

## 22. Safe reset and recommended defaults

Safe reset is required.

Reset levels include:

- reset one setting;
- reset category;
- reset profile;
- reset sync settings;
- reset device profile;
- reset account state;
- disable sync;
- disable all risky sync;
- restore recommended defaults.

Risky settings should show:

- current value;
- recommended value;
- risk label;
- reset action;
- scope;
- device override state.

Safe reset must not delete user data silently.

Safe reset must not remove secrets silently.

## 23. Phone and tablet sync behavior

Phone and tablet sync should be useful but safe.

Allowed by default:

- view sync status;
- safe settings sync;
- theme sync;
- keybindings view;
- extension list view;
- marketplace safe summary;
- dashboard safe preferences;
- disable sync;
- revoke this device;
- export safe profile later.

Not allowed by default:

- approve Workspace Trust sync;
- approve permission grants;
- approve executable sync;
- approve toolchain sync;
- reveal secrets;
- sync raw logs;
- sync raw diagnostics;
- approve production targets;
- approve remote targets;
- enable developer mode sync.

Phone and tablet must not be useless.

Phone and tablet should expose safe actions and clearly disabled risky
actions.

## 24. Privacy defaults

No private user data uploads by default.

Default off:

- telemetry;
- crash upload;
- diagnostics upload;
- AI prompt upload;
- AI response upload;
- usage analytics;
- workspace names upload;
- file paths upload;
- extension install list upload;
- recent files upload;
- project names upload;
- raw log upload;
- raw output upload;
- production target upload;
- remote target upload.

User must explicitly opt in to safe categories.

Privacy defaults must be visible.

## 25. First implementation direction

First implementation starts with local settings and profiles.

Included in v0.1 planning:

- settings schema skeleton;
- settings profile skeleton;
- device profile skeleton;
- local export skeleton;
- local import skeleton;
- sync categories model;
- safe/risky/never-silent categories;
- no cloud sync yet;
- no account required;
- no secret sync;
- no Workspace Trust sync;
- no permission grant sync;
- UI placeholders;
- safe reset skeleton;
- privacy defaults.

First implementation must not depend on cloud sync.

First implementation must not depend on marketplace account.

First implementation must not depend on AI account.

Local export and import are enough for v0.1.

Device profile and settings profile skeletons are more important than
full cloud sync.

Operre must remain buildable by a small team.

## 26. Acceptance tests

Future implementation must test:

- Operre opens without account;
- core editing works without account;
- sync is off by default;
- safe sync categories are visible;
- risky sync categories are separate;
- never-silent categories cannot sync silently;
- Workspace Trust does not sync;
- permission grants do not sync;
- extension list sync is suggestion-only;
- extension binary does not sync;
- device profile exists;
- UI scale can be per-device;
- phone uses phone profile;
- tablet uses tablet profile;
- high-DPI monitor uses appropriate profile;
- conflict UI appears for unsafe merge;
- high-risk settings do not auto-merge;
- sync audit does not expose secrets;
- local export works;
- local import works;
- cloud sync is not required;
- account is not required;
- safe reset can disable sync;
- safe reset can restore recommended defaults;
- telemetry upload is off by default;
- crash upload is off by default;
- diagnostics upload is off by default;
- AI prompt upload is off by default;
- AI response upload is off by default.

Failure conditions:

- account is required for local editing;
- sync enables silently;
- Workspace Trust syncs silently;
- permission grant syncs silently;
- local executable path syncs silently;
- toolchain approval syncs silently;
- secret appears in export;
- raw logs sync silently;
- AI prompts sync silently;
- phone approves risky sync by default;
- tablet approves production target sync by default;
- device profile conflicts auto-merge unsafely;
- telemetry enables silently.

## 27. v0.1 scope

Included in planning:

- optional account model;
- sync off default;
- local-first model;
- safe sync categories;
- risky sync categories;
- never-silent-sync categories;
- device profiles;
- per-device settings;
- synced settings;
- Workspace Trust no-sync policy;
- permission grants no-sync policy;
- extension preference sync model;
- marketplace and account separation;
- provider-independent sync plan;
- encryption-aware sync plan;
- conflict UI;
- sync audit;
- device management later;
- settings profiles;
- safe reset;
- phone and tablet safe sync;
- privacy defaults;
- first implementation buildability limit.

## 28. Relationship with later topics

Next topic:

NEXT_TOPIC: First implementation milestone freeze and v0.1 scope

Likely later topics:

- first implementation code skeleton;
- project setup in `/home/mak/dev`.
