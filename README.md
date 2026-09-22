# Gaslight Games — shared game source

Canonical home for the game content both the Gaslight backend and the
GaslightCodeRunner consume:

- `meyer/` — the Meyer game (state machine, strategy API, types, scoring).
- `strategies/` — demo strategies, the user-facing `exampleStrategy` starter,
  and `security/` attack fixtures used by the runner's security test suite.

This repo is consumed as a **git submodule** by both projects:

- `GaslightCodeRunner/sourceFiles/games/` ← this repo (runner side: fixtures
  for its test suite; production never loads game content from disk).
- `GaslightBackend/development/games/` ← this repo (backend side: the dev
  database seed reads the game files from here).

The runner additionally keeps its *runner infrastructure* (`gameRunners/`,
`gameGuard.ts`, `errors.ts`, `commonTypes.d.ts`, security bootstrap) inside
its own `sourceFiles/` — those are runner-internal, shipped with the runner,
and not part of this repo.

## Ownership

- The runner's test suite (`gameGuard.unit.test.ts`, security and theft tests,
  scoring/tournament suites) validates these files against the real bundling +
  VM pipeline. Changes to game behavior should be made here and verified by
  running that suite.

## Sync after changing this repo

```bash
# in each consumer repo
git submodule update --remote
```
