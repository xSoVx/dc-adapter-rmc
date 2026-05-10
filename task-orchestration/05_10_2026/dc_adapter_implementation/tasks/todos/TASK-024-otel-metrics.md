# TASK-024: Register 8 Required OTel Metrics

**Phase:** 6 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #7
**Depends on:** TASK-022
**Status:** todo

## Description
Register all 8 required metrics in `src/observability/metrics.py` and instrument them at the right call sites.

## Required metrics
`dc_adapter.requests.total`, `dc_adapter.request.duration`, `dc_adapter.pcm_token.cache_hits`, `dc_adapter.pcm_token.cache_misses`, `dc_adapter.introspection.duration`, `dc_adapter.id_resolve.duration`, `dc_adapter.fhir_forward.duration`, `dc_adapter.audit.queue_depth`

## Acceptance Criteria
- [ ] All 8 metric names registered at startup
- [ ] `dc_adapter.requests.total` increments on each request
- [ ] `cache_hits`/`cache_misses` updated in token_service
- [ ] `audit.queue_depth` is a Gauge updated by audit service
- [ ] `/metrics` returns all 8 in Prometheus format

## QA Gate
```bash
curl -sf http://localhost:8080/metrics | grep -c "dc_adapter_" | grep -q "^8$" && echo "8 metrics — PASS"
```
