# Operre Source Review: 5.odt

This document records decisions and operational evidence extracted from `5.odt`.

Source position:

- file: `5.odt`
- processing order: 5 / 5
- topic range: initial repository creation output, first documentation baseline commit, conversation import area, local-only transcript handling, prompt-safe terminal workflow, source-by-source ODT processing discipline, and post-push audit habit.

## 1. Initial repository documentation baseline

5.odt records the successful initial repository documentation baseline.

Observed successful commit:

- commit: `f04f7c8`
- message: `docs: record Operre initial specification baseline`
- branch: `main`
- remote: `origin/main`
- created files:
  - `.gitignore`
  - `README.md`
  - `TODO.md`
  - `specifications.md`

Operational conclusion:

- initial Operre repository bootstrap was successful;
- GitHub SSH authentication worked;
- local clone path was `/home/mak/operre/repo`;
- empty repository was initialized on `main`;
- push to GitHub succeeded.

## 2. Repository audit evidence

5.odt confirms early repository audit habits:

- tool audit;
- git version audit;
- Git identity audit;
- GitHub SSH authentication audit;
- Operre remote audit;
- LogisticSearch remote audit;
- local repository audit;
- clean worktree check;
- commit and push;
- post-push audit.

Accepted rule:

> Every meaningful Operre repository change should include pre-write audit and post-push audit.

## 3. Conversation import area

5.odt records the local conversation import area preparation.

Accepted local paths:

- Operre root: `/home/mak/operre`
- Operre repo: `/home/mak/operre/repo`
- import area: `/home/mak/operre/conversation_import`
- expected full chat export: `/home/mak/operre/conversation_import/operre_chat_full_export.txt`

Security rule:

- import folder is local-only;
- raw full conversation transcript must not be committed unless explicitly decided later;
- transcript import is for comparison and gap analysis;
- repository documentation should contain decisions, not raw private transcript dumps.

## 4. Import area permissions

Accepted operational rule:

- import directory should be local/private;
- `chmod 700` is appropriate for the import directory.

Reason:

- imported conversation may contain private planning details;
- raw transcript may include sensitive project context;
- raw transcript should not be uploaded to GitHub by default.

## 5. Documentation expansion process

5.odt records the transition from initial documentation baseline to stronger specification consolidation.

Accepted direction:

- first write root README/spec/TODO baseline;
- then expand specifications from full planning transcript;
- then patch specification gaps from uploaded transcript;
- then split accepted decisions into structured docs;
- then process source files one by one.

## 6. Source-by-source processing discipline

Accepted processing order:

1. `1.odt`
2. `2.odt`
3. `3.odt`
4. `4.odt`
5. `5.odt`

Rule:

- process source files one by one;
- do not skip `1.odt`;
- do not skip `4.odt`;
- each source review gets a dedicated file;
- TODO status must show each source file processed;
- post-push audit must confirm each commit.

## 7. Prompt/code-block reliability lesson

5.odt includes repeated user emphasis that long prose around code blocks can increase risk of copy/paste/rendering mistakes.

Accepted interaction rule:

- terminal blocks must be Linux Bash compatible;
- code blocks must be prompt-safe;
- avoid malformed heredocs;
- avoid hidden truncation;
- avoid unnecessary chatter around terminal code;
- keep code blocks self-contained;
- include `PROMPT_RETURNED=TRUE`;
- include clear failure exits;
- include pre-write and post-push checks.

## 8. UI/rendering error lesson

A later UI-side error was observed:

- `Cannot use 'in' operator to search for 'type' in epad.`

Operational interpretation:

- this was not a Bash/Git error;
- it was a ChatGPT UI/rendering-side issue;
- terminal repo operations still completed successfully when post-push audit showed success.

Accepted rule:

- do not trust UI rendering alone;
- trust terminal output, git status, commit hash, and remote ref audit;
- if a UI error appears, verify repo state with terminal audit.

## 9. 5.odt accepted decisions summary

Accepted decisions extracted from `5.odt`:

- Initial repository documentation baseline succeeded.
- Operre repo path is `/home/mak/operre/repo`.
- GitHub SSH workflow works.
- Post-push audit is mandatory.
- Conversation import area is local-only.
- Raw full transcript must not be committed by default.
- Documentation should preserve decisions, not raw chat dumps.
- Source files must be processed in order from 1.odt to 5.odt.
- Each ODT source review must be committed and pushed separately or clearly audited.
- Terminal code blocks must be Bash-compatible and prompt-safe.
- UI rendering errors do not replace terminal/git verification.
- After all five source files are processed, continue product decisions after delete behavior.
