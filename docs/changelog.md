# Changelog

This changelog records user- and developer-visible changes between approved releases. Development candidates and local-QA iterations are omitted.

## 0.9.12

### Added

- Protocol projection and HTTP `/ask` Server-Sent Events behavior for requests that set `prefer.streaming` to true.
- SSE event sequence documentation: `start`, indexed `result`, optional `error`, and `complete`.

### Changed

- Clarified that `/mcp` remains a JSON-RPC binding and is not converted into an SSE response by the HTTP `/ask` streaming preference.
- Published a frozen documentation bundle aligned with the approved Widget 0.9.12 runtime.

## 0.9.11

### Added

- Optional retrieval/store documentation for PostgreSQL + pgvector, Neo4j, Haystack, Qdrant Server/Cloud, Qdrant Edge, and SQLite + sqlite-vec.
- Provider capability and settings-reference coverage, including optional installation boundaries and configuration effects.

### Changed

- Expanded consumer, developer, production, content-synchronization, and Windows guidance.
- Added release, contributor, and responsibility guidance for the published package.

## 0.9.10

### Changed

- `NLWEB_ENABLED` defaults to `false` as a startup domain-data projection safeguard.
- Added validated provider/content-synchronization configuration and widget startup orchestration.
- Documented the boundary between current operational state and the future administrative lifecycle extension.

## Published revision policy

Each published revision receives a section, ordered newest first. Multiple internal development iterations are consolidated into the next approved release. Candidate names, local-QA labels, and recovery-only revisions are not part of this public history.
