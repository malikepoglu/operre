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
