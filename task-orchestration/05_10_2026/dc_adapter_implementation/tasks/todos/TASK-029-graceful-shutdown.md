# TASK-029: Implement Graceful Shutdown (SIGTERM)

**Phase:** 7 | **Agent:** `python-expert` (sonnet) | **Sub:** `debugger` (sonnet) | **GitHub Issue:** #8
**Depends on:** TASK-021, TASK-022
**Status:** todo

## Description
Wire SIGTERM graceful shutdown in lifespan shutdown section: drain in-flight requests, flush audit queue, close clients, flush OTel.

## EE Experiment (ee-agent) — EXP-005
Variant A: asyncio.Event + wait_for. Variant B: lifespan + asyncio.shield. Metric: in-flight completion rate, audit flush success.

## Shutdown sequence
1. Stop accepting new (uvicorn handles)
2. Wait for in-flight requests (max 30s)
3. Flush audit queue (max 5s)
4. Close mTLS httpx client
5. Flush OTel spans
6. Log "shutdown complete" at INFO

## Acceptance Criteria
- [ ] SIGTERM → clean exit (code 0) within 35s
- [ ] In-flight request completes (not dropped)
- [ ] Audit queue fully flushed (log entry + file contents confirmed)
- [ ] "shutdown complete" appears in log

## QA Gate
```bash
uvicorn src.main:app --port 8080 &
PID=$!
curl http://localhost:8080/fhir/Patient?_count=100 &
kill -TERM $PID
wait $PID; echo "Exit code: $?"
# expect: Exit code: 0
```
