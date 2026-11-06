# Protocol contract

## Source of truth

This package pins its protocol implementation against NLWeb Specification v0.55, reviewed 2026-08-31. The authoritative specification defines NLWeb as transport-neutral and defines HTTP bindings plus an MCP binding.

## HTTP

`POST /ask` is the primary natural-language operation. The request contains a required `query` object whose `text` field is required, with optional `context`, `prefer`, and `meta` sections. The HTTP binding also defines `POST /await` for checking or cancelling promised long-running results.

NLWeb responses are JSON and use Schema.org-oriented structured data. The specification documents list and summarize modes and extensibility through `@context`.

## MCP

The `/mcp` surface exposes the NLWeb `ask` operation through MCP. MCP clients can discover and call the tool using the MCP JSON-RPC methods. The package supports `tools/list` and `tools/call` for the core demo surface.

## Discovery is deliberately separate

`/.well-known/nlweb` is an optional package discovery document. The NLWeb specification reviewed for this release does **not** define it as a normative NLWeb HTTP endpoint. Therefore the package never describes it as something that search agents are required to crawl.

Likewise `/health` is operational and is not part of the NLWeb protocol contract.

## Root-domain deployment

For broad domain visibility, mount the integration without a prefix so that the public application exposes `/ask` and `/mcp` directly from the domain root. A prefix remains available for applications whose deployment topology requires it.
