# Operre Logs and Diagnostics Export Behavior

## Purpose

This document defines Operre's local logs, diagnostics export, privacy-first logging rules, redaction rules, upload policy, crash log behavior, security audit logs, AI/extension log boundaries, and Settings/Command Palette integration.

This decision follows the error, warning, notification, and problem reporting behavior decision.

## Core principle

Logs must help debug problems without leaking private data.

Diagnostics export must be explicit and user-controlled.

logs are local-only by default.

Diagnostics upload is OFF by default.

Crash upload is OFF by default.

Automatic diagnostics upload is forbidden by default.

file contents are not included by default.

AI prompts/responses are not included by default.

secrets must be redacted.

## Local-only logs

Operre logs are local-only by default.

Rules:

- no automatic upload;
- no hidden telemetry upload;
- no extension access by default;
- no AI access by default;
- no cloud sync by default;
- user can clear logs;
- user can open logs folder;
- user can manually export diagnostics.

## Log categories

Operre may use separate log categories.

Suggested categories:

- `app.log`;
- `errors.log`;
- `warnings.log`;
- `security.log`;
- `extension.log`;
- `ai-agents.log`;
- `diagnostics.log`;
- `performance.log` later;
- `update.log` later;
- `crash-recovery.log`;
- `file-operations.log`;
- `command-execution.log` for security-relevant commands only.

First implementation may use fewer physical files, but the logical categories should exist by design.

## Log levels

Supported log levels should include:

- trace;
- debug;
- info;
- warn;
- error;
- critical;
- security.

Default behavior:

- normal users should use info/warn/error;
- debug is OFF by default;
- trace is OFF by default;
- security-relevant events may use separate security level/category;
- debug/trace export requires explicit user choice.

## Privacy-first log rules

Logs must avoid storing sensitive content by default.

Logs must not include by default:

- file contents;
- raw clipboard content;
- secrets;
- tokens;
- passwords;
- API keys;
- private keys;
- AI provider keys;
- AI prompts/responses;
- full workspace dumps;
- full search results;
- full compare contents;
- hidden/protected path contents;
- raw diagnostics without redaction;
- raw `.env` contents;
- raw credential files.

## Path handling

Path information can be useful for debugging, but it can also be private.

Accepted behavior:

- local logs may include paths where necessary;
- diagnostics export should support path redaction;
- protected paths should be redacted in export by default;
- secret-looking path segments should be redacted;
- export preview should show whether path redaction is enabled;
- full paths in export should be advanced and warning-protected.

## Secret redaction

Diagnostics export must include redaction.

Redaction should detect or protect:

- API keys;
- tokens;
- passwords;
- SSH private key blocks;
- OAuth refresh tokens;
- GitHub tokens;
- AI provider keys;
- `.env` values;
- credential JSON;
- bearer tokens;
- connection strings;
- private key material;
- secret-like setting values.

Redaction is required before diagnostics export.

## Log storage paths

Suggested log paths:

Linux:

- `~/.local/state/operre/logs/`

Windows:

- `%LOCALAPPDATA%\Operre\logs\`

macOS:

- `~/Library/Logs/Operre/`

Suggested diagnostics export output location:

- `~/Operre/Works/Exports/Diagnostics/`

The user may choose another export location.

## Log rotation and retention

Operre must support log rotation and retention.

Settings should include:

- max log size;
- max log files;
- retention days;
- clear logs;
- clear only old logs;
- include debug logs on/off;
- include security logs in export on/off with warning;
- compress diagnostics export on/off.

Default behavior:

- limited log size;
- limited retention;
- local-only;
- privacy-safe defaults.

## Diagnostics export

Diagnostics export must be user-initiated.

Diagnostics export may include:

- app version;
- OS/platform summary;
- renderer/backend versions;
- settings summary, redacted;
- enabled extensions list;
- extension errors summary;
- recent crash summary;
- error/warning summary;
- redacted logs;
- system display/DPI summary;
- workspace trust state;
- large file mode events;
- command failures;
- diagnostics manifest.

Diagnostics export must not include by default:

- file contents;
- secrets;
- AI prompts/responses;
- raw hidden/protected contents;
- raw `.env`;
- raw credentials;
- full recent history;
- full search history;
- full compare contents;
- clipboard contents.

## Export preview

Diagnostics export should show a preview before creation.

Preview should include:

- what will be included;
- what will be excluded;
- number of log files;
- estimated size;
- redaction status;
- path redaction on/off;
- AI content included status, default no;
- secrets detected warning;
- full path warning if enabled;
- user confirmation.

## Export format

Diagnostics export format should be structured.

Suggested package:

- zip initially;
- tar.zst later if useful;
- `manifest.json`;
- `diagnostics-report.md`;
- `logs/`;
- `summaries/`;
- `system/`;
- `settings-redacted.json`;
- `extensions-summary.json`;
- `ai-summary.json` where safe;
- `security-summary.json` where safe.

The manifest should describe included files and redaction state.

## Upload policy

Diagnostics upload is OFF by default.

Crash upload is OFF by default.

Automatic diagnostics upload is forbidden by default.

Rules:

- no automatic upload;
- no crash upload by default;
- no telemetry upload by default;
- user-created export only;
- future upload feature requires explicit consent;
- future upload feature must show preview/summary;
- future upload feature must not include secrets/file contents/AI content by default.

## Crash logs and crash recovery

Crash logs may be local.

Rules:

- crash logs are local-only by default;
- crash upload is OFF by default;
- crash logs must not include file contents by default;
- crash logs must not include AI prompts/responses by default;
- crash recovery data is a separate topic;
- unsaved buffer recovery needs its own dedicated behavior decision;
- crash report export is manual.

## Security audit logs

Security audit logs may be separate.

Security audit events may include:

- extension permission grant/deny;
- AI permission grant/deny;
- protected path access blocked;
- secret-like value detected;
- diagnostics export created;
- settings import/export;
- workspace trust changes;
- dangerous command confirmations;
- future shell permission events;
- future Git destructive command confirmations;
- future network permission events;
- credential access denial.

Security logs must be privacy-safe.

## AI logs relationship

AI logging follows the AI security model.

Diagnostics export default behavior:

- AI action summary may be included;
- AI prompt/response content is not included by default;
- AI provider credentials are never included;
- AI read-file lists may be redacted or summarized;
- AI proposed edits may be summarized;
- AI audit entries remain scoped and privacy-controlled.

## Extension logs relationship

Extension logs may include:

- extension ID;
- extension version;
- command failure;
- activation failure;
- permission denied;
- crash/slow warning;
- blocked network attempt;
- protected path blocked;
- invalid extension settings.

Extension logs must not include by default:

- extension raw data dumps;
- extension secrets;
- user file contents;
- hidden/protected path contents.

Extension telemetry remains denied by default.

## Command Palette relationship

Command Palette should expose logs and diagnostics commands.

Suggested commands:

- `logs.openFolder`;
- `logs.clear`;
- `logs.clearOld`;
- `diagnostics.export`;
- `diagnostics.openSettings`;
- `diagnostics.showLastErrorDetails`;
- `security.openLogSummary`;
- `crash.openRecoveryInfo` later.

Rules:

- diagnostics export requires confirmation;
- security log export requires warning;
- clearing logs requires confirmation when destructive;
- Command Palette must not bypass privacy warnings.

## Settings

Settings should include:

- local logs on/off;
- log level;
- max log size;
- max log files;
- retention days;
- clear logs;
- diagnostics export path;
- include system info;
- include settings summary;
- include extension summary;
- include AI summary;
- include security log summary;
- redact paths in export;
- include full paths in export, advanced with warning;
- include debug logs, advanced;
- include security logs, advanced with warning;
- diagnostics upload OFF;
- crash upload OFF;
- open logs folder;
- export diagnostics.

Required settings facts:

- diagnostics upload is OFF by default.
- crash upload is OFF by default.
- logs are local-only by default.
- file contents are not included by default.
- AI prompts/responses are not included by default.
- secrets must be redacted.

## Accessibility and ergonomics

Diagnostics and log UI must be accessible.

Rules:

- export dialog must be keyboard navigable;
- export dialog must be touch-friendly;
- on-screen keyboard must not hide important inputs where practical;
- high-DPI rendering must be crisp;
- high contrast must be supported;
- redaction warnings must not rely only on color;
- destructive actions must have clear confirmation.

## Storage and sync

Logs and diagnostics state are machine-local.

Rules:

- logs are machine-local;
- diagnostics exports are user files;
- raw logs do not sync by default;
- diagnostics export files do not sync automatically through Operre by default;
- log settings may be user settings where safe;
- raw monitor/system details remain local unless exported manually;
- secret redaction happens before export.

## First implementation recommendation

Operre v0.1 should include:

- local logs;
- limited retention;
- log clearing command;
- open logs folder command;
- manual diagnostics export;
- diagnostics export preview;
- redacted diagnostics summary;
- no automatic upload;
- diagnostics upload OFF by default;
- crash upload OFF by default;
- no file contents by default;
- no secrets by default;
- no AI prompts/responses by default;
- Settings controls;
- Command Palette commands;
- security-relevant event summary.

First version may defer:

- advanced log viewers;
- advanced per-category retention;
- automatic crash report upload;
- sound/notification integration;
- complete structured diagnostics schema;
- tar.zst export format;
- full security audit UI.

## Accepted decision summary

Accepted decisions:

- Logs and diagnostics export behavior must have a dedicated specification.
- Logs are local-only by default.
- Diagnostics upload is OFF by default.
- Crash upload is OFF by default.
- Automatic diagnostics upload is forbidden by default.
- Diagnostics export is user-initiated only.
- Diagnostics export should show preview/summary before creation.
- Secret redaction is required.
- File contents are not included by default.
- AI prompts/responses are not included by default.
- Paths may be redacted in diagnostics export.
- Protected paths are redacted/excluded by default.
- Log rotation and retention are required by design.
- Settings must expose log level, retention, clear logs, export diagnostics, path redaction, diagnostics upload OFF, and crash upload OFF.
- Command Palette must expose Open Logs Folder, Clear Logs, Export Diagnostics, and related diagnostics commands.
- Extension/AI/security events may be included as summaries where safe.
- Detailed crash recovery and unsaved work recovery behavior should be decided next.

## Crash recovery and logs relationship

Accepted behavior:

- Crash summary may be logged.
- Recovery content must not be logged.
- Recovery content is not included in diagnostics export by default.
- Recovery metadata may be included only as redacted/summarized information.
- Safe Mode launch summary may be included in diagnostics where safe.

## Auto Save and file saving logs relationship

Accepted behavior:

- Save failures may be logged.
- File contents are not logged.
- Dirty buffer contents are not logged.
- Backup/recovery content is not logged.
- Diagnostics export may include save error summaries.
- Backup/recovery content is not included in diagnostics export by default.

## Symlink, hardlink, special file, and watcher logs relationship

Accepted behavior:

- Watcher errors may be logged.
- File contents are not logged.
- Watcher event history is not exported by default.
- Protected raw paths may be redacted.
- Diagnostics may include watcher limited/overflow summary.
- Diagnostics must not include protected contents.

## File Explorer, workspace tree, File Info, tabs, and navigation logs relationship

Accepted behavior:

- File operation failures may be logged.
- File contents are not logged.
- Protected raw paths may be redacted.
- Navigation history is not exported by default.
- Explorer tree snapshot is not exported by default.
- Diagnostics may include watcher limited/overflow summaries and safe UI state summaries.
