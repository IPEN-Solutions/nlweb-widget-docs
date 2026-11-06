# Extending the widget

The core package is framework-neutral. Protocol behavior belongs in `nlweb_widget.protocol` and `NLWebWidget`; framework modules are thin adapters named `*_integration.py`.

## Fresh-development dependency contract

`uv sync --dev` must be sufficient to collect every repository test. Tests must not import an optional framework unless that framework is included in the development group or the test is explicitly marked as optional.

## Agent demonstrations

The FastAPI retail agent demo is intentionally offline-first. It discovers the MCP `ask` tool, submits a normative `/ask` request to the local application, prints retrieved URLs, and emits a deterministic mock indexing/visibility rank. A live OpenAI-compatible/OpenRouter implementation may be added as an optional layer but must never be required for CI.
