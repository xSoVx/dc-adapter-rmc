# TASK-046: Write .env.example

**Phase:** 10 | **Agent:** `python-expert` (sonnet) | **Sub:** `security-auditor` (sonnet) | **GitHub Issue:** #11
**Depends on:** TASK-003
**Status:** todo

## Description
Template `.env.example` with all required env vars and inline comments. Zero default secret values.

## Acceptance Criteria
- [ ] Covers all 5 secret vars (CERT, KEY, CA_CERT, JWT_SIGNING_KEY, ID_REPLACEMENT_AUTH) — values empty
- [ ] PCM endpoints for team-python Connectathon pre-filled as comments
- [ ] `DS_ADAPTER_FHIR_BASE_URL` defaults to HAPI for local testing
- [ ] `security-auditor` confirms no secret has a non-empty default

## QA Gate
```bash
grep "=\S" .env.example | grep -v "^#" | grep -v "hapi.fhir.org" && echo "NON-EMPTY SECRET — FAIL" || echo "PASS"
```
