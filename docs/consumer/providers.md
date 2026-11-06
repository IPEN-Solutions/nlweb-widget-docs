# Providers, embeddings and optional capabilities

The widget is intentionally composable. Core protocol and projection behavior does not require a specific database, vector engine, embedding vendor, framework, or live LLM. Optional integrations are installed and configured independently.

## Capability matrix

| Capability | Installation | Main effect |
|---|---|---|
| Memory retrieval | core | dependency-free local retrieval |
| Haystack semantic memory | `nlweb-widget[haystack]` | Haystack `InMemoryDocumentStore` semantic retrieval |
| PostgreSQL + pgvector | `nlweb-widget[postgres]` | durable relational/vector retrieval |
| Neo4j | `nlweb-widget[neo4j]` | graph + vector retrieval |
| Qdrant Server/Cloud | `nlweb-widget[qdrant]` | external vector retrieval |
| Qdrant Edge | `nlweb-widget[qdrant-edge]` | embedded/local vector retrieval |
| SQLite + sqlite-vec | `nlweb-widget[sqlite]` | local FTS5 + vector hybrid retrieval |
| Sentence Transformers | `nlweb-widget[embeddings]` | local configurable embeddings |
| Haystack + Sentence Transformers | `nlweb-widget[semantic]` | combined semantic retrieval/embedding stack |
| Document ingestion | `nlweb-widget[documents]` | normalize supported unstructured sources |
| Framework adapters | matching extra | mount the framework-neutral widget in that framework |

The optional integrations are independently replaceable. Installing an integration does not silently select it as the retrieval backend.

## Installation examples

```powershell
uv add "nlweb-widget[postgres]"
uv add "nlweb-widget[neo4j]"
uv add "nlweb-widget[qdrant]"
uv add "nlweb-widget[qdrant-edge]"
uv add "nlweb-widget[sqlite]"
uv add "nlweb-widget[embeddings]"
uv add "nlweb-widget[documents]"
```

Widget 0.9.12 pins `sqlite-vec==0.1.8` because that dependency is pre-v1. Optional provider versions should be treated conservatively and upgraded only after provider-specific QA.

## Embedding settings

`NLWEB_EMBEDDING_MODEL` selects the local Sentence Transformers model, `NLWEB_EMBEDDING_DEVICE` selects its device, and the query/document prefix settings control models such as E5. Applications can inject a completely different embedding implementation instead.

The benchmark module reports Recall@1/3/5, mean query latency and vector dimensions so a consumer can compare multilingual models before selecting a deployment stack. Benchmark output is evidence for a decision, not an automatic runtime policy.

## Document adapter settings

The optional document adapter reads `DOCLING_DEVICE`, `DOCLING_NUM_THREADS` (falling back to `OMP_NUM_THREADS`) and `DOCLING_SAFE_PDF`. Safe PDF mode is intended for constrained local/Windows environments: it uses backend PDF text extraction without OCR/table-structure inference. The default remains the richer normal adapter path.

**Dependency naming note:** Widget 0.9.12's `pyproject.toml` declares the `docling` distribution. Do not substitute `docling-slim` in deployment instructions until that dependency is deliberately changed and revalidated.
