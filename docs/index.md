# NLWeb Widget

`nlweb-widget` is a framework-neutral Python library for exposing authoritative domain information through the NLWeb protocol so compatible AI agents and AI-search clients can query the domain directly.

The package does **not** replace the application's authoritative database. It exposes a protocol-facing projection over domain-owned data while keeping retrieval/projection concerns separate from the source of truth.

## Production flow

```text
Authoritative application data
        |
        | ingestion / projection
        v
NLWeb Widget core
        |
        +---- /ask
        +---- /mcp
        +---- /.well-known/nlweb (optional package metadata)
        +---- /health (operational)
        |
        v
AI agents / AI-search clients
```

The primary HTTP surface is `POST /ask`. MCP is exposed at `POST /mcp`. The package does not claim `/await` as a normative NLWeb endpoint.

## Reference integrations and visibility suite

The production repository contains the library and its package-level tests. Complete FastAPI, Flask, Django, Starlette and stdlib examples, visibility demonstrations, AskAgent integration, optional UI setup, and example-specific tests/tasks are maintained in the separate `nlweb-widget-examples` repository.

This separation keeps the published widget dependency graph focused on the widget itself and allows the reference suite to use a different Python baseline when external tooling requires it.

## Learn the integrations

For users who want to understand how the integration behaves inside a real application, the separate `nlweb-widget-examples` repository now provides a Zensical-backed reference guide. It explains the mental model, repository boundary, runtime flow, framework-specific examples, visibility testing, optional AskAgent topology, and consumer takeaways.

Use the production docs here to understand the library contract; use the examples documentation to understand how to adapt that contract to an application framework.

## Providers and stores

See [Providers and stores](concepts/providers-and-stores.md) for optional retrieval and storage integrations.

## Architecture and responsibility

The widget is deliberately split into a small protocol-facing core and optional/external capability boundaries. Retrieval engines, embedding implementations, document parsers and framework adapters can be replaced without turning them into the authoritative domain database. This composability is the main durability mechanism of the ecosystem: consumers can scale or replace one capability without redesigning the NLWeb contract.

## Disclaimer

The NLWeb Widget ecosystem packages are designed, developed, tested and release-reviewed with AI coding assistance and human review/local QA. They are intended primarily for education, experimentation and prototyping. They may be used in production only at the consumer's own responsibility, with appropriate security, privacy, operational, dependency and capacity review for the deployment.
