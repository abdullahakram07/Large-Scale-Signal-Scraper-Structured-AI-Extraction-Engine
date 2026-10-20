# Security and Source Policy

- The configured domain allowlist is the source authorization boundary.
- URLs must use HTTPS, contain no embedded credentials, and resolve to public addresses. Redirects are rejected.
- `robots.txt` must permit the configured crawler user agent; failure to retrieve or parse policy denies the page.
- The crawler uses a per-host delay, bounded concurrency, timeouts, and response-size limits.
- Page text is untrusted and may contain prompt injection. The extraction prompt says to treat it as data, but that is not a guarantee. Validate and review important results.
- Never evade access controls, CAPTCHAs, robots directives, quotas, or source terms. For restricted platforms, use approved APIs or licensed data.
- Prevent sensitive source data from reaching unapproved model providers. Keep page text, prompts, and credentials out of logs.

Network egress restrictions are still required: DNS validation in application code alone cannot fully prevent rebinding or infrastructure-level SSRF.
