# TASK-004: Create config.yaml with All Sections

**Phase:** 1 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #2
**Depends on:** TASK-003
**Status:** todo

## Description
Create `config.yaml` with sensible defaults for all sections. No secret values.

## Required structure
```yaml
pcm:
  base_url: ""
  mtls_client: true
  token_ttl_margin_seconds: 5

identity:
  base_url: "http://localhost:9001"
  timeout: 1.0
  retries: 3

fhir:
  base_url: "https://hapi.fhir.org/baseR4"
  forbidden_label: "http://fhir.health.gov.il/cs/il-core-main-security-label|V"
  timeout: 30

jwt:
  algorithm: "ES256"
  issuer: "dc-adapter"
  audience: "fhir-server"
  ttl_seconds: 300

audit:
  targets: ["file"]
  file_path: "/var/log/dc-adapter/audit.jsonl"
  include_response: false

observability:
  otlp_endpoint: ""
  service_name: "dc-adapter"

logging:
  level: "INFO"
```

## Acceptance Criteria
- [ ] No secret value appears in file
- [ ] `fhir.base_url` defaults to HAPI for local testing
- [ ] `audit.include_response` defaults to `false`

## QA Gate
```bash
grep -n "KEY\|CERT\|SECRET\|PASSWORD" config.yaml && echo "SECRETS FOUND — FAIL" || echo "Clean — PASS"
```
