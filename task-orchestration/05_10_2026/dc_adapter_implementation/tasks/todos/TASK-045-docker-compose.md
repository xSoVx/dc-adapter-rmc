# TASK-045: Write docker-compose.yaml

**Phase:** 10 | **Agent:** `deployment-engineer` (haiku) | **GitHub Issue:** #11
**Depends on:** TASK-044, TASK-011
**Status:** todo

## Services
- `dc-adapter`: main service, port 8080, all DS_ADAPTER_* env keys, volume `./certs:/certs:ro`, depends on `mock-id-service`
- `mock-id-service`: port 9001, for local demo
- `jaeger` (optional): `jaegertracing/all-in-one:latest`, ports 16686, 4317

## Acceptance Criteria
- [ ] `docker compose up -d` succeeds
- [ ] `/health` returns 200 within 10s
- [ ] `docker compose stop dc-adapter` triggers graceful shutdown
- [ ] Jaeger service optional (profile: `observability`)

## QA Gate
```bash
docker compose up -d && sleep 10
curl -sf http://localhost:8080/health | python -m json.tool
docker compose down
```
