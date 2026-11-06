# Production deployment

Expose the protocol at the public domain root:

- `POST /ask`
- `POST /mcp`
- `/await` is not a normative/current package endpoint; do not configure clients to depend on it.
- `GET /.well-known/nlweb` for optional package discovery metadata
- `GET /health` for operations

Place normal authentication, authorization, rate limiting, TLS termination and request-size controls at the transport/application boundary. NLWeb itself treats authentication and rate limiting as transport concerns.

The public projection should contain only information the domain owner intentionally makes available to AI consumers. Never index private records merely because they exist in the authoritative application database.
