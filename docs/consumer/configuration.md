# Configuration

`nlweb-widget` uses Pydantic v2 settings with the `NLWEB_` environment prefix. Configuration is external to code; a `.env` file in the application working directory is supported for local development.

## Startup safeguard

`NLWEB_ENABLED` defaults to `false`. This is deliberately a **domain-startup data projection safeguard**: a fresh integration must not accidentally ingest, project, or retrieve authoritative domain data before the operator enables the widget.

It is not an administrative visibility-control system. The protocol routes can remain mounted while the widget reports its widget-owned operational state through `effective_state()`. When disabled, `/ask` and the MCP `ask` binding return the normal response envelope with no retrieval results and an operational-state marker.

Administrative suspension, scheduled disablement, hibernation, expiration, resume, and authorization are future-extension concerns and are not exposed through `/ask` parameters or MCP overrides.

## Conditional validation

Provider and lifecycle settings are validated together:

- `pgvector` requires `NLWEB_POSTGRES_DATABASE_URL`.
- `neo4j` requires URI, username, and password settings.
- startup synchronization requires content synchronization to be enabled.
- content synchronization requires a source-registry path.
- `custom` retrieval requires an application-supplied retrieval store.

The intent is fail-fast configuration rather than a partially initialized service.

## Twelve-Factor alignment

Configuration belongs in the environment, dependencies are explicit, backing services are attached resources, and processes should remain restart-safe and disposable where applicable. Logs are emitted as process output rather than treated as application state.


## Optional SQLite + sqlite-vec

For the SQLite provider, install the optional package extra rather than adding the extension ad hoc:

```powershell
uv add "nlweb-widget[sqlite]"
```

The provider reads `NLWEB_SQLITE_PATH` and `NLWEB_SQLITE_DIMENSIONS`. Keep dimensions aligned with the injected embedding provider and configured index.
