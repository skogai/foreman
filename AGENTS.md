# PROJECT KNOWLEDGE BASE

## OVERVIEW

Foreman plugin: roadmap-backed task selection, prompt crafting, survey updates, and decision-log workflows.

## STRUCTURE

```text
foreman/
├── hooks/       # session/task/post-commit lifecycle hooks
├── scripts/     # roadmap CLI and prompt/decision helpers
├── skills/      # user-facing slash-command workflows
├── tests/       # node:test suites, temp git/roadmap fixtures
└── benchmarks/  # prompt/task quality fixtures
```

## WHERE TO LOOK

| Task | Location | Notes |
|---|---|---|
| Roadmap engine | [scripts/roadmap.js](scripts/roadmap.js) | CRUD, dependencies, candidate ranking, duplicate check. |
| Hook wiring | [hooks/hooks.json](hooks/hooks.json) | Session start, task create/complete, roadmap guard, post-commit. |
| Main coverage | [tests/roadmap.test.js](tests/roadmap.test.js) | Large matrix for roadmap behavior. |
| Test helpers | [tests/helpers.js](tests/helpers.js) | Temp repos and roadmap fixtures. |
| Prompt contract | [prompt-template.md](prompt-template.md) | Keep section order/semantics stable. |
| Decision docs | [decision-doc-template.md](decision-doc-template.md) | Supersede instead of rewriting history. |

## CODE MAP

| Symbol | Location | Role |
|---|---|---|
| `cmdAdd` | [scripts/roadmap.js](scripts/roadmap.js) | Create structured roadmap entries. |
| `cmdUpdateStatus` | [scripts/roadmap.js](scripts/roadmap.js) | Status/touch/commit update flow. |
| `cmdNextCandidates` | [scripts/roadmap.js](scripts/roadmap.js) | Dependency-aware next-task selection. |
| `cmdCheckDuplicate` | [scripts/roadmap.js](scripts/roadmap.js) | Similarity guard for new entries. |

## CONVENTIONS

- Use the CLI scripts; do not read/edit `ROADMAP.jsonl` by hand.
- Skill flows should not paste raw JSON to chat unless explicitly required.
- Pick/roadmap flows should not investigate the codebase while selecting candidates.
- Tests are direct `node --test tests/*.test.js` CommonJS suites.

## ANTI-PATTERNS

- Do not mark tasks `in_progress` yourself in the roadmap pick flow.
- Do not invent candidates outside roadmap output.
- Do not mutate decision-log behavior silently.
- Do not edit decision docs backward; create a new doc with `supersedes`.

## COMMANDS

```bash
node --test tests/*.test.js
node scripts/roadmap.js --help
```
