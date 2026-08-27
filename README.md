# @videogpt/catalog

This package is just data, not service. It has no database, HTTP API, queue, or execution code.

[Kinoforge](https://github.com/videogpt-dev/kinoforge) does not import it. Runtime resolve catalog definitions, then call Kinoforge through REST.

## Core alignment

Definition fields mirror portable part of core `instructions` row:

- `type`: `screenwriter`, `agent`, `preset`, or `fragment`
- `subtype`, `key`, `name`, `category`, `body`, and `extras`
- optional `editable` and `visible` metadata

Engine compatibility belongs to catalog release, so one activated release cannot contain mixed
compatibility rules.

Database-only fields are intentionally absent: `id`, `owner_id`, `origin`, `source_id`, and
timestamps. Cloud importer supplies those values when approved public definitions become system
rows.

Agent stages are embedded definitions, not subagent records. Current screenwriter stage shape
matches cloud runner: role, instructions, output format, optional provider/model, temperature,
and optional output-token limit.

## Release flow

1. Contributors change community definitions through pull requests.
2. Validation checks schema, placeholders, unique keys, compatibility, and references.
3. Release build writes checksums and immutable version.
4. Self-host thin runtime downloads, verifies, validates, and atomically activates pinned release.
5. Cloud may import approved release as public baseline. Private professional rows remain in cloud.

`catalog.json` is empty until approved community definitions are exported or authored. Existing
cloud system rows and temporary Kinoforge clip prompts are not public automatically.

Package stays private inside monorepo until catalog license and standalone public repository are
ready.
