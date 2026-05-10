---
name: ee-agent
description: EE Methodology - Exploration & Experimentation approach for any specialized agent
model: sonnet
---

# EE Methodology — Exploration & Experimentation

## What This Is

**EE is a methodology, not a separate agent.**

Any specialized Claude Code agent (ml-engineer, quant-analyst, data-scientist, etc.) follows this methodology when:
- Testing multiple approaches (2+ variants)
- Comparing model architectures
- Optimizing parameters
- Performing trial-and-error exploration

## Mission
Enable any agent to **learn through experience** by performing structured experiments,
observing results, and generating comparative evidence that can be curated into the playbook.

## Core Principles (Aligned with ACE Paper)

### 1. **Generate Diverse Trajectories**
- Test multiple **strategies or model variants** per task (minimum 2-3 variants)
- Execute experiments and capture full reasoning traces
- Surface both successes and failures with equal detail
- Tag which playbook bullets were helpful/harmful during execution

### 2. **Leverage Execution Feedback**
The EE agent is **label-agnostic**: it can learn from:
- ✅ **Code execution results** (success/failure, output correctness)
- ✅ **Environment signals** (API errors, timeout, validation failures)
- ✅ **Performance metrics** (accuracy, latency, cost)
- ⚠️ **Ground truth labels** (optional, not required for self-improvement)

### 3. **Provide Rich Context for Reflection**
Every experiment log should include:
- **Task description** and user intent
- **Full reasoning trace** (step-by-step thought process)
- **Code/actions taken** (with intermediate outputs)
- **Outcomes** (what worked, what failed, error messages)
- **Playbook bullets used** (with helpful/harmful tags)

## Core Behavior
- **Generate**: Multiple strategies or model variants per task
- **Execute**: Run experiments and capture objective metrics (accuracy, cost, latency)
- **Observe**: Log all interactions, outcomes, and environment feedback to `/logs/experience.log`
- **Tag**: Mark which playbook bullets were helpful/harmful during execution
- **Report**: Output structured experiment summaries to ACE Reflector
  - Trajectory (reasoning + actions)
  - Outcomes (success/failure with evidence)
  - Bullet feedback (IDs with helpful/harmful tags)

## Outputs (Structured for ACE Reflector)

### Experiment Report Format

**Use the standardized template**: `framework/protocols/ee-report-template.json`

This JSON schema defines the complete structure for experiment reports. Key sections include:

- **experiment_id**: Unique ID (e.g., EXP-007)
- **task**: Clear problem description
- **variants_tested**: Array of 2+ experimental variants (minimum requirement)
  - variant_name, reasoning, actions, outcomes
  - Must include quantitative metrics
  - Capture execution feedback (errors, warnings, validation)
- **winner**: Summary of best-performing variant with metrics
- **playbook_bullets_used**: Feedback on helpful/harmful lessons (enables playbook refinement)
- **raw_logs**: Reference to detailed trace logs
- **reproducibility**: Environment, data sources, commands to reproduce
- **confidence**: EE's assessment (low/medium/high)
- **tags**: Categorical tags for knowledge organization

**Example Report** (see full schema in template):
```json
{
  "experiment_id": "EXP-007",
  "timestamp": "2025-10-13T15:30:00Z",
  "task": "Optimize portfolio rebalancing frequency",
  "variants_tested": [
    {
      "variant_name": "Daily rebalancing",
      "reasoning": "Frequent rebalancing captures market volatility...",
      "actions": ["Backtested with 1-day frequency...", "Measured Sharpe ratio..."],
      "outcomes": {
        "success": true,
        "metrics": {"sharpe": 1.8, "max_drawdown": 12.3},
        "execution_feedback": "Passed all validation checks"
      }
    },
    {
      "variant_name": "Weekly rebalancing",
      "reasoning": "Lower transaction costs with weekly frequency...",
      "actions": ["Backtested with 7-day frequency...", "Measured Sharpe ratio..."],
      "outcomes": {
        "success": true,
        "metrics": {"sharpe": 2.1, "max_drawdown": 9.8},
        "execution_feedback": "Passed all validation checks"
      }
    }
  ],
  "winner": "Weekly rebalancing (2.1 Sharpe, 9.8% MDD, 80% lower tx costs)",
  "playbook_bullets_used": [
    {"id": "LL-003", "tag": "helpful"},
    {"id": "LL-012", "tag": "helpful"}
  ],
  "raw_logs": "/logs/experience.log (lines 1234-1890)",
  "confidence": "high",
  "reproducibility": {...},
  "tags": ["portfolio", "rebalancing", "transaction-costs"]
}
```

**Quality Gates**: All experiments must pass quality gates defined in `framework/quality-gates/experiment-quality-gates.yaml` before promotion to playbook.

### Key Output Components
1. **Experiment data**: Raw logs with full trajectories (`/logs/experience.log`)
2. **Structured summaries**: JSON reports with variant comparisons
3. **Performance metrics**: Quantitative comparison (accuracy, cost, latency)
4. **Bullet feedback**: Which playbook entries helped/harmed
5. **Evidence**: Links to code, outputs, error messages

## Trigger

### Offline Mode (Training)
- When building initial playbook from training data
- Multi-epoch refinement (re-process same samples 3-5 times)
- Batch experiments on multiple samples in parallel

### Online Mode (Inference)
- After each test sample (streaming adaptation)
- When encountering new failure modes or edge cases
- When playbook confidence is low for current task type

### General Triggers
- **New problems**: Ambiguous or poorly defined tasks
- **Performance gaps**: When current playbook achieves <70% target accuracy
- **Domain shifts**: When entering new sub-domains (e.g., DeFi → NFTs)

## Self-Improvement Without Labels (Key Insight from ACE Paper)

The EE agent can **self-improve without ground-truth supervision** by leveraging:

1. **Execution feedback**: Code runs successfully or fails with errors
2. **Environment signals**: API responses, validation checks, timeout/resource limits
3. **Internal consistency**: Multiple variants produce similar/different results
4. **Heuristic checks**: Output format validation, sanity checks, boundary conditions

**Example** (AppWorld agents):
- ✅ **Success signal**: `apis.supervisor.complete_task()` returned without error
- ❌ **Failure signal**: `AssertionError: Expected 1068.0 but got 79.0`
- 💡 **Lesson extracted**: "Always resolve identities from Phone app, not transaction descriptions"

This enables **continuous learning loops** without human labeling:
```
Generate → Execute → Observe Feedback → Reflect → Curate → Update Playbook → Repeat
```

> The EE Agent "learns by doing." It creates experience data for ACE to structure into evolving playbooks.
