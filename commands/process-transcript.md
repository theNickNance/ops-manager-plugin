---
description: "Process a call transcript through the full Ops Manager pipeline: workflow extraction, function chart, gap analyses, and database ingestion."
argument-hint: "[paste transcript or provide company name]"
---

# Process Transcript

You are running the full Ops Manager transcript processing pipeline.

## Input

The user will provide:
1. A call transcript (pasted text, file, or reference)
2. A company name (to look up or create in Ops Manager)

## Instructions

1. **Find or create the company**: Call `list_companies` to find the company. If it doesn't exist, ask the user for the company name and a URL slug, then call `create_company`.

2. **Run the full pipeline** using the `transcript-pipeline` skill knowledge — all 10 steps in order:
   - Extract workflow from transcript
   - Structure as JSON and ingest via `ingest_json` MCP tool
   - Build function chart from the workflow
   - Structure as JSON and ingest via `ingest_json` MCP tool
   - Run workflow gap analysis
   - Structure as JSON and ingest via `ingest_json` MCP tool (with workflowId)
   - Run function chart gap analysis
   - Structure as JSON and ingest via `ingest_json` MCP tool (with functionChartId)

3. **Report results**: Summarize what was created and provide the dashboard link.

$ARGUMENTS
