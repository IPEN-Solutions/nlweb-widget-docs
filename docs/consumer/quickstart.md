# Quickstart

## Install the documentation site

This repository is a static documentation project, not a Python runtime package. From the repository root:

```powershell
uv venv --python 3.13
uv sync
uv run zensical build
```

The project deliberately uses `[tool.uv] package = false`, so `uv sync` does not attempt an editable Hatchling build.

## Install the widget repository

For package development:

```powershell
uv venv --python 3.10
uv sync --dev
uv run pytest
```

The development dependency group includes the framework packages required by the bundled framework examples/tests. Consumers install only the framework extra they actually use.


## Enable the projection

The production default is intentionally safe: set `NLWEB_ENABLED=true` when the application is ready for projection and retrieval. See [Configuration](configuration.md) for conditional provider and synchronization settings.


For HTTP `/ask`, clients may request Server-Sent Events with `prefer: {"streaming": true}`. The HTTP streaming response is an SSE event stream; `/mcp` remains JSON-RPC and is not converted into SSE by this preference.
