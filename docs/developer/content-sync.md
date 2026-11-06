# Content-source synchronization

The widget can load a JSON source registry and project authoritative domain data through `ContentSyncService`.

A registry can be either a JSON list or an object containing a `sources` list. Local source locations are resolved relative to the registry file, which makes example and deployment configurations portable.

The projection path is:

`authoritative source → ContentSource → adapter → ContentDocument → retrieval provider → /ask or MCP`

The authoritative source remains distinct from the AI-facing retrieval projection. PostgreSQL/pgvector and Neo4j remain optional provider implementations; the embedding provider is injected rather than bundled into the production package.


## PDF ingestion safety on local hosts

The widget's optional Docling adapter preserves its normal behavior by default. For constrained local or Windows QA environments, set `DOCLING_SAFE_PDF=true` together with `DOCLING_DEVICE=cpu` and a small `DOCLING_NUM_THREADS` value. Safe mode uses backend PDF text extraction without OCR or table-structure inference; leaving `DOCLING_SAFE_PDF=false` retains the richer default Docling pipeline.
