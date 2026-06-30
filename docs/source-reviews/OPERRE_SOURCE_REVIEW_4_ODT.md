# Operre Source Review: 4.odt

This document records decisions and useful planning extracted from `4.odt`.

Source position:

- file: `4.odt`
- processing order: 4 / 5
- topic range: tabs, split editor, Markdown behavior, Markdown preview security, minimap, status bar, command palette, keyboard shortcuts, menu system, Activity Bar/Sidebar, Ideboard separation, Explorer/folder tree, delete behavior, initial repository documentation write.

## 1. Tab system

Accepted tab behavior:

- multiple tabs supported;
- dirty tab indicator: `*`;
- close tab button;
- reopen closed tab;
- pin tab later;
- tab restore through session restore.

## 2. Split editor

Accepted split editor behavior:

- first version supports side-by-side vertical split;
- horizontal split comes later;
- session restore remembers split layout.

## 3. Markdown behavior

Accepted Markdown behavior:

- users can create `.md` files;
- `.md` opens in edit mode by default;
- preview only mode is available;
- side-by-side edit + preview is available;
- live preview toggle is available.

Markdown files created by users belong to users.

Markdown parser/renderer dependencies must be license-audited before implementation.

Rules:

- prefer permissive dependencies;
- preserve required license notices;
- add third-party notices later;
- verify official dependency license sources before implementation.

## 4. Markdown preview security

Accepted Markdown preview security:

- raw HTML disabled or sanitized;
- scripts always blocked;
- remote images/resources blocked by default;
- local images allowed only from current workspace;
- blocked/downgraded content shows warning.

Warning UI:

- web-browser-like yellow top warning bar;
- clear message;
- not hidden as a tiny popup;
- user sees what was blocked.

Example warning:

- Remote resources were blocked for your safety.
- Allow for this file.
- Allow for this workspace.
- Settings.

## 5. Minimap

Accepted minimap behavior:

- default ON;
- right side by default;
- user can disable in settings;
- left/right setting;
- width small/medium/large;
- adaptive tablet/phone/small-screen behavior.

## 6. Status Bar

Accepted Status Bar:

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

## 7. Command Palette

Accepted Command Palette:

- VS Code-like quick command UI;
- shortcut: Ctrl+Shift+P.

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

## 8. Keyboard shortcuts

Keyboard shortcuts must be configurable.

Default shortcuts:

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

## 9. Menu system

Accepted classic desktop menu:

- File;
- Edit;
- View;
- Go;
- Tools;
- Extensions;
- Help.

## 10. Activity Bar / Sidebar

Accepted Left Activity Bar / Sidebar:

- Explorer;
- Search;
- Recent;
- Extensions;
- Settings.

Later icons appear only through installed/enabled extensions/connectors:

- Git;
- GitHub;
- Ideboard.

## 11. Ideboard separation

Accepted Ideboard status:

- separate application;
- separate project;
- meeting and collaboration environment later;
- not Operre core;
- optional Connector Extension later.

## 12. Explorer / folder tree

Accepted Explorer first version:

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

## 13. Delete behavior

Accepted delete behavior baseline:

- default Delete moves item to OS Trash/Recycle Bin;
- Permanent Delete is a separate command;
- every delete operation requires confirmation;
- folder delete requires extra warning.

Remaining details:

- exact permanent delete UI;
- exact OS Trash/Recycle Bin implementation;
- platform-specific behavior;
- undo/restore possibilities;
- permission and audit behavior.

## 14. Initial repository documentation request

4.odt also includes the first major request to write the accumulated planning into the Operre GitHub repository.

Accepted repository memory direction:

- root README.md contains general project information;
- specifications.md contains the full detailed specification;
- TODO.md is planning/TODO memory;
- implementation TODO expands later after specification stabilizes;
- repository documents are English-only;
- chat/user communication remains Turkish;
- terminal workflow follows LogisticSearch-like discipline.

## 15. 4.odt accepted decisions summary

Accepted decisions extracted from `4.odt`:

- tab system accepted;
- vertical split editor accepted;
- Markdown edit/preview behavior accepted;
- Markdown preview security accepted;
- yellow browser-like Markdown warning bar accepted;
- minimap accepted and default ON;
- Status Bar accepted;
- Command Palette accepted;
- configurable keyboard shortcuts accepted;
- classic menu accepted;
- Activity Bar/Sidebar accepted;
- Ideboard remains separate and later optional Connector Extension;
- Explorer/folder tree first version accepted;
- delete behavior baseline accepted;
- initial GitHub documentation/memory direction accepted.
