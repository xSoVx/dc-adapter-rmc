---
name: ace-agent
---

# ACE Methodology — Agentic Context Engineering

## What This Is

**ACE is a methodology, not a separate agent.**

Any specialized Claude Code agent (ml-engineer, quant-analyst, data-scientist, etc.) follows this methodology when:
- Structuring experimental results into playbook
- Updating knowledge base with validated insights
- Curating lessons learned
- Refining existing knowledge

## Mission
Enable any agent to transform raw experiential data into **evolving, comprehensive playbooks**
that accumulate, refine, and organize strategies over time—preventing context collapse while
preserving detailed domain knowledge.

## Core Principles (from ACE Paper)

### 1. **Contexts as Evolving Playbooks, Not Summaries**
- **Avoid brevity bias**: Don't compress insights into concise summaries
- **Comprehensive over concise**: LLMs perform better with detailed, inclusive contexts
- **Grow-and-refine**: Steadily accumulate knowledge while pruning redundancy

### 2. **Prevent Context Collapse**
- **Never use monolithic rewriting**: Full context rewrites cause catastrophic information loss
- **Incremental delta updates**: Add structured bullets, update counters, append insights
- **Preserve domain details**: Keep tactical knowledge, tool guidelines, failure modes

### 3. **Structured, Itemized Bullets**
Each playbook entry contains:
- **Metadata**: Unique ID, helpful/harmful counters, confidence level
- **Content**: Reusable strategy, domain concept, or common failure mode
- **Evidence**: Links to experiments (EXP-001, etc.) and confidence scores

## Core Behavior
- **Receive**: Experiment reports from EE agent (see `framework/protocols/ee-report-template.json`)
- **Reflect**: Validate evidence quality and extract concrete insights (iterative refinement)
- **Curate**: Synthesize lessons into compact delta entries (structured bullets)
- **Merge**: Deterministically integrate deltas into `/knowledge/playbook.yaml`
- **Refine**: De-duplicate via semantic embeddings, update helpful/harmful counters
- **Version**: Track changes in `/logs/playbook_history.log` with clear attribution
- **Load**: Inject relevant playbook sections into Claude Code's context for reasoning

**Follow the ACE Processing Protocol**: `framework/protocols/ace-processing-protocol.md` for detailed workflow steps.

## Workflow: Generation → Reflection → Curation

```
┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│  EE Agent   │  →   │  Reflector  │  →   │  Curator    │
│ (Generator) │      │  (ACE)      │      │  (ACE)      │
└─────────────┘      └─────────────┘      └─────────────┘
      ↓                     ↓                     ↓
  Trajectories          Insights            Delta Context
      ↓                     ↓                     ↓
      └─────────────────────┴──────────────────→ Playbook
```

### Phase 1: Generator (EE Agent)
- Produces reasoning trajectories and surfaces strategies/pitfalls
- Tags which playbook bullets were helpful/harmful

### Phase 2: Reflector (ACE Agent)
- **Critiques** EE's traces to extract concrete lessons
- **Refines** insights across multiple iterations (up to 5 rounds)
- **Validates** evidence quality and clarity
- Outputs: reasoning, error identification, root cause, correct approach, key insights

### Phase 3: Curator (ACE Agent)
- **Synthesizes** Reflector insights into compact delta entries
- **Merges** deltas deterministically into playbook (non-LLM logic)
- **De-duplicates** via semantic embeddings
- **Updates** helpful/harmful counters for existing bullets

## Outputs
- Updated `/knowledge/playbook.yaml` (versioned, with bullet IDs)
- Versioned change log `/logs/playbook_history.log`
- Delta context items (structured JSON/YAML with metadata)
- Performance metrics (accuracy gains, cost reduction, latency improvement)

**Quality Assurance**: Validate experiments against quality gates in `framework/quality-gates/experiment-quality-gates.yaml` before integration.

## Trigger
- **Offline**: After EE completes experiments on training data
- **Online**: After each test sample (streaming adaptation at inference time)
- **Multi-epoch**: Re-process training samples to progressively strengthen context

## Key Performance Indicators (from ACE Paper)
- **+10.6% average on agent benchmarks** (AppWorld)
- **+8.6% average on domain-specific tasks** (FiNER, Formula)
- **86.9% lower adaptation latency** vs monolithic rewriting methods
- **Works without ground-truth labels** (leverages execution feedback)

> The ACE Agent "learns by structuring." It builds comprehensive, evolving playbooks that prevent collapse.

---

## 🧩 Playbook Structure (Enhanced ACE Schema)

Based on the ACE paper, playbooks now use **itemized bullets with metadata** to enable:
- Fine-grained retrieval (only load relevant bullets)
- Localized updates (modify specific entries, not entire contexts)
- Feedback tracking (helpful/harmful counters guide pruning)

```yaml
project: CryptoRain
domain: ai-ml-crypto-trading
version: 0.3.2
status: battle-hardened
last_updated: "2025-10-13T21:00:00Z"

metadata:
  author: ace-agent
  purpose: "Structured knowledge base for AI/ML crypto trading bot development"
  target_audience: [claude-code, future-developers, ee-agent]

contexts:
  - name: "ML Model Selection"
    description: "Choosing appropriate ML architectures for crypto price prediction"
    triggers:
      - "Need to predict price movements"
      - "Evaluating different model architectures"

    patterns:
      - pattern: "GRU for crypto price prediction"
        rationale: "GRU achieves 0.09% MAPE on 60-min Bitcoin prediction, 61% better than LSTM"
        evidence: ["EXP-001: 15+ peer-reviewed studies, p<0.05"]
        confidence: "high (90%)"

    anti_patterns:
      - anti_pattern: "Using Transformer models for crypto trading"
        why_harmful: "High variance on retraining, unstable predictions"
        evidence: ["EXP-001: Multiple studies show LSTM superior"]
        severity: "critical"

    decision_points:
      - question: "Which model family best handles crypto volatility?"
        options:
          - "Short-term: GRU (0.09% MAPE)"
          - "Production: GRU+LSTM ensemble"
        recommendation: "GRU as primary, LSTM as secondary"

lessons_learned:
  - id: "LL-001"
    lesson: "GRU outperforms LSTM for crypto by 61% on MAPE"
    context: "ML model selection for crypto price prediction"
    evidence: "EXP-001: 15+ peer-reviewed studies"
    confidence: "high (90%)"
    transferability: "domain-specific (crypto trading)"
    helpful_count: 0
    harmful_count: 0
    tags: ["ml", "gru", "crypto", "model-selection"]

history:
  - version: "0.3.2"
    date: "2025-10-13T21:00:00Z"
    changes: "Added meta-framework insights, ACE paper alignment"
    author: "claude-code + dx-optimizer"
```

### ACE-Specific Enhancements
1. **Bullet IDs**: Each entry has unique ID (e.g., `LL-001`, `ctx-00263`)
2. **Counters**: Track `helpful_count` and `harmful_count` from Generator feedback
3. **Confidence**: Explicit confidence levels (low/medium/high with percentages)
4. **Transferability**: Project-specific, domain-specific, or universal
5. **Evidence Links**: All claims cite experiments (EXP-001, EXP-002, etc.)

### Anti-Patterns to Avoid (from ACE Paper)
❌ **Brevity bias**: Compressing insights into short summaries
❌ **Context collapse**: Monolithic LLM rewrites that lose information
❌ **Generic advice**: "Create unit tests" without domain-specific details
❌ **Static contexts**: Never updating or refining accumulated knowledge

✅ **Best Practices**:
- Accumulate detailed, tactical knowledge over time
- Use incremental delta updates (never full rewrites)
- Preserve domain-specific heuristics and failure modes
- Let the LLM decide relevance at inference time (don't pre-filter)
