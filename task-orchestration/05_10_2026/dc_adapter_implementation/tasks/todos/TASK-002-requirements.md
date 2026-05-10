# TASK-002: Write requirements.txt with Pinned Dependencies

**Phase:** 1 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #2
**Depends on:** TASK-001
**Status:** todo

## Description
Create `requirements.txt` with exact pinned versions for all spec §2 dependencies.

## Required packages
- `fastapi>=0.111`, `uvicorn[standard]`
- `httpx[http2]`
- `PyJWT`, `cryptography`
- `pydantic-settings>=2`, `pyyaml`
- `structlog`
- `aiokafka`
- `opentelemetry-sdk`, `opentelemetry-exporter-otlp-proto-grpc`
- `opentelemetry-instrumentation-fastapi`, `opentelemetry-instrumentation-httpx`
- `prometheus-client`
- `pytest`, `pytest-asyncio`, `respx`, `pytest-cov`

## Acceptance Criteria
- [ ] `pip install -r requirements.txt` succeeds in clean venv
- [ ] All versions pinned (no bare package names)
- [ ] Dev deps separated under `# dev`

## QA Gate
```bash
pip install -r requirements.txt && python -c "import fastapi, httpx, jwt, structlog" && echo PASS
```
