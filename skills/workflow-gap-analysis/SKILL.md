---
name: workflow-gap-analysis
description: "Analyze a text-based workflow to identify gaps, missing processes, and improvement opportunities based on industry best practices. Use when (1) User has a draft workflow and wants expert review, (2) User asks to find gaps or missing processes in a workflow, (3) User wants to improve or enhance an existing workflow, (4) User mentions gap analysis, best practices, or workflow improvement, (5) Following workflow-architect output that needs refinement."
disable-model-invocation: true
argument-hint: "[paste transcript or workflow below]"
---

# Workflow Gap Analysis

Analyze existing workflows against industry best practices to identify gaps, missing processes, and improvement opportunities.

## Workflow Hierarchy

Workflows use this three-level structure:

1. **Phase** — Major stage of the process
2. **Process** — Key action or milestone within a phase
3. **Core Activity** — Granular task within a process

Gap analysis examines all three levels for completeness.

---

## Failures to Avoid

The following are **critical failures** that invalidate a gap analysis. The AI must avoid these errors.

### Analysis Failures

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| No industry research | Gaps based only on general knowledge | Always search for industry-specific best practices |
| Generic recommendations | "Add more quality checks" | "Add inspection after drywall installation per ICC guidelines" |
| Ignoring company size | Enterprise solutions for 5-person company | Scale recommendations to actual business size |
| Missing prioritization | Flat list of 20 gaps | Rank by impact, frequency, and effort |

### Terminology Failures

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| Using "step" | Incorrect hierarchy term | Use "process" as the middle tier |
| Mixing hierarchy levels | Recommending a "phase" that's really a "process" | Match recommendation to appropriate level |

### Recommendation Failures

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| Personal names in additions | "Add Sarah to review" | "Add Operations Manager review" |
| Roles in process titles | "Sales Team Follow-up" | "Post-Sale Follow-up" |
| Activities without action verbs | "Customer feedback" | "Collect customer feedback" |
| Vague additions | "Add quality process" | Specify exact process with core activities |

### Core Activity Failures (for proposed additions)

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| Missing action verb | "Quality documentation" | "Document quality inspection results" |
| Starting with a noun | "Report to manager" | "Submit report to manager" |
| Role in activity title | "QA reviews output" | "Review output for defects" |
| Passive voice | "Items are inspected" | "Inspect items for damage" |

### Structural Failures

| Failure | Why It's Wrong |
|---------|----------------|
| Gaps without location | "Add quality check" with no phase/process specified |
| Missing risk assessment | Gap identified without explaining the risk |
| No actionable recommendation | Problem stated but no solution provided |
| Enhanced workflow doesn't integrate | New items don't fit logically into existing structure |

---

## Required Context

Before analysis, gather:
1. **The workflow** — Text-based workflow to analyze
2. **Industry** — What industry or business type (e.g., construction, SaaS, healthcare)
3. **Company type** — B2B, B2C, service, product, project-based
4. **Company size** — Solo, small team (2-10), medium (11-50), large (50+)

If any context is missing, ask before proceeding.

## Analysis Process

### Step 1: Research Industry Best Practices

Use web search to research:
- "[Industry] [process type] best practices"
- "[Industry] workflow optimization"
- "Common [process type] mistakes [industry]"

Focus on:
- What high-performing companies in this industry do
- Common failure points in this type of process
- Regulatory or compliance requirements
- Technology/tools commonly used

### Step 2: Analyze Phase Level

For each phase, evaluate:
- Are all necessary phases present?
- Are phases in the right sequence?
- Are there phases that should be split or combined?
- Do phase transitions make sense?

### Step 3: Analyze Process Level

For each process within phases, evaluate:
- Are all necessary processes present?
- Are processes in the right order within the phase?
- Is the right role assigned to each process?
- Are decision points clearly marked?
- Are milestones identified?

### Step 4: Analyze Core Activity Level

For each process, evaluate the core activities:
- Are all necessary core activities listed?
- Are there implicit activities that should be explicit?
- Are activities in logical sequence?
- Are edge cases and exceptions handled?
- **Do all core activities start with action verbs?**
- **Are any names or roles embedded in activity titles?**

### Step 5: Evaluate Cross-Cutting Concerns

**Handoffs**
- Are transitions between phases explicit?
- Is information passed clearly?
- Are there gaps where things could fall through?

**Ownership**
- Is every process assigned to a role?
- Are the right people doing the right things?
- Are there bottlenecks (one role doing too much)?

**Decision Points**
- Are all branches documented?
- Are criteria for decisions clear?
- Are exception paths handled?

### Step 6: Categorize Gaps

**Critical Gaps** — Missing elements that could cause failure
- Missing quality checks
- Skipped approvals or compliance steps
- No error handling

**Efficiency Gaps** — Opportunities to improve speed/cost
- Redundant processes or activities
- Manual tasks that could be automated
- Unnecessary handoffs

**Risk Gaps** — Missing safeguards
- No backup plans
- Missing documentation points
- Unclear escalation paths

**Communication Gaps** — Information flow issues
- Client touchpoints missing
- Internal updates not specified
- Handoff information incomplete

**Measurement Gaps** — Missing tracking/accountability
- No milestones or checkpoints
- No success criteria
- No feedback loops

### Step 7: Prioritize and Recommend

Rank gaps by:
1. **Impact** — How much does this affect outcomes?
2. **Frequency** — How often would this gap cause problems?
3. **Effort** — How hard is it to fix?

Focus recommendations on high-impact, high-frequency issues first.

---

## Output Format

```
# Workflow Gap Analysis: [Workflow Name] Workflow

## Context
- **Industry:** [Industry]
- **Company Type:** [Type]
- **Company Size:** [Size]

## Research Summary
[2-3 sentences on key best practices found for this industry/process]

---

## Phase-Level Gaps

### Gap: [Gap Name]
**Issue:** [What's missing or wrong at the phase level]
**Risk:** [What could go wrong]
**Recommendation:** [Specific fix]

---

## Process-Level Gaps

### Gap: [Gap Name]
**Phase:** [Which phase]
**Issue:** [What process is missing or wrong]
**Risk:** [What could go wrong]
**Recommendation:** [Specific fix]
**Proposed Addition:**
> **Process [X.X]: [Process Name]**
> **Role:** [Role]
>
> **Core Activities:**
> - [Activity 1 — starts with action verb]
> - [Activity 2 — starts with action verb]

---

## Core Activity Gaps

### Gap: [Gap Name]
**Phase:** [Which phase]
**Process:** [Which process]
**Issue:** [What activities are missing]
**Risk:** [What could go wrong]
**Recommendation:** [Specific fix]
**Proposed Activities to Add:**
> - [Core activity 1 — starts with action verb]
> - [Core activity 2 — starts with action verb]

---

## Gap Summary by Category

### Critical Gaps
- [Gap 1]
- [Gap 2]

### Efficiency Gaps
- [Gap 1]

### Risk Gaps
- [Gap 1]

### Communication Gaps
- [Gap 1]

### Measurement Gaps
- [Gap 1]

---

## Enhanced Workflow

[Present the complete workflow with all additions integrated, clearly marking new items with **[NEW]** prefix]

### Phase [N]: [Phase Name]
**Owner:** [Role]

#### Process [N.1]: [Process Name]
**Role:** [Role]

**Core Activities:**
- [Existing activity]
- **[NEW]** [Added activity — starts with action verb]
- [Existing activity]

#### **[NEW]** Process [N.2]: [New Process Name]
**Role:** [Role]

**Core Activities:**
- **[NEW]** [Activity 1 — starts with action verb]
- **[NEW]** [Activity 2 — starts with action verb]
```

---

## Quality Checklist

Before presenting analysis:
- [ ] Research was conducted for this specific industry
- [ ] Gaps identified at all three levels (phase, process, core activity)
- [ ] Every gap has a specific, actionable recommendation
- [ ] Gaps are categorized and prioritized
- [ ] New elements integrate logically into existing workflow
- [ ] Enhanced workflow is complete and uses correct hierarchy
- [ ] Uses "Process" terminology (not "Step")
- [ ] **All proposed core activities start with action verbs**
- [ ] **No personal names in any additions**
- [ ] **No roles embedded in phase/process/activity titles**
- [ ] Workflow title ends with "Workflow"
