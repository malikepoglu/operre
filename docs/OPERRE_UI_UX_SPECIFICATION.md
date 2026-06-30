# Operre UI/UX Specification

## UI reference

Operre should learn from VS Code usability but remain smaller and lighter.

Operre is not a VS Code clone.

## Startup screen

Startup screen should show:

- recent files/projects;
- restore previous session / reopen open files;
- new text file;
- new Markdown note;
- open file;
- open folder/project;
- Operre Works shortcut.

## Session restore

Session restore:

- default: ON;
- user can disable it.

Saved:

- open files;
- open folder/project;
- active tab;
- cursor position;
- scroll position;
- split/panel layout.

Not saved:

- file contents;
- clipboard;
- secrets/tokens;
- prompt/AI content.

## Autosave

Autosave:

- default: OFF.

Possible later options:

- OFF;
- after delay;
- on focus lost;
- prompt on window close.

Default behavior:

- user controls saving;
- Operre does not silently overwrite user files.

## Dirty/unsaved behavior

Rules:

- dirty tab indicator: `*`;
- close warning;
- choices: Save / Don't Save / Cancel;
- local recovery snapshot may exist for crash recovery.

## Crash recovery

Crash recovery:

- default: ON;
- local-only;
- cloud-disabled;
- user-configurable.

Opening order:

1. If crash recovery exists, show recovery screen.
2. User chooses Recover / Discard / Compare if possible.
3. After recovery decision, normal session restore may run.
4. If no recovery exists, normal startup flow runs.

Crash recovery must never silently overwrite files.

Retention:

- default: 7 days;
- options: 1 day, 7 days, 30 days, manual only.

## Tabs

Tab system:

- multiple tabs supported;
- dirty tab indicator: `*`;
- close tab button;
- reopen closed tab;
- pin tab later;
- tab restore through session restore.

## Split editor

Split editor:

- first version: side-by-side vertical split;
- horizontal split later;
- session restore remembers split layout.

## Minimap

Minimap:

- default: ON;
- position: right.

Settings:

- on/off;
- left/right;
- width small/medium/large;
- adaptive tablet/phone/small-screen behavior.

## Status Bar

Status Bar:

- bottom bar;
- file type;
- encoding;
- BOM yes/no;
- LF/CRLF;
- Spaces/Tabs;
- cursor position: Ln, Col;
- dirty/saved state;
- workspace trust status;
- extension warnings.

## Command Palette

Command Palette shortcut:

- Ctrl+Shift+P

Initial commands:

- New Text File;
- New Markdown Note;
- Open File;
- Open Folder;
- Save;
- Save As;
- Toggle Markdown Preview;
- Toggle Minimap;
- Change Theme;
- Convert Line Endings;
- Convert Indentation;
- Manage Extensions.

## Keyboard shortcuts

Keyboard shortcuts must be configurable.

Defaults:

- Ctrl+N: New File;
- Ctrl+O: Open File;
- Ctrl+S: Save;
- Ctrl+Shift+S: Save As;
- Ctrl+W: Close Tab;
- Ctrl+Shift+T: Reopen Closed Tab;
- Ctrl+F: Find;
- Ctrl+H: Replace;
- Ctrl+Shift+P: Command Palette.

Users can customize through:

- keybindings.json.

macOS should later use platform-native Cmd conventions where appropriate.

## Menu system

Initial classic desktop menu:

- File;
- Edit;
- View;
- Go;
- Tools;
- Extensions;
- Help.

## Activity Bar / Sidebar

Left Activity Bar / Sidebar:

- Explorer;
- Search;
- Recent;
- Extensions;
- Settings.

Later icons appear only through installed/enabled extensions/connectors:

- Git;
- GitHub;
- Ideboard.

## Explorer / folder tree

Explorer first version:

- opened folder/project;
- files and folders;
- create file;
- create folder;
- rename;
- delete with confirmation;
- reveal in file manager;
- refresh.

Security:

- default scope = only user-opened folder/project.

## Delete behavior

Delete behavior baseline:

- default delete moves item to OS Trash/Recycle Bin;
- permanent delete is a separate command;
- every delete operation requires confirmation;
- folder delete requires extra warning.

Detailed permanent delete UI and OS Trash/Recycle Bin implementation remain open for further discussion.

## Search and Recent

Accepted Activity Bar entries include Search and Recent.

Details still open:

- search in current file;
- search in opened folder/project;
- replace in files;
- ignore patterns;
- hidden files;
- binary file handling;
- recent files;
- recent folders;
- recent projects;
- privacy-safe recent history.

## Source 4 UI baseline

The `4.odt` review confirms the initial UI/workbench baseline.

Accepted UI features:

- tabs;
- dirty tab indicator;
- reopen closed tab;
- vertical split editor;
- minimap default ON;
- Status Bar;
- Command Palette;
- configurable keyboard shortcuts;
- classic menu;
- Left Activity Bar / Sidebar;
- Explorer;
- Search;
- Recent;
- Extensions;
- Settings.

Accepted Explorer behavior:

- opened folder/project;
- files and folders;
- create file;
- create folder;
- rename;
- delete with confirmation;
- reveal in file manager;
- refresh;
- scope limited to user-opened folder/project.

Accepted delete baseline:

- Delete moves to OS Trash/Recycle Bin by default.
- Permanent Delete is a separate command.
- Every delete requires confirmation.
- Folder delete requires extra warning.

## Hidden files / dotfiles UI baseline

Accepted UI behavior:

- Explorer hides hidden files and dotfiles by default.
- Explorer provides a Show Hidden Files toggle.
- `.operre/` and `.git/` become visible only when hidden files are shown.
- `.operre/` and `.git/` must display protected metadata indicators when visible.
- Sensitive dotfiles such as `.env` should display warnings before open/preview where practical.
- Protected metadata paths should not look like normal user folders.
