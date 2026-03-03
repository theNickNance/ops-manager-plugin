---
name: ops-data-structurer
description: "Convert any ops-manager skill output (workflow-architect, function-chart-architect, workflow-gap-analysis, function-chart-gap-analysis) into structured JSON for database ingestion. Use when (1) You have text output from any of the four ops skills and need JSON, (2) Preparing data for the Ops Manager ingest page, (3) User says 'structure this' or 'convert to JSON' with skill output."
disable-model-invocation: true
argument-hint: "[paste skill output below]"
---

# Ops Data Structurer

Convert the text output from any of the four ops-manager skills into structured JSON that can be directly ingested by the Ops Manager web app.

## Auto-Detection

Determine which skill produced the input by looking for these signals:

| Type | Key Signals |
|------|-------------|
| `workflow` | Phase/Process/Core Activity hierarchy, trigger events, end states, handoffs |
| `function-chart` | Functions/Subfunctions/Core Activities organized by role |
| `workflow-gap` | Gap findings referencing workflow phases/processes, may include enhanced workflow |
| `function-gap` | Gap findings referencing functions/subfunctions, may include enhanced function chart |

## Output Contract

You MUST output ONLY a single JSON code block — no explanation, no commentary, no markdown outside the code block.

The JSON envelope is:
```
{ "type": "<type>", "data": { ... } }
```

Where `type` is one of: `workflow`, `function-chart`, `workflow-gap`, `function-gap`.

---

## JSON Schemas

### Type: `workflow`

```typescript
{
  "type": "workflow",
  "data": {
    "name": string,                    // Workflow name
    "description": string | null,
    "trigger": string | null,          // What starts this workflow
    "endState": string | null,         // What the completed state looks like
    "keyRoles": string[],              // Job titles only, never personal names
    "phases": [
      {
        "name": string,               // Phase name
        "number": number,             // Sequential phase number (1-based)
        "ownerRole": string | null,   // Job title of phase owner
        "processes": [
          {
            "name": string,
            "number": number,         // Sequential within phase (1-based)
            "role": string | null,    // Job title responsible
            "activities": [
              {
                "text": string,
                "type": "standard" | "milestone" | "decision" | "gap",
                "decisionBranches": [  // Only for type "decision"
                  { "condition": string, "outcome": string }
                ] | undefined,
                "isNew": boolean | undefined  // true if added by gap analysis
              }
            ],
            "isGap": boolean | undefined
          }
        ],
        "exitPoints": string[],       // Conditions to move to next phase
        "handoff": {                   // Optional transition to next phase
          "fromRole": string | null,
          "toRole": string | null,
          "context": string
        } | undefined,
        "isGap": boolean | undefined
      }
    ]
  }
}
```

**Example (compact):**
```json
{
  "type": "workflow",
  "data": {
    "name": "Tenant Move-In",
    "description": "End-to-end process for onboarding new tenants",
    "trigger": "Signed lease received",
    "endState": "Tenant occupying unit with all systems active",
    "keyRoles": ["Property Manager", "Maintenance Coordinator", "Leasing Agent"],
    "phases": [
      {
        "name": "Lease Execution",
        "number": 1,
        "ownerRole": "Leasing Agent",
        "processes": [
          {
            "name": "Document Collection",
            "number": 1,
            "role": "Leasing Agent",
            "activities": [
              { "text": "Collect signed lease and deposit", "type": "standard" },
              { "text": "All documents received and verified", "type": "milestone" }
            ]
          }
        ],
        "exitPoints": ["All lease documents executed and filed"],
        "handoff": {
          "fromRole": "Leasing Agent",
          "toRole": "Property Manager",
          "context": "Signed lease package with move-in date"
        }
      }
    ]
  }
}
```

### Type: `function-chart`

```typescript
{
  "type": "function-chart",
  "data": {
    "name": string,                    // Chart name
    "functions": [
      {
        "name": string,               // Function/department name
        "ownerRole": string | null,   // Job title
        "subfunctions": [
          {
            "name": string,
            "activities": [
              {
                "text": string,
                "gapMarker": string | undefined  // "GAP", "REDUNDANT", "ELIMINATE", "CONSOLIDATE", "REASSIGN", "AUTOMATE"
              }
            ],
            "isGap": boolean | undefined
          }
        ]
      }
    ]
  }
}
```

**Example (compact):**
```json
{
  "type": "function-chart",
  "data": {
    "name": "Property Management Functions",
    "functions": [
      {
        "name": "Tenant Relations",
        "ownerRole": "Property Manager",
        "subfunctions": [
          {
            "name": "Lease Administration",
            "activities": [
              { "text": "Process lease renewals and amendments" },
              { "text": "Track lease expiration dates" }
            ]
          }
        ]
      }
    ]
  }
}
```

### Type: `workflow-gap`

```typescript
{
  "type": "workflow-gap",
  "data": {
    "findings": [
      {
        "name": string,                       // Finding title
        "category": string | null,            // e.g., "process", "communication", "technology"
        "findingType": string | null,         // e.g., "gap", "redundancy", "risk"
        "sourceView": "workflow",             // Always "workflow" for this type
        "locationPhase": string | undefined,  // Phase where gap was found
        "locationProcess": string | undefined,
        "issue": string | null,
        "risk": string | null,
        "recommendation": string | null,
        "priority": string | undefined        // "high", "medium", "low"
      }
    ],
    "enhancedWorkflow": <ParsedWorkflow> | null  // Same shape as workflow data above, with gaps marked
  }
}
```

**Example (compact):**
```json
{
  "type": "workflow-gap",
  "data": {
    "findings": [
      {
        "name": "Missing Quality Check",
        "category": "process",
        "findingType": "gap",
        "sourceView": "workflow",
        "locationPhase": "Unit Preparation",
        "locationProcess": "Maintenance Inspection",
        "issue": "No formal quality verification after maintenance work",
        "risk": "Tenant complaints about incomplete repairs",
        "recommendation": "Add quality inspection step with checklist",
        "priority": "high"
      }
    ],
    "enhancedWorkflow": null
  }
}
```

### Type: `function-gap`

```typescript
{
  "type": "function-gap",
  "data": {
    "findings": [
      {
        "name": string,
        "category": string | null,
        "findingType": string | null,
        "sourceView": "function",                  // Always "function" for this type
        "locationFunction": string | undefined,
        "locationSubfunction": string | undefined,
        "issue": string | null,
        "risk": string | null,
        "recommendation": string | null,
        "priority": string | undefined
      }
    ],
    "enhancedFunctionChart": <ParsedFunctionChart> | null  // Same shape as function-chart data above
  }
}
```

## Rules

1. **Job titles only** — Never include personal names. Use role titles (e.g., "Property Manager", not "John").
2. **Preserve all data** — Every phase, process, activity, finding in the input must appear in the output. Do not summarize or omit.
3. **Sequential numbering** — Phase numbers and process numbers must be sequential starting from 1.
4. **Activity types** — Default to `"standard"`. Use `"milestone"` for completion markers, `"decision"` for branching points (include `decisionBranches`), `"gap"` for gap-identified activities.
5. **Gap markers** — In gap analysis outputs, mark new items with `"isGap": true` or `"isNew": true` as appropriate.
6. **Null vs undefined** — Use `null` for fields that exist but have no value. Omit optional fields entirely if not applicable.
7. **Output ONLY the JSON code block** — No preamble, no explanation, no follow-up text.
