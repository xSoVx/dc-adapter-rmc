# TASK-023: Instrument 7 Required OTel Spans

**Phase:** 6 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #7
**Depends on:** TASK-022, TASK-016
**Status:** todo

## Description
Add manual span creation inside `fhir_router.py` for all 7 required spans per spec §9.

## Required spans
| Span | Key attributes |
|------|---------------|
| `dc_adapter.request` | `http.method`, `http.route`, `correlation_id` |
| `dc_adapter.pcm_token` | `cache_hit` (bool) |
| `dc_adapter.introspect` | `consent_id`, `active` |
| `dc_adapter.id_resolve` | `attempt_count` |
| `dc_adapter.jwt_mint` | `alg` |
| `dc_adapter.fhir_forward` | `fhir.resource_type`, `http.status_code` |
| `dc_adapter.verify` | `resources_checked`, `forbidden_found` |

## Acceptance Criteria
- [ ] All 7 span names appear in OTel SDK in-memory exporter capture
- [ ] Each span has correct attributes
- [ ] Spans are children of `dc_adapter.request`

## QA Gate
```bash
pytest tests/unit/test_observability.py::test_all_7_spans_created -v
```
