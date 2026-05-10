# TASK-036: tests/unit/test_errors.py

**Phase:** 8 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #9
**Depends on:** TASK-026, TASK-027, TASK-028
**Status:** todo

## Tests required (5)
- `test_all_13_error_codes_map_to_correct_http_status` (parametrized)
- `test_operation_outcome_structure` (resourceType, system URL, coding)
- `test_no_stack_trace_in_response`
- `test_generic_exception_maps_to_ds500`
- `test_operation_outcome_no_patient_data_leaked`

## QA Gate: all 5 pass, system URL exact match
