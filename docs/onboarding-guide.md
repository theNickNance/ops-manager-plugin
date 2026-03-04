# Ops Map — Consultant Onboarding Guide

Welcome to Ops Map. This guide gets you from zero to processing your first client transcript in about 10 minutes.

---

## What Is Ops Map?

Ops Map is a platform that turns raw client discovery call transcripts into structured, visual operational analysis. Instead of delivering findings as PDFs or static documents, you deliver an interactive web app your clients can explore.

Here's what happens end-to-end:

```
You have a discovery call with a client
        ↓
Paste the transcript into Claude Cowork
        ↓
The Ops Manager plugin automatically:
  1. Extracts a structured workflow (phases, processes, activities)
  2. Builds a function chart (same activities, organized by role)
  3. Runs gap analyses on both views
  4. Saves everything to the Ops Map database
        ↓
You and your client view the results at ops-map-wine.vercel.app
```

No manual data entry. No copy-paste. The AI does the heavy lifting; you review and refine.

---

## Step 1: Get Access

You need two things:

### A. An Ops Map Account

Your admin will create an account for you via Google OAuth. Once set up:

1. Go to [ops-map-wine.vercel.app](https://ops-map-wine.vercel.app)
2. Click **Sign in with Google**
3. Use the Google account your admin registered

Admin users land on the **Dashboard** — this is your home base for managing companies and viewing analysis results.

### B. A Claude Subscription

You need a Claude Pro, Team, or Enterprise subscription to use Claude Cowork. Sign up at [claude.ai](https://claude.ai) if you don't have one.

---

## Step 2: Install Claude Cowork

Claude Cowork is Anthropic's desktop app that gives Claude access to files, folders, and external services on your machine. It's where you'll process transcripts.

1. Download Claude Cowork from [claude.ai](https://claude.ai) (available on macOS and Windows)
2. Install and sign in with your Claude account
3. That's it — Cowork is ready

> **What makes Cowork different from claude.ai?** Cowork can interact with files on your computer and connect to external services (like Ops Map) via plugins. The web version can't do either.

---

## Step 3: Install the Ops Manager Plugin

The plugin gives Claude the skills to analyze transcripts and the MCP connection to save results to Ops Map.

### Installation

1. Download the plugin: [ops-manager-plugin.zip](https://github.com/theNickNance/ops-manager-plugin/releases/latest/download/ops-manager-plugin.zip)
2. Open Claude Cowork
3. Go to **Settings → Plugins**
4. Upload the zip file

### First-Time MCP Authentication

The first time the plugin connects to Ops Map, you'll need to authenticate:

1. Claude will prompt you to authorize the Ops Manager MCP connection
2. You'll be redirected to the Ops Map login page (Google OAuth)
3. Sign in with the same Google account from Step 1
4. Grant access — this creates a secure token so Claude can read/write data on your behalf

> **This only happens once.** After the initial auth, the plugin uses refresh tokens to stay connected. If your session expires, you'll be prompted to re-authenticate.

### What the Plugin Includes

- **2 Commands** you can run directly:
  - `/ops-manager:process-transcript` — Full pipeline (transcript → analysis → database)
  - `/ops-manager:ingest` — Manual ingest of pre-structured JSON

- **7 AI Skills** that Claude uses automatically when relevant:
  - `getting-started` — Welcomes new users and walks through setup
  - `transcript-pipeline` — Orchestrates the full analysis
  - `workflow-architect` — Extracts workflows from transcripts
  - `function-chart-architect` — Builds function charts from workflows
  - `workflow-gap-analysis` — Identifies workflow gaps
  - `function-chart-gap-analysis` — Identifies function chart gaps
  - `ops-data-structurer` — Converts output to structured JSON

- **MCP Tools** for reading/writing data directly to Ops Map

---

## Step 4: Process Your First Transcript

This is the main workflow you'll use after every discovery call.

### 4a. Prepare Your Transcript

Get your call transcript ready. This can be:
- A text file from your transcription service (Otter, Fireflies, etc.)
- Raw text copied from a recording tool
- Notes you've typed up from a call

The more complete the transcript, the better the analysis. The AI is looking for:
- How work flows through the organization (phases, handoffs)
- Who does what (roles, responsibilities)
- Pain points, bottlenecks, and gaps mentioned in conversation

### 4b. Run the Pipeline

In Claude Cowork, run:

```
/ops-manager:process-transcript
```

Then either:
- **Paste the transcript** directly into the conversation, or
- **Reference a file** on your machine that Cowork can access

Claude will ask for a **company name** (and URL slug if it's a new company). Then the pipeline runs:

| Step | What Happens | Time |
|------|-------------|------|
| 1 | Find or create the company in Ops Map | ~5s |
| 2 | Extract structured workflow from transcript | ~30s |
| 3 | Ingest workflow into database | ~5s |
| 4 | Build function chart from workflow | ~30s |
| 5 | Ingest function chart into database | ~5s |
| 6 | Run workflow gap analysis | ~30s |
| 7 | Ingest workflow gaps | ~5s |
| 8 | Run function chart gap analysis | ~30s |
| 9 | Ingest function chart gaps | ~5s |

**Total: ~2-3 minutes** for a standard transcript.

### 4c. Review the Output

When the pipeline finishes, Claude will summarize what was created and give you a direct link to the dashboard. You can also navigate there manually:

1. Go to [ops-map-wine.vercel.app/dashboard](https://ops-map-wine.vercel.app/dashboard)
2. Click on the company
3. Explore the tabs:

| Tab | What You'll See |
|-----|----------------|
| **Workflows** | Vertical phase cards showing the sequence of operations — trigger event through end state |
| **Functions** | Horizontal carousel of function columns organized by role |
| **People** | Mapping of roles to actual people at the company |

### 4d. Check the Gap Analysis

Gap findings appear as **colored dots** on workflow phases/processes and function chart activities:

- 🔴 **Red dot** = High priority finding
- 🟡 **Amber dot** = Medium priority finding
- ⚪ **Gray dot** = Low priority finding

Click any dot to see the full finding: what the issue is, what the risk is, and what the recommendation is.

On the function chart, you'll also see **gap markers** on individual activities:

| Marker | Meaning |
|--------|---------|
| GAP | Missing capability that should exist |
| REDUNDANT | Duplicated across roles |
| ELIMINATE | Should be removed |
| CONSOLIDATE | Should be merged with another activity |
| REASSIGN | Currently owned by the wrong role |
| AUTOMATE | Candidate for automation |

---

## Step 5: Share with Your Client

Once you've reviewed and are happy with the analysis:

### Invite the Client

Client users get **read-only access** scoped to their company. To add a client user:

1. In Claude Cowork, ask Claude to add a client user:
   ```
   Add john@clientcompany.com as a client user for [Company Name]
   ```
2. Claude will use the `add_company_user` MCP tool to create the association
3. The client signs in with Google OAuth at [ops-map-wine.vercel.app](https://ops-map-wine.vercel.app)
4. They're automatically routed to their company's read-only portal

### What Clients See

Clients see the same workflow, function chart, and gap analysis views — but read-only. No dashboard access, no data ingestion, no other companies. Just their operational analysis.

---

## Day-to-Day Usage

### Processing a New Client

```
/ops-manager:process-transcript [paste transcript or provide file]
```

That's it. One command, 2-3 minutes, full analysis in the database.

### Updating an Existing Analysis

Run the pipeline again for the same company. Workflows and function charts are versioned by date, so you'll create a new version rather than overwriting the original.

### Manually Ingesting Data

If you've run individual skills outside the plugin and have structured JSON ready:

```
/ops-manager:ingest [paste JSON]
```

The JSON should be in the standard envelope format:
```json
{
  "type": "workflow",
  "data": { ... }
}
```

Valid types: `workflow`, `function-chart`, `workflow-gap`, `function-gap`

### Asking Claude About Your Data

Because the MCP connection is live, you can ask Claude conversational questions about your data:

- *"What companies do I have in Ops Map?"*
- *"Show me the workflows for Acme Corp"*
- *"What are the high-priority gap findings for Byrd Building?"*
- *"How many functions does the Acme Corp function chart have?"*

Claude will use the MCP read tools (`list_companies`, `get_workflow`, `list_gap_findings`, etc.) to fetch live data and answer.

### Managing People

Map abstract roles to real humans:

- *"Add Rick Smith as Owner/Principal for Byrd Building"*
- *"Update Reed's role to Co-Owner for Byrd Building"*

---

## Troubleshooting

### "MCP connection failed" or "Authentication required"

The OAuth token may have expired. Claude will prompt you to re-authenticate — just follow the Google OAuth flow again.

### Pipeline fails partway through

Claude will report which step succeeded and which failed. You can:
1. Fix the issue (usually a transcript quality problem)
2. Re-run the full pipeline, or
3. Use `/ops-manager:ingest` to manually ingest the remaining pieces

### Data looks wrong in the dashboard

The AI extracts structure from natural conversation, so it can occasionally misinterpret things. You have two options:
- **Re-run the pipeline** with a cleaner transcript or additional context
- **Manually ingest corrected JSON** via the dashboard's Ingest tab or the `/ops-manager:ingest` command

### Can't see a company in the dashboard

Make sure you're logged in with an admin account. Client users only see their assigned company at `/client/{slug}`.

---

## Quick Reference

| Action | How |
|--------|-----|
| Process a transcript | `/ops-manager:process-transcript` in Cowork |
| Manually ingest JSON | `/ops-manager:ingest` in Cowork |
| View dashboard | [ops-map-wine.vercel.app/dashboard](https://ops-map-wine.vercel.app/dashboard) |
| Add a client user | Ask Claude: *"Add email@company.com as a client user for [Company]"* |
| Add a person/role | Ask Claude: *"Add [Name] as [Role] for [Company]"* |
| Check gap findings | Click colored dots on any workflow phase or function chart activity |
| Query your data | Ask Claude anything — it reads live from Ops Map via MCP |

---

## Architecture (For the Curious)

You don't need to know this to use Ops Map, but if you're interested:

- **Ops Map** is a Next.js app hosted on Vercel with a Supabase (PostgreSQL) database
- **The MCP server** is embedded in the app at `/api/mcp` — it's how Claude reads and writes data
- **OAuth 2.0 with PKCE** secures the MCP connection — your Google identity is used to scope database access
- **The plugin** packages 6 AI skills (domain knowledge) + 2 commands (entry points) + the MCP connection config
- **Skills** tell Claude *how* to analyze transcripts; **MCP tools** tell Claude *how* to save the results

```
Claude Cowork
  ├── Plugin (skills + commands + MCP config)
  │     ├── Skills → Claude knows HOW to analyze
  │     └── MCP config → Claude knows WHERE to save
  │
  └── MCP Server (ops-map-wine.vercel.app/api/mcp)
        ├── OAuth 2.0 → Secure identity
        ├── Read tools → Query existing data
        └── Write tools → Ingest analysis results
```
