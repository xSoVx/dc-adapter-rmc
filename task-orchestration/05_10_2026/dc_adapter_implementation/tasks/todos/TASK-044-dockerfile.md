# TASK-044: Write Multi-stage Dockerfile

**Phase:** 10 | **Agent:** `deployment-engineer` (haiku) | **GitHub Issue:** #11
**Depends on:** TASK-002
**Status:** todo

## Description
Multi-stage Dockerfile per spec §12. Stage 1: install deps. Stage 2: runtime as non-root.

## Acceptance Criteria
- [ ] Stage 1 (`builder`): `python:3.11-slim`, deps into `/install`
- [ ] Stage 2 (`runtime`): copy `/install`, copy `src/`, copy `config.yaml`
- [ ] Non-root user: `useradd -r -u 1001 adapter && USER adapter`
- [ ] `EXPOSE 8080`
- [ ] `HEALTHCHECK --interval=30s --timeout=5s CMD curl -sf http://localhost:8080/health`
- [ ] No secrets baked in (all via env at runtime)
- [ ] Image < 500MB

## QA Gate
```bash
docker build -t dc-adapter:latest . && docker run --rm dc-adapter:latest whoami
# expect: adapter
```
