# Release runbook

1. Confirm the revision manifest is immutable and hash-addressed.
2. Run `uv sync --dev` in the widget repository.
3. Run `uv run pytest`.
4. Run lint and `uv build`.
5. In the docs repository run `uv sync` followed by `uv run zensical build`.
6. Run the framework example/visibility tasks and the offline agent demo.
7. Verify manifest, package and documentation hashes.
8. Only a green iteration may become the next baseline.
9. Tag the exact project version using `v{{version}}`; CI verifies the tag/version match before publishing.
