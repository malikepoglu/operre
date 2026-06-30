# Operre Future Features and Restraints

## Future broad direction

Operre may eventually include or support:

- drawing;
- diagrams;
- project boards;
- TODO lists;
- work plans;
- service plans;
- documentation;
- Git/GitHub workflows;
- AI-assisted workflows;
- CAD.

These must not bloat the first core.

## Diagram ideas

Future diagram capabilities may include:

- free canvas;
- boxes/arrows;
- flowcharts;
- architecture diagrams;
- mind maps;
- entity diagrams;
- sequence diagrams;
- SVG export;
- PNG export;
- JSON document model.

## CAD separation

CAD is future work.

Rule:

- CAD must stay separate from diagrams.
- CAD must not be part of first core.
- Default workspace keeps `Diagrams/` and `Cad/` separate.

## TODO/work plan/service plan extensions

Future extensions may include:

- TODO list;
- work plan;
- service plan;
- project planning;
- project notes;
- decision records;
- risk lists.

These are not first core implementation details.

They should be local-first by default and syncable later through explicit extension-level sync.

## First implementation must not include

First implementation must not include:

- full IDE;
- debugger;
- terminal;
- marketplace;
- AI agent;
- GitHub connector;
- Ideboard connector;
- CAD;
- cloud sync;
- collaboration;
- remote workspace.

## First implementation likely focuses on

First implementation should likely focus on:

- Tauri shell;
- Solid/Vite UI;
- Monaco editor display;
- create/open/save text file;
- basic Markdown editing;
- basic layout;
- status bar skeleton;
- settings foundation;
- no unsafe extension execution.

## Draft implementation shape

Possible future shape:

- apps/desktop/
- packages/editor-core/
- packages/workbench-core/
- packages/ui/
- packages/file-core/
- packages/settings-core/
- packages/security-core/
- packages/extension-api/
- packages/markdown-core/
- packages/logging-core/
- docs/
- extensions/ later

This is not final.

## Restraint rule

Do not create application scaffolding until specification and first implementation TODO are approved.
