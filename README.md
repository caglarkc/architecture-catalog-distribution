# Architecture Catalog — public distribution

Version **0.1.0**, MIT. This repository distributes the catalog index and seven
independent architecture starter ZIPs. The development source repository
`caglarkc/architecture-catalog` remains private.

**Untested initial release:** build, types, schemas, manifests and packaging
were checked. Platforms, generator/CLI/library usage, dependency installation,
Docker, starter applications and real providers are `not_run`. No platform
support or working-example guarantee is claimed.

## npm publication status

The package `@caglarkc/architecture-catalog@0.1.0` is prepared. **npm publication
is pending the owner's login and scope authorization.** Installing it from npm
is available only after that step. This repository's release assets can be
inspected independently of npm publication.

## Intended usage once npm is published

Node.js 24 is required for the library and `archcat` CLI.

```sh
npm install -g @caglarkc/architecture-catalog@0.1.0
archcat list
archcat search --language python --type agent
archcat info python-langgraph-agent-api
archcat plan my-agent --template python-langgraph-agent-api --preset mock
archcat create my-agent --template python-langgraph-agent-api --preset mock
```

Or use `npx @caglarkc/architecture-catalog@0.1.0 create ...`. `create` defaults to
files only. `archcat install my-agent` and `archcat run my-agent` are explicit
optional stages. A new project can opt into both with `--install --run`.
Only the selected ZIP is fetched, checked by SHA-256 and cached.

Python starters need Python 3.12 and uv >=0.13.0 for installation/execution.
Node starters need Node.js 24/npm >=11. The Compose preset needs Docker and
Compose v2 for those stages. Scaffolding itself does not need Python or Docker.
OpenAI mode reads `OPENAI_API_KEY` only from the user's runtime environment;
mock mode has no provider dependency. Environment examples are not loaded
automatically. Do not commit credentials.

## Release contents

[Versioned release v0.1.0](https://github.com/caglarkc/architecture-catalog-distribution/releases/tag/v0.1.0)
contains `catalog.json`, `sha256sums.txt`, validation reports and:

| Template | Presets |
| --- | --- |
| `python-fastapi-api` | `minimal` |
| `typescript-nestjs-api` | `minimal` |
| `python-langgraph-agent-api` | `mock`, `openai` |
| `python-typer-cli` | `minimal` |
| `react-fastapi-fullstack` | `local` |
| `python-fastapi-microservices` | `compose` |

The index contains component roles/technologies, parameters, requirements by
phase, install/run commands, file interpolation declarations, artifact size
and SHA-256. Language/framework/role filters match the same component.
Schema version 1 is published in `catalog.schema.json`.

Generated projects are editable, with README, MIT license, pinned manifests,
resolved lockfiles and a first development point. They contain separate
`.archcat/plan.json` and `.archcat/result.json`; no provider keys are persisted.
Only new/empty targets are allowed. Traversal, symlinks and file collisions are
rejected. Template generator scripts do not execute during creation.

The microservice preset has a Traefik file-provider gateway and two FastAPI
services with internal HTTP, JSON logs and propagated request IDs. Container
log collection is included; a persistent searchable log store is not.

## Immutable artifacts and future validation

Published asset bytes are not overwritten. Changes ship as a new version.
The next validation stage on another computer covers npm local/global/npx and
imports, all seven preset generations, cache/offline, bad hashes/targets,
installation, first examples, Docker, platform behavior and real provider calls.
Validation claims will include their actual environment and scope.

The tool and original templates use MIT; dependencies retain upstream licenses.
Questions and issues may be filed in this public repository.
