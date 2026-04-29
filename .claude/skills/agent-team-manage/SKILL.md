---
name: agent-team-manage
description: Interactively add or remove agent roles from a deployed project repo. Shows currently deployed agents and what's available to add.
argument-hint: [target-repo-path]
user-invocable: true
---

# Skill: Manage Team

## Overview

Use this skill to adjust the team deployed in a project — add new agents as the project grows into new tech or requirements, or remove agents that are no longer needed.

## Usage

```
/agent-team-manage ../wtapi
/agent-team-manage /absolute/path/to/project
```

If no path is provided, ask the user.

## Workflow

### Phase 1: Load State

1. Resolve the target repo path.
2. Read all `.md` files from `<target>/.claude/agents/` — these are currently deployed agents.
3. Read all `.md` files from this repo's `agents/` — these are all available agents.

### Phase 2: Display Current State

```
Current team in <project-name> (8 agents):
  ✓ ruby-rails-developer
  ✓ frontend-developer
  ✓ qa-engineer
  ✓ security-engineer
  ✓ devops-engineer
  ✓ database-administrator
  ✓ product-owner
  ✓ solution-architect

Available but not deployed (13 agents):
  + python-developer
  + ios-developer
  + android-developer
  + rust-developer
  + atlassian-developer
  + devex-engineer
  + project-manager
  + ux-designer
  + technical-writer
  + data-engineer
  + growth-analytics-engineer
  + ai-engineer
  + compliance-engineer
```

### Phase 3: Interactive Actions

Ask: "What would you like to do?"
- **add <agent-name>**: Copy the agent file into the target
- **remove <agent-name>**: Delete the agent file from the target (with confirmation)
- **add-all**: Deploy all available agents
- **done**: Exit

Handle multiple operations in one session before exiting.

### Phase 4: Execute Changes

**Adding an agent:**
1. Copy `agents/<name>.md` → `<target>/.claude/agents/<name>.md`
2. Confirm: `✓ Added <name>`

**Removing an agent:**
1. Confirm with user: "Remove <name> from <project>? This deletes the file. [y/n]"
2. Delete `<target>/.claude/agents/<name>.md`
3. Confirm: `✓ Removed <name>`

### Phase 5: Final Report

```
Changes made to <project-name>:
  + Added: python-developer, ux-designer
  - Removed: rust-developer

Current team: 9 agents
```
