# Contributor workflow

Create a clean uv environment, run the full pytest suite, run Ruff, build the package and build the docs before opening a PR.

A change must be declared by the active revision iteration manifest. The build is forward-only: the genesis or current baseline is never rewritten. A failed iteration leaves the baseline unchanged.

Avoid unrelated refactoring in protocol revisions. Protocol claims must be supported by the pinned NLWeb source review.
