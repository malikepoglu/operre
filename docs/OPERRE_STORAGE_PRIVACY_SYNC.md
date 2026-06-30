# Operre Storage, Privacy, and Sync

## User workspace

Default user workspace path must avoid spaces.

Linux/macOS:

- `~/Operre/Works/`

Windows:

- `%USERPROFILE%\Operre\Works\`

## Workspace folders

Default user workspace structure:

- `~/Operre/Works/Notes/`
- `~/Operre/Works/Projects/`
- `~/Operre/Works/Diagrams/`
- `~/Operre/Works/Cad/`
- `~/Operre/Works/Exports/`
- `~/Operre/Works/Scratch/`
- `~/Operre/Works/Templates/`

Rules:

- Diagrams and Cad must be separate.
- Users may change the default workspace path.
- Users without a formal project can save simple notes into the default workspace or their chosen directory.

## Installed extension code

Installed/runnable extension code must be separated from user work data.

Linux:

- `~/.local/share/operre/extensions/`

Windows:

- `%APPDATA%\Operre\extensions\`

macOS:

- `~/Library/Application Support/Operre/extensions/`

## Application configuration

Linux:

- `~/.config/operre/`

Windows:

- `%APPDATA%\Operre\config\`

macOS:

- `~/Library/Application Support/Operre/config/`

Example files:

- settings.json;
- keybindings.json;
- workspace-defaults.json;
- extensions-enabled.json.

## Cache / temporary / generated data

Linux:

- `~/.cache/operre/`

Windows:

- `%LOCALAPPDATA%\Operre\cache\`

macOS:

- `~/Library/Caches/Operre/`

Possible subfolders:

- preview-cache/;
- syntax-cache/;
- thumbnail-cache/;
- extension-cache/;
- download-cache/;
- temporary-build-cache/.

Security rules:

- cache is not trusted;
- no secrets in cache;
- no tokens in cache;
- no private keys in cache;
- no executable trust from cache;
- path traversal must be blocked;
- symlink escape must be blocked;
- cross-project data mixing must be blocked;
- cache must be cleanable.

## Logs and audit records

Linux:

- `~/.local/state/operre/logs/`

Windows:

- `%LOCALAPPDATA%\Operre\logs\`

macOS:

- `~/Library/Logs/Operre/`

Logs may include:

- application logs;
- crash logs;
- extension audit logs;
- security events;
- AI connector system logs.

## Default privacy mode

Default privacy mode:

- Strict Privacy.

Defaults:

- crash upload: OFF;
- telemetry: OFF;
- diagnostics upload: OFF;
- local safe logs: ON;
- user-reviewed diagnostics export: allowed.

## Crash report policy

Acceptable crash report fields, if user explicitly opts in later:

- Operre version;
- OS type;
- OS version;
- CPU architecture;
- Tauri version;
- WebView type/version;
- crash timestamp;
- crash module;
- error code;
- stack trace;
- extension id/version if extension-related.

Must not be uploaded by default:

- source code;
- document contents;
- clipboard contents;
- full file paths;
- user name;
- home directory path;
- GitHub token;
- SSH key;
- `.env` content;
- API key;
- project name;
- repo URL;
- commit message;
- terminal command history.

## Telemetry policy

Telemetry is off by default.

If ever added, it must be opt-in and must avoid:

- opened file names;
- project names;
- document contents;
- source code;
- typed words;
- repo URLs;
- GitHub account data;
- full paths;
- extension-specific sensitive usage.

## Extension telemetry

Extension telemetry is denied by default.

Any extension telemetry requires separate explicit user permission.

## `.operre/` hybrid Git model

Default:

- `.operre/` ignored by Git.

Optional tracked:

- `.operre/shared/`

Always ignored:

- `.operre/audit/`;
- `.operre/secrets/`;
- `.operre/cache/`;
- `.operre/local-state/`;
- `.operre/snapshots/`.

AI audit logs and prompt/response logs are Git-ignored by default.

## Sync strategy

Operre may need servers for:

- app operation;
- extension system;
- extension marketplace/distribution;
- licensing;
- updates;
- account services.

But user-created work data should be local-first by default.

Examples:

- TODO lists;
- work plans;
- service plans;
- notes;
- project docs;
- personal boards;
- local project metadata.

Sync is allowed, but:

- explicit;
- configurable;
- extension/data-domain level;
- not mandatory core cloud dependency.

All Operre apps across environments should eventually be able to sync, but exact details remain future design work.

User-owned sync is important:

- user devices;
- user storage;
- self-hosted storage;
- chosen ecosystem;
- no mandatory upload to Operre servers.

## Source 2 sync baseline

The `2.odt` review confirms the local-first sync direction.

Accepted sync principles:

- User work data is local-first.
- Operre cloud must not be required for user work data.
- Sync is optional.
- Sync is explicit.
- Sync may be implemented by extension/data-domain.
- User-owned sync is important.

User-owned sync may include:

- user's own devices;
- user's own storage;
- self-hosted storage;
- user's chosen ecosystem.

Operre servers may still exist for:

- app operation;
- extension system;
- extension marketplace/distribution;
- licensing;
- updates;
- account services.

These services must not turn core local work into mandatory cloud work.

## Source 3 privacy and metadata baseline

The `3.odt` review confirms the privacy/logging and `.operre/` metadata baseline.

Accepted privacy defaults:

- Strict Privacy default.
- Crash upload OFF.
- Telemetry OFF.
- Diagnostics upload OFF.
- Local safe logs ON.
- Extension telemetry denied by default.

Accepted `.operre/` Git model:

- `.operre/` ignored by default.
- `.operre/shared/` may be tracked if explicitly chosen.
- `.operre/audit/` always ignored.
- `.operre/secrets/` always ignored.
- `.operre/cache/` always ignored.
- `.operre/local-state/` always ignored.
- `.operre/snapshots/` always ignored.

## Hidden/protected path storage baseline

Accepted storage behavior:

- `.operre/` is hidden by default.
- `.operre/shared/` is the only optional shared/tracked subtree.
- `.operre/audit/` is always protected.
- `.operre/secrets/` is always protected.
- `.operre/cache/` is always protected.
- `.operre/local-state/` is always protected.
- `.operre/snapshots/` is always protected.
- Protected paths are excluded from normal search, recent history, automatic indexing, AI context, diagnostics, and sync by default.

## Large file cache baseline

Accepted storage/cache behavior:

- Large file cache is local-only.
- Cache must be bounded by size limits.
- Cache must be cleanable by the user.
- Cache must not be synced by default.
- Cache must not be committed.
- Cache must not store secrets by design.
- Cache follows protected path rules.
- Workspace/project isolation must be respected.

## Recent files/projects storage baseline

Accepted storage behavior:

- Recent history is local-only by default.
- Recent history is state, not logs.
- Recent history should not be stored under log paths.
- Suggested Linux path is `~/.local/state/operre/recent/`.
- Suggested Windows path is `%LOCALAPPDATA%\Operre\recent\`.
- Suggested macOS path is `~/Library/Application Support/Operre/recent/`.
- Recent history sync is OFF by default.
- Recent history export is not first core.
- Sensitive/protected entries are excluded by default.

## Settings storage baseline

Accepted storage behavior:

- User settings use `settings.jsonc`.
- Suggested Linux user settings path is `~/.config/operre/settings.jsonc`.
- Workspace/project shared settings may use `.operre/shared/settings.jsonc`.
- Machine-local settings live separately under local state.
- Machine-local settings are not synced by default.
- Secret values must not be stored in settings files.
- Settings sync is OFF by default.
- Settings import/export must exclude secrets by default.

## Keybinding storage baseline

Accepted storage behavior:

- User keybindings use `keybindings.jsonc`.
- Suggested Linux user keybindings path is `~/.config/operre/keybindings.jsonc`.
- Suggested Windows user keybindings path is `%APPDATA%\Operre\config\keybindings.jsonc`.
- Suggested macOS user keybindings path is `~/Library/Application Support/Operre/config/keybindings.jsonc`.
- Workspace shared keybindings may use `.operre/shared/keybindings.jsonc`.
- Machine-local keybinding overrides, if needed, stay under local state.
- Machine-local keybindings are not synced by default.

## Display and window state storage baseline

Accepted storage behavior:

- Window size and position are machine-local state.
- Fullscreen/maximized state is machine-local state.
- Monitor identity and monitor-specific display state are machine-local state.
- Machine-local display state must not sync by default.
- Safe window restore must prevent restoring unusable off-screen windows.
- User display preferences may live in settings, but raw monitor/window state stays local.

## Error logs and diagnostics storage baseline

Accepted storage behavior:

- Logs are local-only by default.
- Logs must not store secrets by design.
- Logs must not store file contents by default.
- Logs must not store AI prompt/response content by default.
- Diagnostics upload is OFF by default.
- Diagnostics export requires explicit user action and confirmation.
- Paths/settings may be redacted in diagnostics export.

## Logs and diagnostics storage baseline

Accepted storage behavior:

- Logs are machine-local state.
- Logs are local-only by default.
- Diagnostics export files are user-created files.
- Diagnostics export files do not sync automatically through Operre by default.
- Diagnostics upload is OFF by default.
- Crash upload is OFF by default.
- File contents are not included by default.
- AI prompts/responses are not included by default.
- Secrets must be redacted before export.

## Crash recovery storage baseline

Accepted storage behavior:

- Recovery data is machine-local state.
- Recovery data is local-only by default.
- Recovery data does not sync by default.
- Recovery content is not included in diagnostics export by default.
- Recovery content is not exposed to AI/extensions by default.
- Recovery retention and max size must be configurable by design.

## Auto Save and backup storage baseline

Accepted storage behavior:

- Settings/keybindings backups are app state/config data.
- User file sidecar backups are not created by default.
- Backup/recovery content is not included in diagnostics export by default.
- Backup/recovery content is not exposed to AI/extensions by default.
- Backup retention must be configurable where backups are enabled.

## Symlink, hardlink, special file, and watcher storage baseline

Accepted storage behavior:

- Watcher state is machine-local.
- Watcher event history is not synced by default.
- Watcher event history is not exported by default.
- Protected path watcher data must remain privacy-first.
- File identity metadata may be stored only where useful and safe.
