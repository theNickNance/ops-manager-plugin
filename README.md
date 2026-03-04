# Ops Manager Plugin

A Claude Cowork / Claude Code plugin that transforms call transcripts into structured operational analysis and ingests them into the [Ops Manager](https://ops-map-wine.vercel.app) platform.

## What It Does

Drop a call transcript into Claude and this plugin will:

1. **Extract a structured workflow** — phases, processes, core activities, handoffs
2. **Build a function chart** — the same activities reorganized by role
3. **Run gap analyses** — identify missing processes, redundancies, optimization opportunities
4. **Ingest everything** into Ops Manager's database via MCP

No manual copy-paste. No technical setup beyond installing the plugin.

## Installation

### Claude Code
```bash
claude plugins add /path/to/ops-manager-plugin
```

### Cowork
Install via Settings > Plugins, or load with `--plugin-dir`:
```bash
claude --plugin-dir ./ops-manager-plugin
```

## Usage

### Full Pipeline
```
/ops-manager:process-transcript [paste transcript]
```

### Manual Ingest
```
/ops-manager:ingest [paste structured JSON]
```

### First Time?

Just say hello. The plugin will walk you through authentication, show you what it can do, and get you ready to process your first transcript. No manual required.

For a deeper dive, see the [full onboarding guide](docs/onboarding-guide.md).

### Skills (Auto-Invoked)

The plugin includes domain skills that Claude uses automatically when relevant:

- **getting-started** — Welcomes new users and walks through setup and first use
- **transcript-pipeline** — Orchestrates the full analysis pipeline
- **workflow-architect** — Extracts workflows from transcripts
- **function-chart-architect** — Builds function charts from workflows
- **workflow-gap-analysis** — Identifies workflow gaps
- **function-chart-gap-analysis** — Identifies function chart gaps
- **ops-data-structurer** — Converts skill output to structured JSON

## MCP Tools

The plugin connects to the Ops Manager MCP server, providing these tools:

**Read:** `list_companies`, `get_company`, `list_workflows`, `get_workflow`, `list_function_charts`, `get_function_chart`, `list_gap_findings`, `list_people`

**Write:** `create_company`, `ingest_json`, `ingest_workflow`, `ingest_function_chart`, `ingest_workflow_gaps`, `ingest_function_gaps`, `add_person`, `update_person`, `add_company_user`

## Requirements

- Claude Pro, Team, or Enterprise subscription
- Ops Manager instance with MCP server deployed
