# TASK-025: Configure structlog JSON Logging

**Phase:** 6 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #7
**Depends on:** TASK-005
**Status:** todo

## Description
Configure structlog in `src/logging/setup.py`: JSON renderer, ISO timestamps, level-based stream routing (INFO/DEBUG → stdout, WARNING/ERROR → stderr).

## Acceptance Criteria
- [ ] Every log line is valid JSON with `timestamp`, `level`, `event`, `correlation_id`
- [ ] INFO/DEBUG → sys.stdout
- [ ] WARNING/ERROR → sys.stderr
- [ ] `DEBUG` enabled when `DS_ADAPTER_LOGGING_LEVEL=DEBUG`
- [ ] `setup_logging()` called before app startup in lifespan

## QA Gate
```bash
uvicorn src.main:app --port 8080 > /tmp/stdout.log 2>/tmp/stderr.log &
curl -sf http://localhost:8080/health
python3 -c "
import json
lines = open('/tmp/stdout.log').readlines()
for l in lines:
    e = json.loads(l)
    assert e['level'] in ('info','debug'), f'Wrong level on stdout: {e}'
print('stdout routing PASS')
"
kill %1
```
