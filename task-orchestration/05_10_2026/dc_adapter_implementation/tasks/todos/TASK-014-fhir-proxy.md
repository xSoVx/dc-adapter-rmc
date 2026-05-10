# TASK-014: Implement FHIR Forward Proxy

**Phase:** 4 | **Agent:** `python-expert` (sonnet) | **Sub:** `performance-engineer` (sonnet) | **GitHub Issue:** #5
**Depends on:** TASK-013
**Status:** todo

## Description
Implement `src/fhir/proxy.py` — strips incoming `Authorization`, injects internal JWT, forwards to FHIR server. Streams response (no buffering).

## EE Experiment (ee-agent) — EXP-002
Variant A: buffer full response → verify → return.
Variant B: stream + verify inline. Metric: memory @ 50MB Bundle.

## Acceptance Criteria
- [ ] Incoming `Authorization` header stripped from outgoing request
- [ ] `Authorization: Bearer <internal_jwt>` set on outgoing request
- [ ] `Host` header not forwarded
- [ ] Response streamed (tested: 50MB body uses < 10MB RAM)
- [ ] Timeout: 30s (from config)

## QA Gate
```bash
pytest tests/unit/test_fhir_proxy.py -v
# test_authorization_stripped_and_replaced
# test_host_not_forwarded
```
