# TASK-010: Implement ID Replacement Client with Retry+Jitter

**Phase:** 3 | **Agent:** `ee-agent`+`python-expert` (sonnet) | **Sub:** `backend-architect` (sonnet) | **GitHub Issue:** #4
**Depends on:** TASK-005
**Status:** todo

## Description
Implement `src/identity/id_replacement.py` — POST `/api/v1/resolve`, 1s timeout, 3 retries with exponential+jitter backoff.

## EE Experiment (ee-agent, sonnet) — EXP-001
Variants: uniform jitter / full jitter / decorrelated jitter. Metric: p99 latency under simulated thundering herd. Winner → playbook LL-001.

## Acceptance Criteria
- [ ] Timeout: `config.identity.timeout` (default 1.0s)
- [ ] Retries: up to `config.identity.retries` (default 3)
- [ ] Jitter: stddev of sleep times > 0 (verified in test)
- [ ] All retries exhausted → `IdentityResolutionError` (DS-503 → HTTP 503)
- [ ] `national_id` masked in all log output

## QA Gate
```bash
pytest tests/unit/test_id_replacement.py -v
# test_jitter_varies_sleep_times: assert stddev > 0
```
