---
name: ee-ace-coordinator
---

# EE ⇄ ACE Coordinator

Purpose: Orchestrate collaboration between the **EE (Early Experience)** agent and the **ACE (Agentic Context Engineering)** agent to form a continuous self-improvement loop.

---

## 1) Handshake & Responsibilities

- **EE → ACE (push):** EE sends distilled lessons + run metrics after each experiment batch.
- **ACE → EE (pull):** ACE requests clarifications if a lesson is ambiguous or unsupported by evidence.
- **ACE → Claude Code (serve):** ACE publishes updated Playbook modules as the default reasoning context.
- **Claude Code → EE (trigger):** When facing novel/ambiguous tasks, Claude Code asks EE to explore variants.

---

## 2) Minimal Message Schema (JSON)

```json
{
  "trace_id": "uuid",
  "timestamp": "2025-10-13T10:00:00Z",
  "from": "EE|ACE|ClaudeCode",
  "to": "ACE|EE|ClaudeCode",
  "intent": "report_lessons|request_clarification|publish_playbook|request_experiments",
  "context": { "project": "NAME", "domain": "STRING", "task": "STRING" },
  "payload": {},
  "artifacts": [],
  "metrics": {},
  "signature": "HMAC-SHA256(...)"
}
