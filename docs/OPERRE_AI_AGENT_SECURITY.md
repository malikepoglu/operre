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
