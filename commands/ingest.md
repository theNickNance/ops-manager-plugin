---
description: "Manually ingest structured JSON into Ops Manager. Use when you have pre-structured output from an individual skill and want to save it to the database."
argument-hint: "[paste JSON or describe what to ingest]"
---

# Manual Ingest

Ingest pre-structured JSON into Ops Manager via the `ingest_json` MCP tool.

## Instructions

1. **Identify the company**: Call `list_companies` to find the target company, or ask the user.

2. **Get the JSON**: The user will provide structured JSON in the standard envelope format:
   ```json
   { "type": "workflow" | "function-chart" | "workflow-gap" | "function-gap", "data": { ... } }
   ```

3. **For gap types**, check if there's a matching workflow or function chart to link to:
   - For `workflow-gap`: Call `list_workflows` to find the workflow ID
   - For `function-gap`: Call `list_function_charts` to find the function chart ID

4. **Ingest**: Call `ingest_json` with the company ID, JSON string, and optional linking IDs.

5. **Report**: Confirm what was saved and provide the dashboard link.

$ARGUMENTS
