# Providers and stores

`nlweb-widget` uses a composable provider boundary: the core owns the NLWeb contract, domain projection, orchestration and retrieval interface; optional/external engines implement retrieval behind that interface. The application database remains authoritative. A retrieval store is an AI-facing derived projection unless the consumer deliberately designs a different source-of-truth architecture.

## Built-in core

- **Memory** — dependency-free retrieval for development, tests and lightweight deployments.
- **Custom** — application-supplied retrieval implementation through the widget retrieval contract.
- **Content synchronization** — source-registry driven projection into `ContentDocument`; this is separate from the retrieval engine.

## Optional retrieval providers

| Provider | Extra | Operational model | Typical use |
|---|---|---|---|
| Haystack InMemory | `haystack` | process-local | semantic experiments and small deployments |
| PostgreSQL + pgvector | `postgres` | external database | durable relational/vector deployments |
| Neo4j | `neo4j` | external graph database | relationship-rich and graph/vector domains |
| Qdrant Server/Cloud | `qdrant` | external Qdrant service | durable vector search |
| Qdrant Edge | `qdrant-edge` | embedded local shard | local/offline vector search without a server |
| SQLite + sqlite-vec | `sqlite` | local database file | lightweight hybrid lexical/vector retrieval |

Optional extras are isolated from the core runtime. Install only the capability required by the deployment.

## Qdrant Server/Cloud vs Qdrant Edge

Qdrant Server/Cloud uses the official Qdrant client and requires `NLWEB_QDRANT_URL`; Qdrant Edge embeds a local shard and requires a filesystem path instead. They are separate provider contracts and must not share lifecycle or state merely because both use Qdrant technology.

## SQLite + sqlite-vec

The SQLite provider combines SQLite FTS5 keyword retrieval with `sqlite-vec` vector KNN and reciprocal-rank fusion. The package declares `sqlite-vec==0.1.8` through the `sqlite` extra. This pin is deliberate because the extension is pre-v1; consumers should treat upgrades as compatibility changes and validate them before promotion.

## Embeddings

Embedding generation is an injection boundary. The widget can use its optional Sentence Transformers adapter, but applications may inject another provider. Model choice, dimensions, device, query/document prefixes, cost and credentials therefore remain under application control.

The default local model is `sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`. E5-family models receive `query:` and `passage:` prefixes automatically when the corresponding settings are not explicitly overridden.

## Document ingestion

The optional document adapter normalizes unstructured sources into `ContentDocument`; parser-specific objects do not cross the public widget boundary. The current candidate declares the `docling` optional extra. If a future dependency distribution changes to `docling-slim`, that is a dependency-manifest mutation and must not be represented as a documentation-only change.

## Testing contract

Provider integration tests are conditional: an unconfigured optional provider is skipped; an explicitly configured provider must initialize the real backend, exercise operational behavior, and fail when the configured service is unavailable or misconfigured. Test state is isolated from production/example state, and vector dimensions remain configuration-driven.
