# Local Setup and Deployment

## Run locally

```sh
cd "Large-Scale-Signal-Scraper-Structured-AI-Extraction-Engine"
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
export ALLOWED_DOMAINS='example.org'
export LLM_EXTRACTOR_URL='https://provider.example/v1/chat/completions'
export LLM_EXTRACTOR_MODEL='your-approved-json-capable-model'
export LLM_EXTRACTOR_API_KEY='replace-with-a-provider-key'
uvicorn app.main:app --host 127.0.0.1 --port 8011
```

Use real host and provider values only after verifying the domain's collection permissions and provider data handling. The sample values above are placeholders.

## API example

```sh
curl -sS http://127.0.0.1:8011/extract \
  -H 'content-type: application/json' \
  -d '{"urls":["https://example.org/catalog/item"],"output_schema":{"type":"object","properties":{"title":{"type":"string"},"price":{"type":["number","null"]}},"required":["title","price"],"additionalProperties":false}}'
```

## Deployment security

The service has no authentication and is local-development only. Before network exposure add identity and tenant authorization, durable job processing, quotas, source-specific approvals, and monitoring. DNS is checked before fetch, but application checks cannot replace network egress controls against DNS rebinding; deploy with firewall or proxy rules that deny private, loopback, link-local, and metadata-service destinations. Do not allow user-controlled domains to bypass `ALLOWED_DOMAINS`.
