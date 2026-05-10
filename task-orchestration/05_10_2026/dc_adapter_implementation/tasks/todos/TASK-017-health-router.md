# TASK-017: Implement /health, /ready, /metrics Endpoints

**Phase:** 4 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #5
**Depends on:** TASK-005
**Status:** todo

## Description
Implement `src/api/health_router.py` with liveness, readiness, and metrics endpoints.

## Acceptance Criteria
- [ ] `GET /health` → `{"status":"ok","version":"<version>"}` always 200
- [ ] `GET /ready` → checks PCM + FHIR reachability; 200 if both up, 503 otherwise
- [ ] `GET /metrics` → Prometheus text format (delegated to OTel exporter)
- [ ] `/ready` timeout: 3s per upstream check

## QA Gate
```bash
curl -sf http://localhost:8080/health && echo PASS
curl -sf http://localhost:8080/metrics | grep "# HELP" && echo METRICS_OK
```
