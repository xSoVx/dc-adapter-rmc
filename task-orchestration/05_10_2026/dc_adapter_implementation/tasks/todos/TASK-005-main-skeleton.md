# TASK-005: Implement src/main.py Skeleton

**Phase:** 1 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #2
**Depends on:** TASK-003, TASK-004
**Status:** todo

## Description
Implement `src/main.py` with FastAPI app, lifespan context manager stubs, and middleware registration stubs. No real connections yet.

## Acceptance Criteria
- [ ] `FastAPI(title="DC Adapter", version="0.1.0", lifespan=lifespan)`
- [ ] `lifespan` is an `asynccontextmanager` with startup/shutdown stubs
- [ ] `GET /health` returns `{"status":"ok","version":"0.1.0"}`
- [ ] App importable: `from src.main import app`

## QA Gate
```bash
uvicorn src.main:app --port 8080 &
sleep 2 && curl -sf http://localhost:8080/health | python -m json.tool
kill %1
```
