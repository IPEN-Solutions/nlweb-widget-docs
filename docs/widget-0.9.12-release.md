# Widget 0.9.12 release record

Widget 0.9.12 is the approved immutable runtime baseline. It includes protocol projection and HTTP `/ask` Server-Sent Events behavior for requests that set `prefer.streaming` to true. The HTTP `/ask` streaming response is distinct from the JSON-RPC response on `/mcp`.

Consumer Windows QA on Python 3.10.21 reported 58 passed and 6 optional-provider tests skipped. Optional providers require their own configured-provider QA when enabled.

The corresponding standalone documentation bundle is independently versioned and approved as `nlweb-widget-docs-0.9.12`. Examples and ecosystem-docs candidates are governed separately; inclusion in the ecosystem master book does not promote them.
