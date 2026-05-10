# TASK-006: Implement mTLS httpx Client

**Phase:** 2 | **Agent:** `python-expert` (sonnet) | **Sub:** `security-auditor` (sonnet) | **GitHub Issue:** #3
**Depends on:** TASK-005
**Status:** todo

## Description
Build `src/auth/mtls_client.py` — an `httpx.AsyncClient` with mTLS configured from env secrets. Expose singleton with async lifecycle managed via lifespan.

## Acceptance Criteria
- [ ] `mtls_client=true` → `cert=(DS_ADAPTER_PCM_CLIENT_CERT, DS_ADAPTER_PCM_CLIENT_KEY)`, `verify=DS_ADAPTER_PCM_CA_CERT`
- [ ] `mtls_client=false` → standard TLS (`verify=True`)
- [ ] `http2=True`
- [ ] Client closed on shutdown (no resource leak)
- [ ] `security-auditor` confirms no cert path written to logs

## QA Gate
```bash
pytest tests/unit/test_mtls_client.py -v
# test_mtls_enabled_uses_cert_tuple
# test_mtls_disabled_uses_plain_tls
# test_client_closed_on_shutdown
```
