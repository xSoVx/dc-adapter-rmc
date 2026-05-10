# TASK-035: tests/unit/test_audit_service.py

**Phase:** 8 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #9
**Depends on:** TASK-021
**Status:** todo

## Tests required (5)
- `test_patient_id_masked_last_4_digits`
- `test_event_written_to_file`
- `test_file_write_failure_does_not_propagate`
- `test_kafka_skipped_when_not_configured`
- `test_queue_flushed_on_shutdown`

## QA Gate: all 5 pass, file write failure must NOT affect response
