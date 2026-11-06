# Retrieval stores and extras

## PostgreSQL + pgvector

The PostgreSQL option is the preferred ready-to-use production-oriented path when the consumer already operates PostgreSQL. Benefits include operational maturity, transactional tooling and keeping vector data beside relational projection metadata. Costs include PostgreSQL operations and vector-extension management.

## Neo4j

Neo4j is optional when relationships and graph traversal are first-class requirements. It is useful for relationship-rich domains but introduces a separate graph operational dependency.

## SQLite + sqlite-vec

SQLite + sqlite-vec is the lightweight local hybrid option. Install the widget with the `sqlite` extra:

```powershell
uv add "nlweb-widget[sqlite]"
```

Then configure the provider explicitly, for example:

```text
NLWEB_RETRIEVAL_STORE=sqlite
NLWEB_SQLITE_PATH=./.nlweb-sqlite/nlweb.db
NLWEB_SQLITE_DIMENSIONS=384
```

Widget 0.9.12 pins `sqlite-vec==0.1.8` because the upstream extension remains pre-v1.

## Custom stores

The core only requires the retrieval contract. Consumers can provide their own vector, lexical, graph or hybrid implementation.

No store becomes the domain source of truth merely because the widget indexes it.

## Provider configuration and tests

Provider integrations are optional. PostgreSQL + pgvector requires its configured database URL; Neo4j requires its configured URI and credentials. Provider tests intentionally skip when a provider is unconfigured and fail when it is configured but unavailable. This keeps the default test suite dependency-light without hiding a broken configured service.
