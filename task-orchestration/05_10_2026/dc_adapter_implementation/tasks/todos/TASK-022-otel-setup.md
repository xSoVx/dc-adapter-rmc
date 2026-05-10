# TASK-022: Configure OpenTelemetry SDK

**Phase:** 6 | **Agent:** `python-expert` (sonnet) | **Sub:** `performance-engineer` (sonnet) | **GitHub Issue:** #7
**Depends on:** TASK-005
**Status:** todo

## Description
Initialize OTel SDK in `src/observability/otel.py`: TracerProvider (OTLP gRPC), MeterProvider (Prometheus), auto-instrumentation for FastAPI and httpx.

## EE Experiment (ee-agent) — EXP-004
Variant A: OTLP gRPC only. Variant B: Prometheus pull only. Variant C: both. Metric: startup time, per-request overhead.

## Acceptance Criteria
- [ ] `FastAPIInstrumentor().instrument_app(app)` called on startup
- [ ] `HTTPXClientInstrumentor().instrument()` called on startup
- [ ] Resource: `service.name`, `service.version`, `deployment.environment`
- [ ] App starts without crash when `otlp_endpoint` is empty

## QA Gate
```bash
DS_ADAPTER_OBSERVABILITY_OTLP_ENDPOINT="" uvicorn src.main:app --port 8080 &
sleep 2 && curl -sf http://localhost:8080/health && echo "Starts without OTel — PASS"
kill %1
```
