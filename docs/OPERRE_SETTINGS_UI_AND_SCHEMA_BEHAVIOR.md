# Operre Settings UI and Settings Schema Behavior

## Purpose

This document defines Operre's Settings UI, `settings.json` / JSONC behavior, settings schema, validation, storage levels, privacy rules, secret handling, import/export, migration, and security interaction.

This decision follows the Recent Files and Projects behavior decision.

## Core principle

Operre settings must be powerful for advanced users, simple for normal users, safe by default, local-first, privacy-first, and resilient against invalid configuration.

Operre must provide both:

- a user-friendly Settings UI;
- an advanced editable settings file.

## Settings access modes

Operre must support two settings access modes.

### Settings UI

For normal users.

Required behavior:

- searchable settings screen;
- category-based navigation;
- visible modified indicators;
- Reset to Default action;
- clear labels and descriptions;
- warnings for risky settings;
- restart-required indicators;
- validation feedback;
- safe defaults.

### settings.json / JSONC

For advanced users.

Required behavior:

- user can directly edit settings;
- JSON schema validation is required;
- invalid JSON must not crash Operre;
- invalid values fall back to safe defaults;
- user sees a clear warning;
- Settings Problems panel may show issues;
- JSONC is accepted so comments are allowed.

Accepted decision:

- Operre should support JSONC for user-editable settings files.

## Settings file format

Primary format:

- JSONC.

Reason:

- readable;
- familiar to developer users;
- supports comments;
- works well with schema validation;
- can be edited in Operre itself.

Rules:

- comments are allowed in user-editable settings files;
- persisted machine-generated settings may use plain JSON internally if needed;
- exported settings may use JSONC or JSON depending on export mode;
- schema version must be stored or inferable.

## Settings levels

Operre should support layered settings.

Levels:

- Default settings;
- User settings;
- Workspace/project settings;
- Folder settings later;
- Language-specific settings;
- Extension settings;
- Machine-local settings;
- Temporary/session override.

Baseline priority order:

- Default;
- User;
- Workspace/Project;
- Folder;
- Language-specific;
- Temporary/session override.

Extension settings should be namespaced and merged according to permission/trust rules.

Machine-local settings should not be synced by default and may override syncable user settings where necessary.

## Default settings

Default settings are built into Operre.

Rules:

- read-only;
- documented;
- visible through UI where useful;
- used when user setting is missing or invalid;
- must be safe and privacy-first.

## User settings

User settings apply globally to the current user.

Suggested Linux path:

- `~/.config/operre/settings.jsonc`

Suggested Windows path:

- `%APPDATA%\Operre\config\settings.jsonc`

Suggested macOS path:

- `~/Library/Application Support/Operre/config/settings.jsonc`

Rules:

- user-owned;
- local by default;
- may be exportable;
- may be syncable later only with explicit consent;
- must not contain secrets.

## Workspace/project settings

Workspace/project settings apply to an opened workspace/project.

Possible path:

- `.operre/shared/settings.jsonc`

Reason:

- `.operre/shared/` is the accepted optional shared/tracked `.operre` subtree.

Rules:

- workspace settings must not silently enable dangerous features;
- workspace settings must obey Workspace Trust;
- workspace settings must not contain secrets;
- workspace settings must not silently grant extension, AI, terminal, network, Git, or credential permissions;
- security-impacting workspace settings require explicit user consent.

## Folder settings

Folder settings may come later.

Purpose:

- override settings for a folder inside a large workspace.

First version may defer folder settings, but architecture should not block them.

## Language-specific settings

Language-specific settings are required by design.

Examples:

- Markdown settings;
- TypeScript settings later;
- JSON settings;
- plain text settings;
- CAD/text formats later.

Use cases:

- indentation;
- word wrap;
- formatting rules;
- editor features;
- syntax behavior.

## Extension settings

Each extension must have its own settings namespace.

Examples:

- `extensions.github.enabled`;
- `extensions.ideboard.enabled`;
- `extensions.example.someSetting`.

Rules:

- extension settings cannot bypass permissions;
- extension settings cannot grant secret/network/workspace access by themselves;
- extension settings are subject to Workspace Trust;
- extension uninstall may ask whether to remove extension settings;
- extension settings must be validated against extension-provided schema where possible.

## AI settings

AI settings must be explicit and safe by default.

Accepted baseline:

- AI agents default OFF;
- provider selection later;
- model/provider credentials are not stored as plaintext settings;
- real secrets live in Secret Vault / OS keyring;
- AI workspace access default OFF;
- AI logs settings are separate;
- prompt/response logging default OFF;
- per-project/per-agent override may be supported;
- Workspace Trust can restrict AI settings;
- AI settings cannot silently grant workspace access.

## Machine-local settings

Machine-local settings are local state and should not sync by default.

Examples:

- window position;
- window size;
- monitor placement;
- local path history;
- recent history;
- cache limits;
- device performance profile;
- private mode state;
- local-only extension state;
- local file picker history;
- local session restore state where needed.

Suggested Linux area:

- `~/.local/state/operre/`

Machine-local settings must be separate from syncable user settings.

## Secret handling

Secrets must not be stored in `settings.jsonc`.

Secrets include:

- passwords;
- tokens;
- API keys;
- OAuth refresh tokens;
- SSH private keys;
- cloud credentials;
- AI provider keys;
- GitHub tokens;
- Ideboard tokens;
- extension credentials.

Accepted model:

- settings may store a reference to a secret;
- real secret value lives in Secret Vault / OS keyring;
- exporting settings must not export secret values;
- diagnostics must not include secret values;
- UI must warn if a user appears to paste a secret into settings.

## Secret Vault relationship

Secret Vault is separate from settings.

Settings may reference:

- secret ID;
- provider name;
- credential label;
- account alias.

Settings must not store:

- raw token;
- raw password;
- raw private key;
- raw credential JSON;
- raw refresh token.

## Privacy-first defaults

Default privacy/security settings:

- telemetry OFF;
- crash upload OFF;
- diagnostics upload OFF;
- recent sync OFF;
- settings sync OFF;
- AI access OFF;
- extension permissions deny by default;
- search history local-only;
- recent history local-only;
- prompt/response logging OFF;
- extension telemetry denied by default.

## Settings categories

Settings UI categories should include:

- General;
- Appearance;
- Editor;
- Files;
- Explorer;
- Search;
- Replace;
- File Compare;
- Large Files;
- Markdown;
- Recent Files / Projects;
- Session Restore;
- Keyboard Shortcuts;
- Extensions;
- AI Agents;
- Privacy & Security;
- Storage & Cache;
- Sync;
- Diagnostics;
- Updates;
- Developer / Advanced.

The exact UI order can be refined later.

## General settings

Possible General settings:

- startup behavior;
- default new file type;
- default workspace path;
- language/locale later;
- update behavior;
- confirm before close;
- restore previous session;
- private mode.

## Appearance settings

Appearance settings should include:

- theme;
- system theme;
- light theme;
- dark theme;
- gray theme;
- high contrast theme;
- accent color later;
- icon size;
- UI scale;
- status bar visibility;
- activity bar visibility;
- sidebar visibility;
- sidebar position later;
- minimap visibility where editor-specific.

Important rule:

- dark mode must not be assumed as default.

## Editor settings

Editor settings should include:

- font family;
- font size;
- line height;
- tab size;
- spaces/tabs;
- word wrap;
- minimap;
- render whitespace;
- line numbers;
- auto save;
- format on save later;
- default encoding;
- default line ending;
- preserve existing BOM;
- trim trailing whitespace later;
- insert final newline later.

## Files settings

Files settings should include:

- default encoding;
- line ending behavior;
- BOM handling;
- autosave behavior;
- save confirmation;
- delete confirmation;
- permanent delete confirmation;
- hidden files visibility;
- protected path warnings;
- large file thresholds.

## Explorer settings

Explorer settings should include:

- Show Hidden Files;
- show protected metadata markers;
- confirm delete;
- confirm permanent delete;
- reveal behavior;
- file nesting later;
- sort order;
- folders first;
- compact folders later.

## Search settings

Search settings should include:

- case sensitive default;
- whole word default;
- regex default;
- include hidden files default OFF;
- include protected paths default OFF or advanced only;
- max search results;
- search history on/off;
- search history retention;
- large file search result limit.

## Replace settings

Replace settings should include:

- confirm replace all;
- confirm replace in files;
- preview before replace in files;
- backup/snapshot before risky replace later;
- exclude hidden/protected paths by default.

## File Compare settings

File Compare settings should include:

- default layout: side-by-side or stacked;
- synchronized scrolling;
- highlight differences;
- highlight same/identical regions;
- red/difference highlight intensity;
- optional green/same highlight;
- ignore whitespace;
- ignore leading/trailing whitespace;
- ignore line endings;
- ignore case;
- ignore blank lines;
- collapse unchanged sections later;
- diff granularity: line / word / character;
- large file compare mode.

## Large Files settings

Large Files settings should include:

- warning threshold;
- Large File Mode threshold;
- Very Large File Mode threshold;
- memory budget;
- cache size;
- minimap disable threshold;
- lazy syntax highlighting;
- read-only fallback;
- large file search result limit;
- large file compare mode;
- cache cleanup policy.

## Markdown settings

Markdown settings should include:

- default open mode: edit;
- preview mode;
- side-by-side preview;
- live preview;
- sanitization behavior;
- local image loading policy;
- remote resource blocking;
- warning bar visibility.

Raw HTML/script security remains controlled by security policy and should not be silently weakened.

## Recent Files / Projects settings

Recent settings should include:

- max recent files;
- max recent projects;
- max recent comparisons later;
- pinned items enabled;
- clear on exit;
- private mode;
- retention duration;
- clear missing entries;
- sensitive/protected exclusion behavior.

## Session Restore settings

Session Restore settings are separate from Recent history.

Settings should include:

- restore previous session;
- restore tabs;
- restore active tab;
- restore split layout;
- restore cursor position;
- restore scroll position;
- session restore on crash;
- crash recovery retention.

## Keyboard Shortcuts settings

Keyboard shortcut settings should include:

- editable keybindings;
- `keybindings.jsonc`;
- Settings UI editing;
- conflict detection;
- reset shortcut;
- reset all;
- export/import shortcuts later.

Detailed keybinding behavior should be defined in a dedicated follow-up decision.

## Extension settings category

Extension settings should include:

- installed extensions;
- enabled/disabled state;
- per-extension settings;
- extension permissions;
- extension trust;
- extension telemetry setting;
- uninstall cleanup behavior.

## AI Agents settings category

AI settings should include:

- AI enabled/disabled;
- agent list later;
- provider selection later;
- credential reference;
- workspace access permissions;
- prompt/response logging;
- AI audit log settings;
- per-project/per-agent overrides;
- model behavior settings later.

## Privacy & Security settings

Privacy & Security settings should include:

- telemetry;
- crash upload;
- diagnostics upload;
- strict privacy mode;
- extension telemetry;
- AI access;
- prompt/response logging;
- secret vault access;
- recent history behavior;
- search history behavior;
- protected path handling.

## Storage & Cache settings

Storage & Cache settings should include:

- cache location display;
- cache size limit;
- clear cache;
- large file cache;
- compare cache;
- search index cache later;
- local state location display;
- storage cleanup tools.

## Sync settings

Sync is OFF by default.

Future sync settings may include:

- settings sync;
- keyboard shortcuts sync;
- theme sync;
- extension list sync;
- extension settings sync;
- recent history sync;
- exclude secrets;
- exclude local paths;
- exclude machine-local settings;
- user-owned sync preference.

Sync requires explicit user consent.

## Diagnostics settings

Diagnostics settings should include:

- local logs;
- diagnostics export;
- redaction;
- include system info;
- include app settings;
- exclude secrets;
- exclude recent history by default;
- exclude file contents by default.

## Updates settings

Updates settings may include:

- update checks;
- auto-update later;
- update channel later;
- release notes;
- restart required notice.

First implementation can defer complex updater behavior.

## Developer / Advanced settings

Developer/Advanced settings may include:

- open settings JSONC;
- open keybindings JSONC;
- open logs folder;
- open cache folder;
- reset user settings;
- reset workspace settings;
- show internal diagnostics;
- enable experimental features;
- advanced hidden/protected path settings.

Dangerous advanced settings must show warnings.

## Settings sync

Settings sync is OFF by default.

If added later:

- explicit user consent required;
- secret values excluded;
- recent history excluded by default;
- local paths excluded by default;
- cache settings excluded where machine-specific;
- machine-local settings excluded;
- extension credentials excluded;
- AI credentials excluded;
- user-owned sync is preferred.

## Import/export

Settings import/export may be supported.

Export rules:

- explicit user action;
- no secrets;
- no raw credentials;
- no recent history by default;
- no local path history by default;
- include schema version;
- allow redacted export.

Import rules:

- preview before import;
- validate before applying;
- show changed settings;
- show invalid settings;
- do not silently enable risky settings;
- respect Workspace Trust;
- allow cancel.

## Validation

Settings validation is required.

Validation should catch:

- invalid JSON/JSONC;
- unknown setting;
- wrong type;
- invalid enum value;
- invalid numeric range;
- invalid path;
- unsafe setting blocked by Workspace Trust;
- extension setting schema error;
- secret-like value in plaintext setting.

Invalid settings must not crash Operre.

## Schema version

Settings schema version is required.

Purpose:

- migration;
- compatibility;
- warnings;
- extension schema coordination;
- export/import validation.

## Migration

Settings migration is required by design.

Behavior:

- migrate old settings when safe;
- preserve unknown settings where practical;
- warn about deprecated settings;
- do not delete user settings silently;
- backup before destructive migration where practical.

## Deprecated and unknown settings

Unknown settings:

- should not crash Operre;
- may be shown in Settings Problems;
- may be preserved in file.

Deprecated settings:

- should show warning;
- may suggest replacement;
- may be migrated automatically if safe.

## Settings Problems panel

Settings Problems panel should show:

- invalid JSON/JSONC;
- unknown setting;
- deprecated setting;
- invalid value;
- extension setting error;
- workspace setting blocked by trust;
- secret mistakenly stored warning;
- restart required warning;
- failed migration warning.

The panel should help users fix issues without losing settings.

## Workspace Trust relationship

Workspace Trust affects workspace/project settings.

Rules:

- untrusted workspace settings are limited;
- workspace settings cannot silently enable extension permissions;
- workspace settings cannot silently enable AI access;
- workspace settings cannot silently enable network access;
- workspace settings cannot silently enable terminal/shell access;
- workspace settings cannot silently enable Git operations;
- security-impacting settings require explicit user approval.

## Extension security relationship

Settings do not bypass extension security.

Rules:

- setting `extensions.someExtension.enabled` does not grant permissions;
- extension permissions remain explicit;
- extension telemetry remains denied by default;
- extension network access requires permission;
- extension workspace access requires permission.

## AI security relationship

Settings do not bypass AI security.

Rules:

- AI enabled does not mean workspace access granted;
- AI provider credential reference does not grant file access;
- AI workspace access remains scoped;
- prompt/response logging remains OFF by default;
- AI settings are logged/audited where relevant.

## First implementation recommendation

Operre v0.1 should include:

- Settings UI;
- searchable settings;
- category-based settings;
- modified indicators;
- Reset to Default;
- `settings.jsonc`;
- JSON schema validation;
- safe fallback on invalid settings;
- User settings;
- Workspace/Project settings;
- Machine-local settings separation;
- Secret Vault separation;
- privacy-first defaults;
- Settings Problems panel;
- schema version;
- migration-ready design.

First implementation may defer:

- full settings sync;
- full settings import/export;
- folder settings;
- per-language UI polish;
- complex extension setting UI;
- multi-device settings conflict resolution.

## Accepted decision summary

Accepted decisions:

- Settings UI is required.
- `settings.jsonc` is required.
- JSONC comments are accepted.
- JSON schema validation is required.
- Invalid settings must not crash Operre.
- Settings Problems panel is required by design.
- User settings and Workspace/Project settings are separate.
- Machine-local settings are separate and not synced by default.
- Secret/token/password values must not be stored in settings files.
- Secret Vault / OS keyring is separate from settings.
- Privacy/security defaults are OFF/safe by default.
- Settings search, Reset to Default, and modified indicators are required.
- Settings import/export may come later but must be designed safely.
- Settings schema version and migration are required by design.
- Workspace Trust can restrict workspace settings.
- Extension and AI settings cannot bypass permission systems.
- Detailed keyboard shortcut/keybinding behavior should be decided next.

## Keybindings settings relationship

Accepted behavior:

- Settings UI must include Keyboard Shortcuts.
- `keybindings.jsonc` is required.
- JSONC comments are accepted.
- Keybinding schema validation is required.
- Conflict detection is required.
- Reset shortcut and Reset all shortcuts are required.
- Settings Problems panel should show invalid keybindings.
- Workspace Trust can restrict workspace keybindings.
- On-screen keyboard, touch mode, and touch target preferences should be configurable where practical.

## Display, DPI, scaling, and responsive ergonomics settings relationship

Accepted behavior:

- Settings must include UI scale.
- Settings must keep editor font size separate from UI scale.
- Settings should include app UI font size, Markdown preview font size, sidebar font size, and status bar font size.
- Settings should include touch mode auto/on/off and touch target sizing where practical.
- Settings should include compact mode, sidebar default visibility, panel position, split direction, and compare layout.
- Settings should include safe window restore and window restore behavior.
- Machine-local display state must not sync by default.

## Command Palette and warning settings relationship

Accepted behavior:

- Settings must include Command Palette shortcut.
- Settings should include show command IDs on/off.
- Settings should include show disabled commands on/off.
- Settings should include show recent commands on/off.
- Settings should include max recent commands.
- Settings should include command result density.
- Settings should include touch-friendly Command Palette mode.
- Error, warning, notification, and problem reporting behavior must have detailed Settings controls in a dedicated follow-up specification.
- Critical safety warnings must not be disabled casually.
- critical safety warnings must not be disabled silently.
- critical safety warnings must not be disabled casually.

## Error, warning, notification, and Problems settings relationship

Accepted behavior:

- Settings must expose warning and notification behavior where safe.
- Settings should include toast duration, info notifications, success notifications, warning banners, Problems auto-open, quiet mode, focus mode, grouping, max visible notifications, and notification retention.
- Settings should support per-category notification preferences later.
- Settings should support per-extension notification preferences later.
- Settings should support per-AI-agent warning preferences later.
- Critical safety warnings must not be disabled casually.
- Critical safety warnings must not be disabled silently.
- Diagnostics upload remains OFF by default.

## Logs and diagnostics export settings relationship

Accepted behavior:

- Settings must expose local logs on/off where safe.
- Settings must expose log level.
- Settings must expose max log size, max log files, and retention days.
- Settings must expose Clear Logs.
- Settings must expose Open Logs Folder.
- Settings must expose Export Diagnostics.
- Settings must expose diagnostics export path.
- Settings must expose redact paths in export.
- Settings must expose include debug logs as advanced.
- Settings must expose include security log summary as advanced.
- diagnostics upload is OFF by default.
- crash upload is OFF by default.
- logs are local-only by default.
- file contents are not included by default.
- AI prompts/responses are not included by default.
- secrets must be redacted.

## Crash recovery and unsaved work settings relationship

Accepted behavior:

- Settings must expose Crash Recovery where safe.
- Settings must expose Hot Exit.
- Settings must expose Session Restore.
- Auto Save remains separate and configurable.
- Settings should expose recovery retention days and max recovery size.
- Settings should expose Clear Recovery Data with confirmation.
- Recovery data is local-only and machine-local by default.
- Recovery content is not included in diagnostics export by default.
- AI and extensions cannot access recovery content by default.
- Disabling Crash Recovery or Hot Exit requires clear warning.

## Auto Save and file saving settings relationship

Accepted behavior:

- Auto Save is OFF by default.
- Auto Save can be enabled by user preference.
- Settings must expose Auto Save mode.
- Settings must expose Auto Save delay.
- Settings should expose Auto Save exclusions for large files and protected paths.
- Settings must expose save conflict behavior.
- Settings must expose default encoding and line-ending preservation behavior.
- Settings and keybindings require atomic write.
- Settings and keybindings require last-known-good backup.
- User file backup is not aggressive by default.

## Symlink, hardlink, special file, and watcher settings relationship

Accepted behavior:

- Settings should expose file watcher enabled.
- Settings should expose watcher backend auto/polling.
- Settings should expose polling interval and watcher excludes.
- Settings should expose follow symlinks in explorer.
- Settings should expose show symlink target path.
- Settings should expose warn on hardlinked files.
- Settings should expose auto reload clean files.
- Settings must confirm reload dirty files.
- Settings should expose network filesystem conservative mode.
- Settings should expose protected path watcher exclusion.

## File Explorer, workspace tree, File Info, tabs, and navigation settings relationship

Accepted behavior:

- Settings should expose show hidden files.
- Settings should expose protected path visibility mode.
- Settings should expose explorer row density.
- Settings should expose show file badges.
- Settings should expose sort folders first and sort mode.
- Settings should expose preview tabs enabled.
- Settings should expose confirm drag and drop and confirm recursive delete.
- Settings should expose auto reveal active file.
- Settings should expose breadcrumbs enabled.
- Settings should expose navigation history enabled.
- Settings should expose large workspace lazy loading and explorer excludes.

## Workbench chrome settings

Workbench chrome settings should include window.menuBarVisibility, workbench.toolbar.visible, workbench.toolbar.compact, workbench.toolbar.overflowBehavior, workbench.statusBar.visible, workbench.statusBar.compact, workbench.statusBar.showSecurityIndicators, workbench.statusBar.showEncoding, workbench.statusBar.showLineEndings, workbench.statusBar.showLanguageMode, workbench.titleBar.style, workbench.uiScale, workbench.touchMode, workbench.compactMode, workbench.reduceAnimations, workbench.minTouchTarget, workbench.autoDetectHighDPI, workbench.warnWhenChromeTooSmall, workbench.phoneLayoutMode, and workbench.tabletLayoutMode.

Invalid chrome settings must not make Operre unusable. Safe reset commands must remain available.

## Extension sync and device profile settings

Extension sync must be profile-aware and device-aware. Safe settings, keybindings, theme, extension IDs, extension enabled state, and extension version preferences may sync. UI scale, layout dimensions, panel size, sidebar width, touch mode, compact mode, window geometry, recent files, workspace trust, logs, diagnostics, secrets, local toolchain paths, runtime paths, and external process configuration remain machine-local by default.

## Extension permission settings

Extension permission settings should include extensions.permissions.updatePolicy, extensions.permissions.showInstallSummary, extensions.permissions.runtimePromptsEnabled, extensions.permissions.defaultDurationLowRisk, extensions.permissions.defaultDurationMediumRisk, extensions.permissions.defaultDurationHighRisk, extensions.permissions.defaultDurationVeryHighRisk, extensions.permissions.allowPersistentVeryHighRisk, extensions.permissions.syncGrants, extensions.permissions.localDeveloperMode, extensions.permissions.warnOnUnsignedLocalPackage, extensions.permissions.showDisabledDesktopRequiredCapabilities, extensions.permissions.showStatusBarSummary, extensions.permissions.showRiskBars, extensions.permissions.requireAcknowledgeForCritical, and extensions.permissions.recommendedDefaultsProfile.

Recommended defaults use update policy B, runtime prompts enabled, install summary enabled, sync grants disabled, Developer Mode disabled, unsigned package warning enabled, desktop-required capabilities visible, status bar summary enabled, risk bars enabled, and critical acknowledgement required.

## Workspace Trust settings

Workspace Trust settings should include workspace.trust.enabled, workspace.trust.showOpeningBar, workspace.trust.promptOnDangerousAction, workspace.trust.defaultState, workspace.trust.allowMachineTrust, workspace.trust.allowGlobalTrust, workspace.trust.syncTrust, workspace.trust.showStatusBarState, workspace.trust.showReviewNeeded, workspace.trust.showDisabledDesktopRequired, workspace.trust.requireAcknowledgeForCritical, workspace.trust.redactPathsInWarnings, workspace.trust.recheckOnRootChange, workspace.trust.recheckOnRemoteChange, and workspace.trust.recheckOnToolchainChange. Recommended defaults keep trust enabled, global trust disabled, trust sync disabled, status bar state enabled, review needed enabled, and critical acknowledgement required.

## Terminal and process execution settings

Terminal settings should include terminal.mode, terminal.availableModes,
terminal.defaultProfile.linux, terminal.defaultProfile.macos,
terminal.defaultProfile.windows, terminal.requireWorkspaceTrust,
terminal.requireCommandPreview, terminal.confirmLowRisk,
terminal.confirmMediumRisk, terminal.confirmHighRisk,
terminal.confirmVeryHighRisk, terminal.confirmCritical,
terminal.allowElevatedExecution, terminal.allowSudo,
terminal.allowAdmin, terminal.allowRootShell,
terminal.allowAiSuggestedCommands, terminal.allowAiApprovedExecution,
terminal.sanitizeEnvironment, terminal.redactEnvironment,
terminal.log.enabled, terminal.log.stdout, terminal.log.stderr,
terminal.log.commandPreview, terminal.log.environmentSummary,
terminal.log.retentionDays, terminal.log.maxSize,
terminal.output.maxVisibleLines, terminal.output.maxBytes,
terminal.process.maxConcurrent, terminal.process.defaultTimeoutSeconds,
terminal.showLogLinks, terminal.showWorkingDirectoryLinks,
terminal.phone.showSafeSummaries, and terminal.tablet.showSafeSummaries.

## External toolchain settings

External toolchain settings should include operre.worksRoot,
toolchains.enabled, toolchains.discovery.enabled,
toolchains.discovery.passive, toolchains.discovery.verified,
toolchains.install.mode, toolchains.install.allowHelper,
toolchains.install.allowCuratedInstaller,
toolchains.requireProfileApproval, toolchains.requireWorkspaceTrust,
toolchains.requireCommandPreview, toolchains.allowProfileTemplateSync,
toolchains.syncExecutableApprovals, toolchains.syncExecutablePaths,
toolchains.syncSecrets, toolchains.productionGuard.enabled,
toolchains.remote.enabled, toolchains.dashboard.enabled,
toolchains.safeReset.enabled, resourceGovernor.enabled,
resourceGovernor.defaultTimeoutSeconds,
resourceGovernor.defaultIdleTimeoutSeconds,
resourceGovernor.maxOutputBytes, resourceGovernor.maxLogBytes,
resourceGovernor.maxConcurrentProcesses, resourceGovernor.restartLimit,
sandbox.fileScope.enabled, sandbox.networkScope.enabled,
sandbox.platformSandbox.enabledLater, python.preferProjectVenv,
cpp.requireSeparateRunApproval, node.warnOnInstallScripts,
database.productionGuardDefault, webServer.defaultBindAddress, and
ai.toolchainAdvisoryOnly.

## Managed project settings

Managed project settings should include operre.worksRoot,
projects.defaultMode, projects.createManagedByDefault,
projects.externalWritePolicy, projects.folderCreationMode,
projects.dashboard.defaultOpenMode, projects.dashboard.showOnFirstOpen,
projects.dashboard.sidebarAccess, projects.dashboard.statusBarAccess,
projects.dashboard.showSecuritySummary,
projects.dashboard.showToolchainsSummary,
projects.dashboard.showOutputsSummary, projects.dashboard.showLogsSummary,
projects.dashboard.showArtifactsSummary,
projects.dashboard.showResourceSummary, projects.dashboard.showSafeReset,
projects.templates.enabled, projects.templates.allowLocalTemplates,
projects.templates.allowImportedTemplates,
projects.templates.allowMarketplaceTemplatesLater,
projects.templates.requirePreview, projects.cleanup.enabled,
projects.cleanup.maxLogAgeDays, projects.cleanup.maxLogBytes,
projects.cleanup.maxOutputBytes, projects.cleanup.maxSpoolBytes,
projects.cleanup.protectPinnedArtifacts, projects.safeReset.enabled, and
projects.mobile.safeSummaryMode.

## Marketplace and extension update settings

Marketplace and update settings should include extensions.marketplace.enabled,
extensions.marketplace.publicEnabled,
extensions.marketplace.privateRegistryEnabled,
extensions.marketplace.unknownUrlImportEnabled,
extensions.package.format, extensions.package.requirePreview,
extensions.package.verifyHashes,
extensions.package.requireSignatureForHighRisk,
extensions.signing.enabledLater, extensions.publisher.trustEnabled,
extensions.publisher.blockEnabled, extensions.update.policy,
extensions.update.autoCheck, extensions.update.autoInstall,
extensions.update.requirePermissionDiff, extensions.update.showYellowBar,
extensions.rollback.enabled, extensions.quarantine.enabled,
extensions.developerMode.enabled, extensions.developerMode.sessionOnly,
extensions.offlineInstall.enabled, extensions.phone.safeMarketplaceMode,
extensions.tablet.safeMarketplaceMode,
extensions.privacy.telemetryUpload, extensions.privacy.crashUpload,
extensions.privacy.usageUpload, and extensions.review.enabledLater.

## Settings sync and device profile relationship

Settings must separate local, per-device, profile-level, synced,
risky-sync, and never-silent-sync settings. Account is optional for core
local use. Sync is off by default. Device profiles are required. Safe
reset should show current value, recommended value, risk label, scope,
sync state, and device override state.
