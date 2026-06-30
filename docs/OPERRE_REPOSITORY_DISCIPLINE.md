# Operre Repository Discipline

## Repository as project memory

The GitHub repository is the project memory.

Every meaningful detail must be written into the repository.

This includes:

- product decisions;
- rejected decisions;
- architecture decisions;
- security rules;
- UX behavior;
- storage paths;
- extension rules;
- implementation details;
- TODO changes;
- completed work;
- post-push audit state.

## Language rule

Repository documentation must be English-only.

Chat discussion may be Turkish, but GitHub documentation must be English.

## Current phase

Current phase is specification consolidation.

Implementation must not start until:

1. specifications are stable enough;
2. core scope is frozen for the first milestone;
3. repository discipline is accepted;
4. first implementation TODO queue is generated.

## TODO-driven workflow

After specification consolidation, every task must follow:

1. Select one TODO item.
2. Audit current state.
3. Implement or document.
4. Verify.
5. Update documentation.
6. Update TODO.
7. Review git diff.
8. Commit.
9. Push.
10. Post-push audit.

## Terminal/audit style

Operre should follow the disciplined terminal workflow used for LogisticSearch:

- named Bash code blocks;
- explicit full paths;
- read-only audit before write blocks;
- fail fast on dirty worktrees;
- no detached HEAD work;
- no hidden state changes;
- post-push audit;
- no silent assumptions.

## Initial repository model

Current local path:

- `/home/mak/operre/repo`

Remote:

- `git@github.com:malikepoglu/operre.git`

Initial branch:

- `main`

## Package manager discipline

Operre uses pnpm only.

Allowed after implementation begins:

- `pnpm-lock.yaml`;
- `pnpm-workspace.yaml`;
- `packageManager` field in `package.json`.

Forbidden:

- `package-lock.json`;
- `yarn.lock`;
- `bun.lockb`.

Future CI install rule:

- `pnpm install --frozen-lockfile`

## Secrets rule

Never commit:

- `.env`;
- tokens;
- API keys;
- private SSH keys;
- credentials;
- runtime secrets;
- local logs;
- AI prompt/response logs;
- local caches.

## Git history rule

Default rule:

- no force push;
- no history rewrite;
- no mixed project files between Operre and LogisticSearch.

## Source 4 repository memory baseline

The `4.odt` review confirms the first major GitHub memory direction.

Accepted repository writing model:

- root README.md contains general project information;
- specifications.md contains detailed project specification;
- TODO.md tracks planning and later work queue;
- implementation TODO comes after specification stabilization;
- repository docs are English-only;
- terminal workflow follows LogisticSearch-like audit/write/commit/push discipline.

## Source 5 import and verification baseline

The `5.odt` review confirms repository execution and source import discipline.

Accepted operational rules:

- Initial repository baseline must be verified by commit hash and remote ref.
- Conversation import area is local-only.
- Raw full transcript must not be committed by default.
- Source files are processed one by one in order.
- Each source review updates TODO and documentation.
- Post-push audit confirms remote state.
- UI rendering errors must not be confused with terminal/git failures.
