---
name: transcript-pipeline
description: "Orchestrate the full ops analysis pipeline from a call transcript. Use when (1) User provides a call transcript to process, (2) User asks to analyze a business process from a conversation, (3) User mentions ops analysis, workflow extraction, or operational mapping, (4) User says 'process this transcript' or 'analyze this call'."
---

# Transcript Pipeline

Process a call transcript through the full Ops Manager analysis pipeline: extract workflows, build function charts, run gap analyses, and ingest everything into the Ops Manager database via MCP tools.

## Prerequisites

Before starting the pipeline, you need:

1. **A company in Ops Manager** — Use the `list_companies` MCP tool to find the right company, or `create_company` to create one if it doesn't exist.
2. **A call transcript** — The raw text of a discovery call, interview, or Q&A session.

## Pipeline Sequence

Execute these steps **in order**. Each step feeds the next.

### Step 1: Extract Workflow

Apply the `workflow-architect` skill knowledge to transform the transcript into a structured workflow with:
- Phases (4-8), each with an owner role
- Processes within each phase, each with a responsible role
- Core activities within each process (every activity starts with an action verb)
- Decision points with branches
- Milestones
- Handoffs between phases
- Trigger event and end state

**Critical rules:**
- Use job titles/roles only — never personal names
- Every core activity starts with an action verb
- Use "Process" terminology, not "Step"

### Step 2: Structure Workflow JSON

Apply the `ops-data-structurer` skill knowledge to convert the workflow into the JSON envelope format:

```json
{
  "type": "workflow",
  "data": {
    "name": "...",
    "description": "...",
    "trigger": "...",
    "endState": "...",
    "keyRoles": ["..."],
    "phases": [...]
  }
}
```

### Step 3: Ingest Workflow

Call the `ingest_json` MCP tool with:
- `companyId`: The company UUID from Step 0
- `json`: The JSON envelope string from Step 2
- `versionLabel`: "Initial Assessment" (or appropriate label)

**Save the returned workflow ID** — you need it for Step 7.

### Step 4: Build Function Chart

Apply the `function-chart-architect` skill knowledge to reorganize the workflow's core activities by role/function rather than by sequence:
- Functions (5-10) representing major business areas
- Subfunctions within each function
- The same core activities from the workflow, now organized by who does them

### Step 5: Structure Function Chart JSON

Apply the `ops-data-structurer` skill knowledge to convert to the JSON envelope:

```json
{
  "type": "function-chart",
  "data": {
    "name": "...",
    "functions": [...]
  }
}
```

### Step 6: Ingest Function Chart

Call the `ingest_json` MCP tool with the function chart envelope.

**Save the returned function chart ID** — you need it for Step 9.

### Step 7: Workflow Gap Analysis

Apply the `workflow-gap-analysis` skill knowledge to analyze the workflow against industry best practices. Research the specific industry. Identify:
- Critical gaps (missing quality checks, approvals, compliance)
- Efficiency gaps (redundant processes, automation candidates)
- Risk gaps (missing safeguards, escalation paths)
- Communication gaps (missing client touchpoints)
- Measurement gaps (missing KPIs, feedback loops)

Include an enhanced workflow with [NEW] items integrated.

### Step 8: Structure + Ingest Workflow Gaps

Structure as a `workflow-gap` envelope and call `ingest_json` with:
- `workflowId`: The workflow ID from Step 3

### Step 9: Function Chart Gap Analysis

Apply the `function-chart-gap-analysis` skill knowledge to analyze the function chart. Identify gaps, redundancies, and optimization opportunities. Mark activities with gap markers (GAP, REDUNDANT, ELIMINATE, CONSOLIDATE, REASSIGN, AUTOMATE).

### Step 10: Structure + Ingest Function Gaps

Structure as a `function-gap` envelope and call `ingest_json` with:
- `functionChartId`: The function chart ID from Step 6

## Completion

After all steps complete, summarize:
- Workflow name and phase count
- Function chart name and function count
- Number of gap findings (workflow + function)
- Link to view results: `https://ops-map-wine.vercel.app/dashboard/companies/{companyId}/workflows`

## Error Handling

If any step fails:
1. Report which step succeeded and which failed
2. Include the error message
3. The user can re-run individual steps using the specific skills and `ingest_json` tool

## Important Notes

- The `ingest_json` tool accepts the standard `{ "type": "...", "data": { ... } }` envelope
- All workflow data uses roles/job titles — never personal names
- Every core activity must start with an action verb
- The pipeline typically takes 2-3 minutes for a standard transcript
