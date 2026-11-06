# Architecture

The core contains protocol models, orchestration, ingestion contracts, retrieval abstractions and projection logic. Framework adapters only translate their framework's routing/request/response conventions into the core contract.

## Data authority

The application database remains authoritative. PostgreSQL/pgvector, Neo4j, Chroma or another retrieval backend is a derived AI-search projection unless the consumer explicitly designs a different architecture.

This separation permits consumers to refresh or rebuild AI-search indexes without changing customer-facing domain records.

## Extensibility

Consumers implement the retrieval protocol or register future providers rather than modifying the core. Framework integrations are intentionally named `*_integration.py` so they cannot be confused with framework modules.

## Storage boundary

Ingestion and provider capabilities are implemented behind package-owned contracts. PostgreSQL + pgvector and Neo4j are optional derived stores; they do not replace the authoritative application data source. The widget core does not depend on NLWeb reference-implementation internals.
