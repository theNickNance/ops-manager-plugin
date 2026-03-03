---
name: function-chart-gap-analysis
description: "Analyze a function chart to identify gaps, redundancies, and opportunities for optimization based on industry best practices. Use when (1) User has a function chart and wants to identify improvements, (2) User wants to find missing functions or activities, (3) User asks about redundancies or inefficiencies in their org structure, (4) Following function-chart-architect output to enhance the function chart."
disable-model-invocation: true
argument-hint: "[paste transcript or workflow below]"
---

# Function Chart Gap Analysis

Analyze a business function chart to identify gaps, redundancies, and optimization opportunities.

## Function Chart Hierarchy

1. **Function** — Major business area or department
2. **Subfunction** — Category of work within a function
3. **Core Activity** — Specific task within a subfunction

---

## Failures to Avoid

The following are **critical failures** that invalidate a function chart gap analysis. The AI must avoid these errors.

### Analysis Failures

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| No industry research | Gaps based only on general knowledge | Always search for industry-specific best practices |
| Generic recommendations | "Add more quality activities" | "Add defect tracking subfunction with specific activities" |
| Ignoring company size | Enterprise structure for 5-person company | Scale recommendations to actual business size |
| Missing prioritization | Flat list of gaps | Rank by impact, frequency, and effort |

### Recommendation Failures

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| Personal names in additions | "Add Sarah to do X" | "Add Quality Manager responsibility" |
| Roles in subfunction names | "Manager Review" | "Quality Review" |
| Activities without action verbs | "Customer feedback" | "Collect customer feedback" |
| Vague additions | "Add quality function" | Specify exact subfunctions and activities |

### Core Activity Failures (for proposed additions)

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| Missing action verb | "Budget documentation" | "Document budget allocations" |
| Starting with a noun | "Report generation" | "Generate monthly reports" |
| Role in activity | "QA inspects items" | "Inspect items for defects" |
| Passive voice | "Invoices are processed" | "Process invoices" |

### Structural Failures

| Failure | Why It's Wrong |
|---------|----------------|
| Gaps without location | "Add quality check" with no function/subfunction specified |
| Missing risk assessment | Gap identified without explaining the risk |
| No actionable recommendation | Problem stated but no solution provided |
| Enhanced chart doesn't integrate | New items don't fit logically into existing structure |

### Marker Failures

| Failure | Why It's Wrong |
|---------|----------------|
| Missing [GAP] markers | New items not clearly identified |
| Inconsistent markers | Some gaps marked, others not |
| Wrong marker type | Using [ELIMINATE] when [CONSOLIDATE] is correct |

---

## Analysis Categories

### 1. Gaps (Missing Elements)
Elements that should exist but don't:
- **Missing Functions** — Entire business areas not represented
- **Missing Subfunctions** — Categories of work within a function that are absent
- **Missing Activities** — Specific tasks that best practices suggest should exist

### 2. Redundancies (Duplications)
Work being done in multiple places:
- **Duplicate Activities** — Same task listed under multiple functions
- **Overlapping Subfunctions** — Similar work categories that could be consolidated
- **Role Confusion** — Unclear ownership leading to duplicate effort

### 3. Optimization Opportunities
Areas for improvement:
- **Eliminations** — Activities that don't add value and could be removed
- **Consolidations** — Scattered activities that could be grouped
- **Automations** — Manual activities that could be systematized
- **Reassignments** — Activities in the wrong function

---

## Process

### Step 1: Gather Context

Before analysis, understand:
1. **Industry** — What type of business?
2. **Size** — How many employees? Revenue range?
3. **Growth stage** — Startup, growing, mature?
4. **Pain points** — What problems are they experiencing?

### Step 2: Research Best Practices

Use web search to find:
- Industry-specific organizational structures
- Common functions for this business type
- Best practices for the business size
- Emerging trends in the industry

Search queries:
- "[industry] company organizational structure"
- "[industry] business functions best practices"
- "[industry] operations efficiency"
- "small [industry] company departments"

### Step 3: Gap Analysis

Compare the function chart against:
1. **Industry templates** (see references)
2. **Best practices research**
3. **Logical completeness**

For each function, ask:
- Are all expected subfunctions present?
- Are there activities that should exist but don't?
- Is this function appropriately scoped?

### Step 4: Redundancy Analysis

Look for:
1. **Same activity in multiple places**
   - Is this intentional (legitimate shared work)?
   - Or unclear ownership (wasted effort)?

2. **Similar subfunctions across functions**
   - Could they be consolidated?
   - Is separation justified?

3. **Handoff points**
   - Are there too many handoffs?
   - Could work flow more efficiently?

### Step 5: Optimization Analysis

Identify:
1. **Low-value activities**
   - Does this activity contribute to outcomes?
   - Is it required by regulation/compliance?
   - Could it be eliminated?

2. **Consolidation opportunities**
   - Are related activities scattered?
   - Would grouping improve efficiency?

3. **Automation candidates**
   - Is this activity repetitive?
   - Could technology handle it?

4. **Misplaced activities**
   - Does this activity belong in this function?
   - Would another function be more appropriate?

---

## Output Format

### Gap Analysis Report

```
# Function Chart Gap Analysis
## [Business Name]
Analysis Date: [Date]

---

## Executive Summary
[2-3 sentences summarizing key findings]

---

## Gaps Identified

### Critical Gaps
[Gaps that significantly impact business operations]

1. **[Gap Name]**
   - Type: [Missing Function / Missing Subfunction / Missing Activity]
   - Location: [Where it should be added]
   - Impact: [Why this matters]
   - Recommendation: [Specific addition — activities start with action verbs]

### Efficiency Gaps
[Gaps that affect efficiency but aren't critical]

### Risk Gaps
[Gaps that create compliance or quality risks]

---

## Redundancies Identified

### Duplicate Activities
1. **[Activity Name]**
   - Found in: [Function A], [Function B]
   - Recommendation: [Consolidate to X / Keep separate because Y]

### Overlapping Subfunctions
1. **[Subfunction A] vs [Subfunction B]**
   - Issue: [Description of overlap]
   - Recommendation: [Merge / Clarify boundaries]

---

## Optimization Opportunities

### Potential Eliminations
1. **[Activity Name]**
   - Current location: [Function > Subfunction]
   - Reason to consider elimination: [Rationale]
   - Risk if eliminated: [Assessment]

### Consolidation Candidates
1. **[Activities/Subfunctions]**
   - Currently: [Scattered across X, Y, Z]
   - Proposed: [Consolidated under A]
   - Benefit: [Expected improvement]

### Automation Candidates
1. **[Activity Name]**
   - Current state: [Manual process description]
   - Automation approach: [Suggested solution]

---

## Prioritized Recommendations

### Immediate (0-30 days)
1. [Recommendation]
2. [Recommendation]

### Short-term (30-90 days)
1. [Recommendation]
2. [Recommendation]

### Long-term (90+ days)
1. [Recommendation]
2. [Recommendation]

---

## Enhanced Function Chart

[Include the original function chart with [GAP], [REDUNDANT], and [ELIMINATE] markers]
```

---

## Gap Markers

When marking up the function chart:

- **[GAP]** — New item to add (missing element)
- **[REDUNDANT]** — Duplicate that needs resolution
- **[ELIMINATE]** — Candidate for removal
- **[CONSOLIDATE]** — Should be merged with another item
- **[REASSIGN]** — Belongs in a different function
- **[AUTOMATE]** — Candidate for automation

---

## Common Gaps by Function

### Sales
- Lead scoring/prioritization
- Pipeline reporting
- Win/loss analysis
- Referral program management

### Operations
- Quality control checkpoints
- Safety protocols
- Continuous improvement
- Capacity planning

### Project Management
- Risk management
- Lessons learned capture
- Resource forecasting
- Stakeholder communication plan

### Finance
- Job costing analysis
- Cash flow forecasting
- Budget vs actual tracking
- Financial KPIs

### Administration
- Document management
- Compliance tracking
- Vendor management
- Business continuity planning

---

## Questions to Ask

### Validating Gaps
- "Do you currently do [activity]? If not, has it caused problems?"
- "Who would be responsible for [missing subfunction]?"
- "Is [gap] something you've been meaning to add?"

### Validating Redundancies
- "I see [activity] in both [A] and [B]. Is that intentional?"
- "Who is ultimately responsible for [overlapping area]?"
- "Has unclear ownership caused issues?"

### Validating Eliminations
- "What would happen if you stopped doing [activity]?"
- "Is [activity] required by customers, regulations, or internal policy?"
- "How much time/money does [activity] consume?"

---

## Quality Checklist

Before presenting analysis:
- [ ] Research was conducted for this specific industry
- [ ] Gaps identified at all three levels (function, subfunction, activity)
- [ ] Every gap has a specific, actionable recommendation
- [ ] Gaps are categorized and prioritized
- [ ] New elements integrate logically into existing structure
- [ ] **All proposed core activities start with action verbs**
- [ ] **No personal names in any additions**
- [ ] **No roles embedded in function/subfunction/activity names**
- [ ] All markers are applied consistently

## Deliverables

1. **Gap Analysis Report** — Comprehensive findings document
2. **Enhanced Function Chart** — Original chart with markers showing all identified items
3. **Prioritized Action List** — Recommended changes in priority order
