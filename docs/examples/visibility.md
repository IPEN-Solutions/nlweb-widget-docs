# AI-visibility demonstrations

Every framework example has a paired visibility demonstration. Each demo starts the example application, submits a natural-language query to `/ask` or `/mcp`, and prints a deterministic mock AI-search indexing/visibility result.

The demo proves the integration path; it does not claim to reproduce a real search engine's ranking or indexing algorithm. OpenRouter is an optional OpenAI-compatible live LLM provider and is never required by the default CI suite.


## Example execution contract

Every bundled visibility demo is runnable in either of these forms from the repository root:

```powershell
uv run python examples/fastapi_retail/visibility_demo/run_demo.py
uv run python -m examples.fastapi_retail.visibility_demo.run_demo
```

Framework examples must not depend on the caller's current working directory or an IDE-specific `PYTHONPATH`. The same rule applies to the FastAPI retail agent companion. This makes the examples usable from PowerShell, VS Code tasks, CI, and direct Python invocation.
