# Windows 10 x64 development

Use PowerShell and uv. From a clean checkout:

```powershell
uv venv --python 3.10
.venv\Scripts\activate
uv sync --dev
uv run pytest
uv run ruff check .
uv build
```

The package includes a PowerShell bootstrap script and VS Code launch/tasks configuration for the framework examples and their visibility demonstrations.
