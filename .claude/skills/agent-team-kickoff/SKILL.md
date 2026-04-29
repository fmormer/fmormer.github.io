---
name: agent-team-kickoff
description: Describe a feature or task and get a structured work plan executed by the right specialist agents. The primary day-to-day interface for working with your deployed team.
argument-hint: "<feature or task description>"
user-invocable: true
---

# Skill: Kickoff

## Overview

`/agent-team-kickoff` is how you use your deployed team. Describe what you want to build or fix in plain language, and this skill:
1. Identifies which agents need to be involved
2. Produces a phased work plan
3. Executes it by spawning the right agents in sequence
4. Reports back with a summary of what was done

This skill is deployed into target repos alongside the agent files, so it's always available where your team is.

## Usage

```
/agent-team-kickoff "add CSV export to the invoices list page"
/agent-team-kickoff "implement user impersonation for the admin panel, with full audit logging"
/agent-team-kickoff "the checkout flow breaks on mobile Safari — investigate and fix"
/agent-team-kickoff "write the README for the new authentication service"
```

## Workflow

### Phase 1: Analyze the Request

Parse the feature or task:
- What type of work is this? (new feature, bug fix, refactor, documentation, security review, etc.)
- Which layers of the stack does it touch? (backend, frontend, database, mobile, infrastructure)
- Are there any cross-cutting concerns? (security, compliance, performance, accessibility)
- What's the complexity? (can be done in one pass, or needs multiple phases?)

### Phase 2: Identify Required Agents

Map the work to the deployed agents (read `<current-repo>/.claude/agents/`):
- Only use agents that are deployed in this repo
- If a needed agent isn't deployed, note it and suggest adding it via `/agent-team-manage`
- Order agents by dependency (architect first, then implementers, then QA)

### Phase 3: Build Work Plan

Present the plan before executing. **Always include the product-owner and qa-engineer phases** — Jira issue creation and Smartruns test management are not optional:

```
## Work Plan: [Feature Name]

**Complexity:** Medium
**Estimated phases:** 4

### Phase 0: Jira (product-owner)
- Assess scope and create the appropriate Jira issue type (task, story, or epic)
- Write acceptance criteria that QA will verify against
- Returns: Jira issue key to be used by subsequent phases

### Phase 1: Design (solution-architect)
- Define the data model changes needed for CSV export
- Confirm API endpoint design: GET /invoices.csv with filter params

### Phase 2: Implementation (ruby-rails-developer + frontend-developer)
- Rails: Add CSV serializer to InvoicesController, support filter params
- React: Add "Export CSV" button to InvoiceListPage, handle loading/error states

### Phase 3: Testing & Security (qa-engineer + security-engineer)
- QA: Create test cases in Smartruns linked to the Jira issue, execute them, log results
- Security: Verify export is scoped to current tenant — no cross-tenant data

**Ready to proceed? [y/n]**
```

### Phase 4: Execute

Once confirmed, spawn agents in the defined order. For each agent:

1. State what the agent is about to do
2. Spawn it as a subagent with the specific task and all relevant context:
   - The feature description
   - Any design decisions from previous phases
   - File paths and patterns in this repo to follow
   - The agent's specific scope (don't ask it to do another agent's job)
   - The Jira issue key from Phase 0 (so agents can reference it)
3. Wait for the agent to complete
4. Summarize what it did before moving to the next phase

**Phase 0 is always first.** The product-owner agent must run before any implementation begins. Its output (Jira issue key + acceptance criteria) is passed as context to all subsequent agents.

#### Agent Invocation Context Template
```
You are the [role] on this project. Your task: [specific task]

Project context:
- Tech stack: [from CLAUDE.md or detected files]
- Relevant files: [list key files]
- Constraints: [any rules from CLAUDE.md or AGENTS.md]
- Jira issue: [key returned by product-owner in Phase 0]
- Previous phase output: [summary of what was designed/built so far]

Read AGENTS.md and CLAUDE.md from the project root before starting — they contain project-specific instructions that take priority over your defaults.

Complete your task and report what you did.
```

### Phase 5: QA Phase (always last if qa-engineer is deployed)

The QA agent always runs after implementation. Smartruns test management is **mandatory**, not optional:
1. Start the dev environment if needed (based on the project's stack)
2. Read Smartruns credentials from `.claude/team-config.json`
3. Create test cases in Smartruns linked to the Jira issue from Phase 0
4. Test the implemented feature in the browser against the acceptance criteria
5. Log pass/fail results against each test case in Smartruns
6. Report: Smartruns run URL, passed flows, any bugs found with reproduction steps

### Phase 6: Final Summary

```
## Kickoff Complete: [Feature Name]

### Jira: [ISSUE-KEY] — [Issue title]

### What was done:
- **product-owner**: Created [ISSUE-KEY] (story/task/epic), wrote acceptance criteria
- **solution-architect**: Designed CSV export endpoint and data model
- **ruby-rails-developer**: Implemented InvoicesController#index.csv with tenant scoping
- **frontend-developer**: Added Export CSV button with loading state and error handling
- **security-engineer**: Confirmed tenant scoping — no cross-tenant risk found
- **qa-engineer**: 5 test cases created and executed in Smartruns — all passed. [Link to run]

### Files changed:
- app/controllers/invoices_controller.rb
- app/serializers/invoice_csv_serializer.rb
- src/pages/InvoiceListPage.tsx

### Next steps:
- [ ] PR review
- [ ] Deploy to staging for final validation
```

## Notes

- If an agent is blocked or produces an error, report it and ask how to proceed before continuing
- Complex features may need multiple `/agent-team-kickoff` calls (one per major phase)
- For bug investigations, the first agent is usually the language specialist for the affected layer; QA confirms the fix
