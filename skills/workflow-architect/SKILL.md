---
name: workflow-architect
description: "Transform interviews, transcripts, or Q&A sessions into structured text-based workflow documentation. Use when (1) Processing a meeting transcript to extract a business process, (2) Documenting how a team or company operates, (3) Converting verbal process descriptions into structured workflows, (4) Creating initial workflow drafts from stakeholder interviews, (5) User mentions workflow, process documentation, how we do things, or provides a transcript to document."
disable-model-invocation: true
argument-hint: "[paste transcript or workflow below]"
---

# Workflow Architect

Transform unstructured input (transcripts, interviews, Q&A) into structured text-based workflow documentation.

## Workflow Hierarchy

All workflows use this three-level structure:

1. **Phase** — Major stage of the process (4-8 typical)
2. **Process** — Key action or milestone within a phase
3. **Core Activity** — Granular task within a process

This hierarchy aligns with function charts where Core Activities are the same items organized by role rather than sequence.

---

## Failures to Avoid

The following are **critical failures** that invalidate a workflow. The AI must avoid these errors.

### Naming Failures

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| Personal names anywhere | "Sarah sends the proposal" | "Account Executive sends the proposal" |
| Roles in phase/process titles | "Sales Team Qualification" | "Lead Qualification" |
| Person-named workflows | "John's Sales Process" | "Sales Process" |
| Vague process names | "Handle the thing" | "Process Change Order Request" |

### Core Activity Failures

| Failure | Why It's Wrong | Correct Approach |
|---------|----------------|------------------|
| Missing action verb | "Client information" | "Collect client information" |
| Starting with a noun | "Proposal to client" | "Send proposal to client" |
| Role in activity title | "Manager reviews doc" | "Review document for accuracy" |
| Passive voice | "Documents are reviewed" | "Review documents" |

**Valid action verbs for core activities:** Schedule, Send, Review, Create, Update, Verify, Document, Confirm, Prepare, Complete, Submit, Approve, Notify, Assign, Track, Record, Calculate, Generate, Process, Coordinate, Collect, Analyze, Deliver

### Structure Failures

| Failure | Why It's Wrong |
|---------|----------------|
| No trigger defined | Workflow has no clear starting point |
| No end state defined | Workflow has no clear completion criteria |
| Activities without owners | Unclear who is responsible |
| Missing decision branches | Process variations not documented |
| Phases with only 1-2 processes | Phase is too granular, should be combined |
| 15+ processes in a phase | Phase is too broad, should be split |

### Hierarchy Failures

| Failure | Why It's Wrong |
|---------|----------------|
| Mixing levels | Core activities described at phase level |
| Skipping levels | Going from phase directly to core activities |
| Using "step" terminology | Must use "process" as the middle tier |
| Inconsistent depth | Some phases have 2 levels, others have 3 |

---

## Critical Rule: No Personal Names

**All workflows must use job titles and roles — never personal names.**

This applies to:
- Workflow titles (name after the process, not a person)
- Phase owners
- Process owners
- Any reference to who does what

### Name-to-Role Conversion

When processing transcripts or interviews, convert all personal names to their job title or functional role:

| In the transcript | In the workflow |
|-------------------|-----------------|
| "Sarah sends the proposal" | "Account Executive sends the proposal" |
| "Then Mike measures the space" | "Field Technician measures the space" |
| "Janet approves it" | "Operations Manager approves it" |
| "I hand it off to Tom" | "Sales hands off to Production Manager" |

**If a role is unclear from context:**
1. First, check if the transcript mentions their title anywhere
2. If not, infer from their responsibilities (person doing estimates = Estimator, person managing projects = Project Manager)
3. If still unclear, use a functional description: "Team member responsible for [function]"
4. Flag it in Notes & Assumptions for the user to clarify

### Workflow Naming Convention

Name workflows after the **process being documented**, not people or departments:

| Wrong | Right |
|-------|-------|
| "John's Sales Process" | "Sales Process" |
| "Marketing Team Workflow" | "Lead Generation Process" |
| "Sarah's Onboarding" | "Client Onboarding Process" |

Good workflow names describe what gets accomplished:
- "Residential Project Delivery Workflow"
- "Inbound Lead Qualification Workflow"
- "Change Order Management Workflow"
- "New Employee Onboarding Workflow"

---

## Core Activity Rules

Every core activity **must** follow these rules:

### 1. Start with an Action Verb

**Wrong:**
- Client contact information
- The proposal document
- Budget review

**Right:**
- Collect client contact information
- Create proposal document
- Review budget for accuracy

### 2. No Names or Roles in the Activity Title

The activity title describes WHAT is done, not WHO does it. The owner is specified separately.

**Wrong:**
- Manager approves budget
- Sarah calls the client
- Sales team qualifies lead

**Right:**
- Approve budget
- Call client to confirm appointment
- Qualify lead against criteria

### 3. Be Specific and Actionable

**Wrong:**
- Handle paperwork
- Deal with issues
- Do the thing

**Right:**
- Complete permit application
- Resolve customer complaint
- Process payment

---

## Input Types

1. **Transcript** — Recording of a conversation describing how work gets done
2. **Interview notes** — Written notes from a process discovery session
3. **Q&A responses** — Answers to workflow discovery questions
4. **Verbal description** — User explaining their process in chat

## Workflow Process

### Step 1: Identify the Process Scope

Determine what process is being documented:
- What is the start trigger? (lead comes in, order placed, project kicks off)
- What is the end state? (deal closed, project complete, customer satisfied)
- Who are the key roles involved?

If unclear from input, ask: "What process are we documenting, and where does it start and end?"

### Step 2: Build a Role Map

Before extracting content, identify all people mentioned and map them to roles:

1. List every name mentioned in the input
2. Identify their job title or function from context
3. Create a reference map for consistent role naming throughout the workflow

Example role map:
```
Sarah → Account Executive
Mike → Field Technician
Janet → Operations Manager
Tom → Production Manager
"The guys in the shop" → Production Team
```

If you cannot determine a role, note it for clarification but continue with a functional placeholder.

### Step 3: Extract Raw Content

Read through input and extract every action, decision, or handoff mentioned. Capture:
- Actions ("we send a proposal", "they measure the space")
- Decisions ("if they approve", "depending on budget")
- Handoffs ("then it goes to production", "designer takes over")
- Timing ("takes about 2 weeks", "same day")

**As you extract, immediately convert names to roles using your role map.**

Don't organize yet — just capture everything mentioned.

### Step 4: Identify Phases

Group extracted content into 4-8 logical phases. Common patterns:

**Sales/Service businesses:** Lead → Qualification → Discovery → Proposal → Close → Delivery → Follow-up

**Project-based businesses:** Initiation → Planning → Execution → Monitoring → Closeout

**Manufacturing/Production:** Order → Design → Procurement → Production → QC → Delivery

Name phases using the business's own language when possible.

### Step 5: Define Processes Within Phases

For each phase, identify the major processes (typically 3-8 per phase). Processes are significant actions or milestones, not granular tasks.

Examples of processes within a "Sales" phase:
- Initial Contact
- Qualification Call
- Site Visit
- Proposal Development
- Proposal Presentation
- Contract Signing

### Step 6: Map Core Activities Within Processes

For each process, identify the core activities — the granular tasks that make up the process.

Example for "Site Visit" process:
- Arrive and introduce team
- Walk existing space with client
- Take detailed measurements
- Photograph existing conditions
- Document mechanical locations
- Discuss client vision and pain points
- Set expectations for next steps

**Remember:** Each core activity must start with an action verb.

### Step 7: Assign Roles to Each Level

For each level, document:
- **Owner/Role** — Who is responsible (use job title, never a name)
- **Decision Points** — Where the process can branch
- **Milestones** — Key deliverables or gates
- **Handoffs** — Where work transfers between roles/phases

### Step 8: Document Gaps and Assumptions

Note anything unclear or assumed:
- Processes mentioned but not detailed
- Variations mentioned but not fully explained
- **Roles that could not be determined from context** (list the name and what they seem to do)
- Timing that seems inconsistent

---

## Output Format

```
# [WORKFLOW NAME] Workflow

## Overview
- **Process:** [What this workflow accomplishes]
- **Trigger:** [What starts this process]
- **End State:** [What signals completion]
- **Key Roles:** [List job titles involved — no names]

---

## Phase 1: [Phase Name]
**Owner:** [Job title responsible]

### Process 1.1: [Process Name]
**Role:** [Job title who performs this process]

**Core Activities:**
- [Core activity 1 — starts with action verb]
- [Core activity 2 — starts with action verb]
- [Core activity 3 — starts with action verb]

### Process 1.2: [Process Name]
**Role:** [Job title who performs this process]

**Core Activities:**
- [Core activity 1]
- **DECISION:** [Decision point description]
  - If [condition A] → [outcome]
  - If [condition B] → [outcome]
- [Core activity 2]
- **MILESTONE:** [Key deliverable]

### Handoff to Phase 2:
- [What gets passed to next phase]
- [Role that receives it]

---

## Phase 2: [Phase Name]
[Continue pattern...]

---

## Notes & Assumptions
- [Gap or assumption 1]
- [Gap or assumption 2]
- [Any roles that need clarification]
```

---

## Discovery Questions

Use these questions when input is incomplete. Ask no more than 3 at a time.

### Process Scope
- What triggers this process to start?
- What does "done" look like — how do you know it's complete?
- Who are the main people involved?

### Processes & Sequence
- Walk me through what happens from start to finish
- What happens after [last mentioned process]?
- Are there processes that happen at the same time (in parallel)?

### Decisions & Branches
- Where do things go differently depending on the situation?
- What would cause this process to stop or restart?
- Are there approval points or gates where someone has to sign off?

### Handoffs
- When work moves from one person to another, how does that happen?
- What information gets passed along at handoffs?
- Where do things most often fall through the cracks?

### Timing
- How long does the whole process typically take?
- Which processes take the longest?
- Are there waiting periods or dependencies?

### Role Clarification
Use these when a transcript mentions names but not job titles:

- What is [Name]'s job title or role in the company?
- Is there a specific role that handles [function], or does it vary?
- When you mentioned [Name], are they in a leadership/management role or more hands-on?
- Does [Name] have a team under them, or do they work independently?
- If [Name] weren't available, who else could do that task? (helps identify the role vs. the person)
- Is [function they perform] their primary responsibility, or just part of what they do?

### Sales Process Questions
- How do leads come in?
- What makes a lead "qualified"?
- Who handles the first contact?
- What happens during a sales meeting or consultation?
- How do you present pricing or proposals?
- What needs to happen for a deal to close?
- How do you hand off to delivery/operations?

### Project-Based Business Questions
- How do projects get kicked off?
- Who creates the project plan or schedule?
- How is work assigned to team members?
- How do you track progress?
- What happens when scope changes?
- How does a project officially close out?

### Service Delivery Questions
- How do customers request service?
- How is work scheduled?
- Who performs the work?
- How do you ensure quality?
- What happens after the service is complete?
- How do you handle issues or callbacks?

### Construction/Contracting Questions
- How do you estimate or bid jobs?
- What happens between contract signing and start date?
- How do you coordinate subcontractors?
- What inspections or approvals are required?
- How do change orders work?
- What's the closeout process?

### Follow-Up Probes
When an answer is vague, probe deeper:
- "Tell me more about [specific process]"
- "Who specifically handles that — what's their role?"
- "What information do they need to do that?"
- "What could go wrong at that point?"
- "What happens if [condition]?"

---

## Quality Checklist

Before presenting workflow:
- [ ] **No personal names appear anywhere in the workflow**
- [ ] **Workflow is named after the process, not a person**
- [ ] **Workflow title ends with "Workflow"**
- [ ] **All core activities start with action verbs**
- [ ] **No roles or names in phase, process, or core activity titles**
- [ ] Phases represent major stages (4-8 total)
- [ ] Processes are significant actions within phases
- [ ] Core activities are granular tasks within processes
- [ ] Every process has an owner/role (job title)
- [ ] Decision points show all branches
- [ ] Handoffs between phases are explicit
- [ ] Milestones mark key deliverables
- [ ] Gaps and assumptions are documented (including unclear roles)
- [ ] Language matches how the business talks about their work
- [ ] Uses "Process" terminology (not "Step")
