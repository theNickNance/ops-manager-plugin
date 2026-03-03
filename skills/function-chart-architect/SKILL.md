---
name: function-chart-architect
description: "Transform workflow documentation into a structured function chart by reorganizing activities by role/function rather than by sequence. Use when (1) User has a completed workflow and wants to create a function chart, (2) User wants to see their business organized by function/department, (3) User asks to map roles and responsibilities, (4) Following workflow-architect output to create the complementary function view."
disable-model-invocation: true
argument-hint: "[paste transcript or workflow below]"
---

# Function Chart Architect

Transform a workflow into a function chart by reorganizing core activities from sequential order to functional/role-based organization.

## Relationship to Workflow

The **workflow** and **function chart** are two views of the same information:

| View | Organization | Purpose |
|------|--------------|---------|
| Workflow | By sequence (Phase → Process → Activity) | Shows WHEN things happen |
| Function Chart | By role (Function → Subfunction → Activity) | Shows WHO does what |

The **core activities are identical** in both views—they're just organized differently.

## Function Chart Hierarchy

1. **Function** — Major business area or department (e.g., Sales, Operations, Finance)
2. **Subfunction** — Category of work within a function (e.g., Lead Management, Estimating)
3. **Core Activity** — Specific task (same activities from workflow, reorganized)

---

## Failures to Avoid

The following are **critical failures** that invalidate a function chart. The AI must avoid these errors.

### Naming Failures

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| Personal names anywhere | "Sarah's Responsibilities" | "Account Executive" as function |
| Person-named functions | "John's Team" | "Sales" or "Operations" |
| Vague function names | "Other Stuff" | "Administrative Support" |
| Role as function name | "The Manager's Work" | Name the business area |

### Core Activity Failures

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| Missing action verb | "Client information" | "Collect client information" |
| Starting with a noun | "Proposal to client" | "Send proposal to client" |
| Role in activity | "Manager reviews budget" | "Review budget for accuracy" |
| Name in activity | "Sarah calls client" | "Call client to confirm details" |
| Passive voice | "Documents are reviewed" | "Review documents" |

**Every core activity must start with an action verb.**

### Subfunction Failures

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| Role in subfunction name | "Manager Tasks" | "Budget Oversight" |
| Too broad | "Everything Else" | Split into specific subfunctions |
| Single activity | Subfunction with 1 activity | Combine with related subfunction |
| 20+ activities | Subfunction too large | Split into multiple subfunctions |

### Structure Failures

| Failure | Why It's Wrong |
|---------|----------------|
| Missing function owner | Every function needs assigned ownership |
| Orphaned activities | Activities from workflow not in any subfunction |
| Duplicate activities without justification | Same activity in multiple places needs explanation |
| 15+ functions | Too many — consolidate related areas |
| Single subfunction per function | Function is too granular |

### Hierarchy Failures

| Failure | Why It's Wrong |
|---------|----------------|
| Mixing levels | Activities placed directly under functions |
| Skipping subfunctions | Going from function to activities |
| Inconsistent depth | Some functions have 5 subfunctions, others have 1 |

---

## Input Requirements

To build a function chart, you need:
1. A completed workflow with phases, processes, and core activities
2. Clear ownership assignments for each phase/process
3. Understanding of the business structure

## Process

### Step 1: Extract All Core Activities

From the workflow, list every core activity along with:
- The phase and process it belongs to
- The owner (role/team) assigned

### Step 2: Identify Functions

Functions are the major business areas. Common functions include:

**Client-Facing:**
- Sales
- Marketing
- Customer Service/Support
- Account Management

**Delivery:**
- Operations/Production
- Project Management
- Design/Engineering
- Quality Assurance

**Back Office:**
- Finance/Accounting
- Administration
- Human Resources
- IT/Technology

Ask: "What are the major functional areas in this business?"

### Step 3: Define Subfunctions

For each function, group related activities into subfunctions. Subfunctions should:
- Be logical groupings of related work
- Typically contain 3-15 core activities each
- Have clear, descriptive names (no roles or personal names)
- Not overlap significantly with other subfunctions

**Example for Sales Function:**
- Lead Management
- Customer Qualification
- Appointment Scheduling
- Site Assessment
- Estimating/Pricing
- Proposal Development
- Contract Management
- Handoff to Operations

### Step 4: Map Core Activities

Place each core activity under the appropriate subfunction. Consider:
- WHO performs this activity (determines function)
- WHAT type of work is it (determines subfunction)
- Activities may appear in multiple subfunctions if legitimately performed by different roles

**Remember:** Each core activity must start with an action verb.

### Step 5: Validate Completeness

Check that:
- [ ] Every workflow activity appears in at least one subfunction
- [ ] No orphaned activities
- [ ] Subfunctions are balanced (not too large or too small)
- [ ] Function assignments match actual business structure
- [ ] **All core activities start with action verbs**
- [ ] **No personal names anywhere**
- [ ] **No roles embedded in function/subfunction/activity names**

---

## Output Format

```
# [Business Name] Function Chart

## Function: [Function Name]
Owner: [Role/Department]

### Subfunction: [Subfunction Name]
- [Core Activity 1 — starts with action verb]
- [Core Activity 2 — starts with action verb]
- [Core Activity 3 — starts with action verb]

### Subfunction: [Subfunction Name]
- [Core Activity 1]
- [Core Activity 2]

---

## Function: [Function Name]
Owner: [Role/Department]

### Subfunction: [Subfunction Name]
- [Core Activity 1]
- [Core Activity 2]
```

---

## Discovery Questions

If building from scratch (not from an existing workflow), ask:

### Business Structure
1. What are the main departments or functional areas in your business?
2. Who are the key roles and what do they do?
3. How is work divided between sales and operations?

### For Each Function
1. What are the main categories of work in [function]?
2. What specific tasks fall under each category?
3. Who is responsible for each area?

### Validation
1. Are there any activities that span multiple functions?
2. Are there any gaps—work that gets done but isn't clearly assigned?
3. Does this organization match how you actually operate?

---

## Common Patterns by Industry

### Construction/Contracting
- **Sales**: Lead management, estimating, proposals, contracts
- **Design**: Plans, specifications, selections, permits
- **Operations**: Scheduling, procurement, field work, quality
- **Project Management**: Coordination, communication, documentation
- **Finance**: Invoicing, payments, job costing
- **Admin**: HR, office management, compliance

### Professional Services
- **Business Development**: Marketing, proposals, networking
- **Client Services**: Onboarding, delivery, support
- **Operations**: Resource planning, quality, methodology
- **Finance**: Billing, collections, reporting

---

## Tips

1. **Start with the workflow** — It's easier to reorganize existing activities than to create from scratch
2. **Match reality** — The function chart should reflect how the business actually operates, not an idealized structure
3. **Keep it practical** — 5-10 functions is typical; more than 12 becomes unwieldy
4. **Balance subfunctions** — Aim for similar granularity across all functions
5. **Document ownership** — Every function should have a clear owner

---

## Quality Checklist

Before presenting function chart:
- [ ] **All core activities start with action verbs**
- [ ] **No personal names appear anywhere**
- [ ] **No roles embedded in function/subfunction/activity titles**
- [ ] All workflow activities are accounted for
- [ ] Functions represent major business areas (5-10 typical)
- [ ] Subfunctions are balanced (3-15 activities each)
- [ ] Every function has an owner assigned
- [ ] Duplicate activities are justified or consolidated
- [ ] Structure matches how business actually operates

## Deliverable

A structured text document containing:
1. List of all functions with owners
2. Subfunctions within each function
3. Core activities mapped to each subfunction
4. Notes on any activities that span multiple functions
