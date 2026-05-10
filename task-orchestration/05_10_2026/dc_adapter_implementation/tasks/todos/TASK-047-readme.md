# TASK-047: Write README.md

**Phase:** 10 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #11
**Depends on:** TASK-044, TASK-045, TASK-046
**Status:** todo

## Description
Concise README covering quick-start (5 commands), config reference, demo flow, architecture diagram, testing instructions.

## Sections required
1. **Quick Start** — 5 commands from clone to `/health` 200
2. **Configuration** — table of all config.yaml sections + env overrides
3. **Demo Flow** — mirrors Hackathon Delivery Scope §6.2 steps 1-6
4. **Architecture** — ASCII diagram (reuse from MASTER-COORDINATION.md)
5. **Testing** — `pytest tests/unit/` and `pytest tests/integration/` instructions
6. **Spec Conformance** — link to spec §14 checklist

## Acceptance Criteria
- [ ] `docker compose up` to running demo in < 5 commands
- [ ] All secret env var names documented
- [ ] HAPI FHIR endpoint noted for local testing
- [ ] Connectathon PCM endpoints noted

## QA Gate
```bash
# README exists and is non-empty
wc -l README.md | awk '{if ($1 > 50) print "README OK"; else print "TOO SHORT — FAIL"}'
```
