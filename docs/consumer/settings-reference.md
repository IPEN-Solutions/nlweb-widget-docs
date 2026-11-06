# Settings reference

Settings use Pydantic v2 with the `NLWEB_` environment prefix. The application working directory `.env` is supported for local development. Defaults below describe the approved Widget 0.9.12 runtime.

## Core

| Setting | Default | Effect |
|---|---|---|
| `NLWEB_ENABLED` | `false` | enables the widget's domain-data projection/retrieval behavior |
| `NLWEB_PREFIX` | `/nlweb` | configured widget prefix |
| `NLWEB_PUBLIC_BASE_URL` | `http://localhost:8000` | public base URL used by integrations |
| `NLWEB_SITE` | `default` | site identifier carried through retrieval/projection |
| `NLWEB_RETRIEVAL_STORE` | `memory` | selects `memory`, `haystack`, `haystack-memory`, `pgvector`, `neo4j`, `qdrant`, `qdrant_edge`, `sqlite` or `custom` |

`NLWEB_ENABLED=false` is a startup projection safeguard, not an authentication or administrative lifecycle system.

## Content synchronization

| Setting | Default | Effect |
|---|---|---|
| `NLWEB_CONTENT_SYNC_ENABLED` | `true` | enables source-registry synchronization |
| `NLWEB_CONTENT_SOURCES_FILE` | `./nlweb-sources.json` | source registry path |
| `NLWEB_CONTENT_SYNC_STATE_FILE` | `.nlweb-sync-state.json` | incremental synchronization state |
| `NLWEB_CONTENT_SYNC_INTERVAL_SECONDS` | `900` | recurring synchronization interval; `0` disables periodic waiting |
| `NLWEB_CONTENT_SYNC_ON_STARTUP` | `false` | performs synchronization during startup; requires synchronization to be enabled |

## PostgreSQL + pgvector

`NLWEB_POSTGRES_DATABASE_URL`, `NLWEB_PGVECTOR_DIMENSIONS` (default `384`), `NLWEB_PGVECTOR_TABLE` (default `nlweb_documents`) and `NLWEB_POSTGRES_AUTO_INITIALIZE` (default `true`) control the provider. The database URL is required when `NLWEB_RETRIEVAL_STORE=pgvector`.

## Qdrant Server/Cloud

`NLWEB_QDRANT_URL`, `NLWEB_QDRANT_API_KEY`, `NLWEB_QDRANT_COLLECTION` (default `nlweb_documents`), `NLWEB_QDRANT_DIMENSIONS` (default `384`) and `NLWEB_QDRANT_AUTO_INITIALIZE` (default `true`) control the provider. The URL is required when the provider is selected.

## Qdrant Edge

`NLWEB_QDRANT_EDGE_PATH` (default `./.nlweb-qdrant-edge`) selects the local shard directory and `NLWEB_QDRANT_EDGE_DIMENSIONS` (default `384`) selects vector dimensions. No Qdrant server is required.

## SQLite + sqlite-vec

`NLWEB_SQLITE_PATH` defaults to `./.nlweb-sqlite/nlweb.db`; `NLWEB_SQLITE_DIMENSIONS` defaults to `384`. Install the `sqlite` extra first. Widget 0.9.12 pins `sqlite-vec==0.1.8`.

## Neo4j

`NLWEB_NEO4J_URI`, `NLWEB_NEO4J_USERNAME` and `NLWEB_NEO4J_PASSWORD` are required for the provider. `NLWEB_NEO4J_DATABASE` defaults to `neo4j`; `NLWEB_NEO4J_VECTOR_INDEX` defaults to `nlweb_document_embedding`; `NLWEB_NEO4J_VECTOR_DIMENSIONS` defaults to `384`; `NLWEB_NEO4J_AUTO_INITIALIZE` defaults to `true`.

## Embeddings

`NLWEB_EMBEDDING_MODEL` defaults to `sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`; `NLWEB_EMBEDDING_QUERY_PREFIX` and `NLWEB_EMBEDDING_DOCUMENT_PREFIX` default to unset; `NLWEB_EMBEDDING_DEVICE` defaults to `cpu`. Install the `embeddings` extra when using the bundled Sentence Transformers implementation.

## Configuration rules

Provider dependencies are validated together. A selected provider without required connection/path settings fails fast. Optional providers not selected remain outside the runtime dependency path. Consumers should keep vector dimensions aligned between their embedding model and selected store.
