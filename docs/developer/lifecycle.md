# Operational lifecycle boundary

The current widget lifecycle is intentionally small.

1. Construct `NLWebWidget` with validated settings.
2. `startup()` initializes a selected external provider when configured.
3. If enabled, configured authoritative content sources may be synchronized through `ContentSyncService`.
4. Protocol bindings consult `widget.effective_state`.
5. `close()` stops optional synchronization and closes external providers.

`NLWEB_ENABLED=false` prevents projection and retrieval. It does not provide administrative suspension, scheduled expiration, hibernation, or authorization.

Those capabilities belong to the separate future administrative extension manifest. That extension may later mount administrative endpoints on a widget-owned router, but those endpoints must remain outside the normative `/ask` and `/mcp` protocol operations and must require authentication and authorization.
