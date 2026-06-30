# Operre AI Agent Security

## AI category

AI agents are optional Connector Extensions.

Examples:

- Codex-like connector;
- Claude-like connector;
- local LLM connector;
- custom API connector;
- self-hosted agent connector.

AI must not be part of core.

## Default restrictions

AI agents cannot by default:

- read the full workspace;
- edit files;
- run commands;
- access Git;
- access terminal;
- access secrets;
- send data to network destinations;
- push;
- commit.

## Allowed access

AI agents may access only:

- selected files;
- selected folders;
- selected project context;

and only after explicit scoped permission.

## Edit rule

All AI-made edits must be shown as diff before apply.

AI must not silently change anything.

## Audit logging

Every AI agent action must be logged one by one.

Log fields should include:

- timestamp;
- agent/connector id;
- model/provider;
- requested action;
- granted permissions;
- selected files/folders;
- read operations;
- proposed edits;
- diff before apply;
- user approval/rejection;
- executed commands if any;
- Git actions if any;
- network destinations if any;
- errors/warnings.

## Prompt/response logging

Prompt/response logging:

- default: OFF;
- optional: ON per project/per agent;
- preferred mode: redacted;
- full mode: explicit warning required.

Reason:

- prompt/response may contain source code, secrets, or private information.

## Project-local AI audit storage

Project-related AI actions:

- `~/Operre/Works/Projects/<project>/.operre/audit/ai-agents/`

Possible substructure:

- yearly/monthly JSONL logs;
- diffs directory;
- exports directory;
- optional prompt/response directory only if enabled.

## Global AI logs

Linux:

- `~/.local/state/operre/logs/ai-agents/`

Windows:

- `%LOCALAPPDATA%\Operre\logs\ai-agents\`

macOS:

- `~/Library/Logs/Operre/ai-agents/`

Global logs are for:

- connector startup/shutdown;
- provider errors;
- authentication failures;
- permission denials;
- rate limits;
- extension crashes;
- blocked network destinations;
- security policy violations.

## Format

Preferred format:

- JSON Lines for event logs;
- `.diff` files for proposed edits;
- optional redacted prompt/response Markdown if user enables it.

AI agent should not write arbitrary audit logs directly.

Rule:

- AI logs must go through Operre Core Audit API.

## Hard security rule

AI cannot silently:

- read everything;
- write files;
- run commands;
- push/commit;
- send data;
- access secrets;
- change settings;
- approve its own diff.

## Source 3 AI security baseline

The `3.odt` review confirms the AI agent baseline.

Accepted principles:

- AI agents are optional Connector Extensions.
- AI is not core.
- AI cannot read the full workspace by default.
- AI cannot edit files by default.
- AI cannot run commands by default.
- AI cannot access Git by default.
- AI cannot access terminal by default.
- AI cannot access secrets by default.
- AI cannot send data by default.
- AI cannot push or commit by default.
- AI edits require diff before apply.
- AI cannot silently change anything.
- AI cannot approve its own diff.
- Every AI action must be logged one by one.

Prompt/response logging:

- default OFF;
- optional per project/per agent;
- redacted preferred;
- full mode only with explicit warning.

## Hidden/protected path AI baseline

Accepted AI behavior:

- AI agents cannot access hidden/protected paths by default.
- AI default exclusions include `.git/`, `.operre/`, `.env`, `.env.*`, `.ssh/`, secrets, tokens, credentials, private keys, caches, logs, and snapshots.
- AI access to hidden files requires explicit scoped permission.
- AI access to protected secrets remains denied by default.

## Search/compare AI access baseline

Accepted AI behavior:

- AI cannot access search results by default.
- AI cannot access compared file contents by default.
- AI cannot use search/compare as hidden workspace context without explicit scoped permission.
- Protected/sensitive paths remain denied by default even if AI is granted normal workspace context.

## Large file AI access baseline

Accepted AI behavior:

- AI cannot access large file content by default.
- AI access to large files must be scoped and explicit.
- Selected ranges are preferred over whole large files.
- User must see what content is sent where practical.
- Protected/sensitive paths remain denied by default.

## Recent history AI access baseline

Accepted AI behavior:

- AI cannot access recent history by default.
- AI cannot use recent history as hidden project context.
- If AI access is ever allowed, explicit scoped permission is required.
- Sensitive/protected entries remain excluded.
- Access must be logged.

## Settings and AI security baseline

Accepted AI behavior:

- AI agents default OFF.
- AI workspace access default OFF.
- AI credentials are not stored as plaintext settings.
- AI settings cannot bypass scoped permission requirements.
- Prompt/response logging remains OFF by default.
- Per-project/per-agent overrides may exist but remain governed by privacy and Workspace Trust.

## Keybindings and AI security baseline

Accepted AI behavior:

- AI commands should not receive broad default shortcuts in first core.
- AI shortcuts cannot silently enable workspace access.
- AI shortcuts cannot bypass scoped permissions.
- AI shortcuts cannot silently change prompt/response logging.
- AI shortcut actions must respect audit logging.

## Command Palette and AI command baseline

Accepted AI behavior:

- AI commands default OFF or limited in first core.
- AI commands cannot silently enable workspace access.
- AI commands cannot bypass scoped permissions.
- AI commands cannot bypass Workspace Trust.
- AI commands must follow AI audit rules.
- Prompt/response logging cannot be silently changed by command.

## AI warning and problem baseline

Accepted AI behavior:

- AI warnings must include permission requirements, protected path denials, workspace access restrictions, missing credentials, and logged actions.
- AI commands must not bypass warning/confirmation policy.
- AI prompt/response content is not included in diagnostics automatically.
- AI access to warning/error history is denied by default.

## AI logs and diagnostics baseline

Accepted AI behavior:

- AI action summaries may be included in diagnostics where safe.
- AI prompts/responses are not included by default.
- AI provider credentials are never included.
- AI read-file lists may be redacted or summarized.
- AI access to logs/diagnostics history is denied by default.

## AI recovery boundary baseline

Accepted AI behavior:

- AI cannot access recovery content by default.
- AI cannot silently read recovered buffers.
- AI cannot include recovery content in prompts automatically.
- AI proposed edits to recovered content require user review.
- AI recovery access, if ever added, requires explicit scoped permission.

## AI save boundary baseline

Accepted AI behavior:

- AI cannot silently save user files.
- AI proposed edits require user review according to AI policy.
- AI cannot bypass save conflict handling.
- AI cannot bypass protected path save warnings.
- AI cannot access backup/recovery content by default.

## AI watcher boundary baseline

Accepted AI behavior:

- AI cannot receive watcher event history by default.
- AI cannot monitor protected paths.
- AI requires explicit scoped permission for workspace-change awareness later.
- Raw watcher events are not hidden prompt context.
- AI may explain visible file-changed warnings only from user-visible context.

## AI Explorer and navigation boundary baseline

Accepted AI behavior:

- AI cannot read Explorer tree by default.
- AI cannot read navigation history by default.
- AI cannot read protected paths by default.
- AI workspace tree summary requires explicit scoped permission later.
- AI cannot use hidden watcher/tree state as hidden prompt context.
- AI suggestions for file operations require user confirmation.

## AI access to operational panels

AI cannot read Problems, Search Results, Output, Logs, or Diagnostics by default. The user must grant scoped access to a specific panel, session, and content type before AI can summarize or act on that data. Safe summaries may be exposed only through explicit permission. Protected path details, secrets, full logs, full output, diagnostics bundles, AI prompts, and AI responses remain denied or redacted by default.

## AI and extension boundary

Extensions cannot grant AI access to data that the user did not explicitly authorize. AI connectors are high-risk extensions and must require scoped permission, audit logging, privacy summaries, and Workspace Trust where project data or tool execution is involved. Open UI does not imply AI data access.

## AI permission prompts and extension requests

AI access requested by an extension is a very-high-risk permission. It requires runtime critical prompt, scoped grant, duration choice, Workspace Trust where project data is involved, visible audit logging, and revocation support. Extension UI visibility never grants AI data access. Open UI does not imply data access.

## Workspace Trust and AI access

AI workspace access requires Workspace Trust where project data is involved. AI cannot use visible workspace UI as hidden data access. Open UI does not imply data access. In untrusted workspaces, AI workspace read, AI tool execution, and AI-assisted external toolchain actions remain locked unless a later explicit trusted flow allows them.
