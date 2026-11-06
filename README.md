# NLWeb Widget documentation 0.9.12

Standalone Zensical documentation for the approved immutable `nlweb-widget` 0.9.12 runtime. The production package remains intentionally lean; complete framework examples, runnable applications, AskAgent integration, AI visibility demonstrations, starter profiles and provider infrastructure fixtures live in the separately versioned `nlweb-widget-examples` package.

## Build

Use the Python version already installed by the hosting platform, then run:

```powershell
uv sync
uv run zensical build
```

This frozen docs baseline is independently versioned from the Widget runtime. Documentation bundles omit `.python-version`; private maintainers documentation is excluded. A future change requires a new forward-only revision.
