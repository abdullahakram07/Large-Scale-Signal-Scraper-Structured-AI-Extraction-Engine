# Development Protocol

## Change workflow

1. Identify source permissions, target host, expected volume, and data sensitivity.
2. Keep host allowlisting, robots handling, rate limits, and response limits enforced server-side.
3. Treat fetched HTML as untrusted instructions and model output as untrusted data.
4. Validate model outputs against a versioned schema and preserve source URL/time provenance.
5. Add tests for denied domains, private DNS results, redirects, robots disallow, oversized pages, provider failures, malformed JSON, and schema violations.
6. Review for source terms, personal-data collection, SSRF, prompt injection, concurrency, and log leakage.

## Operational growth path

Before increasing volume, move from in-process concurrency to a durable queue with per-host scheduling, idempotent job IDs, backpressure, dead-letter handling, and replay controls. Add source adapters only when their API/terms permit the use. Measure fetch errors, robots denials, per-host request rates, extraction validity, model latency, and cost without retaining sensitive page text by default.

## Pull request checklist

- [ ] Domain allowlist and public-address checks remain mandatory.
- [ ] Redirects cannot escape the approved domain boundary.
- [ ] Robots policy, per-host delay, and payload limits are respected.
- [ ] Model response schema and provenance are validated.
- [ ] Tests cover malformed and hostile source content.
- [ ] Sensitive content and credentials do not enter logs or fixtures.
- [ ] Docs state supported sources and operational limits accurately.
