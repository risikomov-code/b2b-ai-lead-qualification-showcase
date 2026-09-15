# Architecture Notes

This document explains the qualification architecture without exposing private prospect data or proprietary commercial rules.

## 1. Intake

Prospects may originate from a professional-network export, research list, website lead source, event list, spreadsheet or another structured source.

The production implementation normalises records into a consistent internal shape before qualification.

Typical fields may include:

- company context;
- role / seniority;
- geography;
- business category;
- stated objective;
- response status;
- prior interaction state.

The public showcase intentionally omits real field mappings and source-specific identifiers.

## 2. Validation

Before AI classification, the workflow checks whether the record contains enough information to support a meaningful decision.

Examples:

- missing company context;
- missing role;
- contradictory market information;
- duplicate records;
- records already actioned;
- insufficient conversation context.

A record that fails validation should not be silently treated as qualified.

## 3. AI-assisted qualification

AI is used as a bounded decision-support layer, not as an unrestricted sales agent.

The model receives a controlled subset of prospect context and returns structured classification fields.

Possible output concepts include:

- fit level;
- opportunity type;
- commercial relevance;
- priority;
- confidence;
- rationale;
- recommended next action.

Exact prompts, labels and thresholds are private.

## 4. Decision routing

The workflow routes the record based on structured outcomes.

### High priority

Potentially valuable or strategically relevant records are surfaced for human review.

### Medium priority

Relevant contacts with incomplete intent or weaker urgency enter a follow-up queue.

### Low / unclear

Records may be held, nurtured or excluded from immediate action.

## 5. Human review

The system preserves a human decision gate before commercially sensitive outreach or commitment.

This allows the reviewer to:

- confirm or override the classification;
- check business nuance;
- reject false positives;
- choose the appropriate response strategy;
- escalate high-value opportunities.

## 6. CRM-ready output

Approved records are converted into a consistent downstream structure.

Representative fields:

```text
qualification_status
fit_category
priority
confidence
rationale
recommended_action
follow_up_state
human_review_required
```

The showcase uses a provider-neutral contract. A production deployment may map these fields to a CRM, spreadsheet, database or sales workflow.

## 7. Privacy boundary

Personal data should be minimised at every stage.

The architecture separates:

- operational identifiers;
- qualification features;
- private contact details;
- AI context;
- downstream sales data.

Only the minimum context required for a qualification decision should be sent to an AI provider.

## Engineering patterns demonstrated

- schema normalisation
- input validation
- structured LLM output
- decision routing
- confidence-aware handling
- human-in-the-loop automation
- privacy-by-design
- CRM-neutral integration
- error / ambiguity states
- auditable workflow design

## Deliberately omitted

- real prospect records
- source exports
- private taxonomies
- prompt text
- scoring formulas
- automation node graphs
- CRM mappings
- credentials
- endpoints
- message templates
