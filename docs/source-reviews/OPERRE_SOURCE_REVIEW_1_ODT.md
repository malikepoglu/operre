# Operre Source Review: 1.odt

This document records decisions and useful research extracted from `1.odt`.

Source position:

- file: `1.odt`
- processing order: 1 / 5
- topic range: VS Code, Cursor, Monaco Editor, Monaco licensing, early editor/workspace direction, early Ideboard relationship ideas.

## 1. VS Code architecture reference

VS Code is an important reference for Operre, but Operre must not become a VS Code clone.

Useful VS Code architecture notes:

- VS Code desktop is based on Electron.
- Electron includes Chromium and Node.js.
- VS Code UI is largely rendered with web technologies.
- VS Code workbench is not React/Angular/Vue as a normal app framework choice; it uses a custom TypeScript workbench architecture.
- Monaco Editor is the code editor area inside VS Code.
- Monaco is not the whole VS Code product.
- VS Code includes much more than Monaco:
  - Explorer;
  - Activity Bar;
  - Side Bar;
  - Editor Groups;
  - Terminal;
  - Problems/Output/Debug panels;
  - Status Bar;
  - Extension Host;
  - Debug system;
  - Source Control UI;
  - Remote/SSH/Container infrastructure.

Accepted Operre lesson:

- Operre can use Monaco as editor engine.
- Operre must build its own workbench around Monaco.
- Operre must not assume Monaco provides VS Code's workbench, extension system, Git UI, settings UI, or security model.

## 2. VS Code extension architecture reference

Useful VS Code ideas:

- extension manifest;
- extension host separation;
- language server pattern;
- language client / language server separation;
- activation by language or command;
- UI contribution points;
- webviews;
- workspace trust;
- secret storage.

Important Operre decision:

- Operre should be VS Code-like in usability but stricter in permissions.
- VS Code extensions have broad power through the extension host.
- Operre must use explicit permissions and default-deny behavior.

Accepted rule:

> Operre should learn from VS Code extensibility, but use a stricter privacy-first and permission-scoped model.

## 3. Cursor architecture reference

Cursor is useful as an AI-first reference, but not as Operre's product model.

Cursor is understood as:

- VS Code / Code-OSS fork lineage;
- Electron/Chromium desktop lineage;
- Monaco / VS Code editor-core lineage;
- VS Code extension compatibility direction;
- custom proprietary AI layer;
- AI Chat / Composer;
- inline edits;
- tab completion;
- codebase indexing;
- local/cloud agent workflows;
- Cursor backend involvement in AI request flow.

Accepted Operre lesson:

- Cursor's main difference is not the editor engine; it is the AI/agent layer.
- Operre must not copy cloud-first AI assumptions.
- Operre AI must be optional, permission-scoped, auditable, and diff-before-apply.

## 4. AI privacy lesson from Cursor

Cursor-like AI capabilities create a large privacy/security surface:

- codebase indexing;
- prompt building;
- model routing;
- cloud agents;
- snippets/context sent to backend;
- possible sensitive context exposure.

Accepted Operre rule:

- AI agents are optional Connector Extensions.
- AI cannot read the full workspace by default.
- AI cannot edit files by default.
- AI cannot run commands by default.
- AI cannot push/commit by default.
- AI cannot access secrets by default.
- AI cannot send source code or project data without explicit scoped permission.
- All AI-made edits must be shown as diff before apply.
- Every AI action must be logged.

## 5. Monaco Editor decision

Monaco Editor is accepted as the preferred editor engine candidate.

Useful Monaco capabilities:

- text buffer/model;
- syntax highlighting/tokenization;
- completion/intellisense API surface;
- diagnostics decorations;
- multi-cursor;
- diff editor;
- minimap;
- folding;
- decorations;
- editor worker infrastructure.

Accepted distinction:

> Monaco Editor is not Visual Studio Code.

Monaco provides the editor area. Operre must separately design:

- workbench shell;
- Explorer;
- tabs;
- split editor;
- Status Bar;
- Command Palette;
- settings UI;
- extension runtime;
- permission model;
- Git/GitHub integration;
- AI connector model;
- security sandbox;
- storage model.

## 6. Monaco license planning

Planning assumption from research:

- Monaco Editor is open source.
- Monaco Editor uses a permissive license suitable for commercial/proprietary use when notices are preserved.

Implementation rule:

- verify the official Monaco package license before dependency addition;
- preserve Monaco copyright/license notices;
- audit Monaco wrapper packages separately;
- audit language workers separately where needed;
- do not use VS Code/Microsoft branding;
- do not assume VS Code extension API is included.

## 7. Early product direction from 1.odt

Early direction included a broader editor/workspace idea:

- more controlled than VS Code;
- simpler than a full IDE;
- more privacy-conscious than AI-cloud-first editors;
- capable of Git/GitHub support later;
- connected to Ideboard later but not dependent on it.

Accepted current refined direction:

- Operre is independent.
- Ideboard is separate.
- Operre starts as a lightweight editor/project platform.
- Git/GitHub, Ideboard, diagrams, CAD, and AI come later through extensions/connectors.

## 8. Drawing and diagram early idea

1.odt included early ideas around combining:

- code;
- notes;
- diagrams;
- project board;
- Git/GitHub;
- documentation;
- AI summaries.

Accepted current rule:

- drawing/diagrams remain future direction;
- CAD remains later and separate;
- first core must not become too large;
- diagrams and CAD must be separate categories.

## 9. Restraint rule from 1.odt

Operre must not try to become a huge IDE at the beginning.

First implementation should not include:

- full debugger;
- terminal;
- full extension marketplace;
- cloud collaboration;
- full AI agent;
- GitHub connector;
- Ideboard connector;
- CAD;
- remote containers;
- devcontainers;
- full LSP ecosystem.

First implementation should focus on:

- lightweight app shell;
- Monaco editor;
- `.txt` editing;
- Markdown editing;
- basic file open/save;
- simple workbench;
- safe local storage;
- future extension foundation.

## 10. Decisions extracted from 1.odt

Accepted decisions:

- Use Monaco Editor as preferred editor engine.
- Treat VS Code as architecture reference, not clone target.
- Treat Cursor as AI reference, not product model.
- Keep Operre smaller than VS Code.
- Keep Operre less cloud-centered than Cursor.
- Keep AI optional and permission-scoped.
- Preserve license notices for Monaco and any dependencies.
- Audit all wrappers/dependencies separately.
- Do not use VS Code or Microsoft branding.
- Keep Ideboard separate.
- Keep GitHub optional.
- Keep diagrams/CAD as future features.
- Build a controlled, privacy-first project workspace over time.
