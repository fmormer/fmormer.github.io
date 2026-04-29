---
name: agent-team-update
description: Refresh agent files already deployed in a target repo with the latest versions from this claude-team repo.
argument-hint: <target-repo-path>
user-invocable: true
---

# Skill: Update Agents

## Overview

When you've improved agent files in this `claude-team` repo, use this skill to push the updates to a project that already has agents deployed. Only agents that exist in both repos are updated — no new agents are added (use `/agent-team-manage` for that).

## Usage

```
/agent-team-update ../wtapi
/agent-team-update /absolute/path/to/project
```

## Workflow

### Phase 1: Validate Paths

1. Confirm the source (this repo's `agents/` directory) and target paths.
2. Check that `<target>/.claude/agents/` exists. If it doesn't, suggest running `/agent-team-deploy` first.

### Phase 2: Compare

1. List all `.md` files in `<target>/.claude/agents/`
2. For each, check if a matching file exists in this repo's `agents/`
3. Build two lists:
   - **To update**: files that exist in both repos
   - **Not in source**: files in target that no longer exist in this repo (flag but don't delete)

### Phase 3: Show Diff Summary

Before copying, show what will change:

```
Agents to update (8):
  ruby-rails-developer.md
  frontend-developer.md
  qa-engineer.md
  ...

Agents in target NOT in source (1) — will not be touched:
  custom-agent.md  ← may be project-specific, skipping

Proceed? [y/n]
```

### Phase 4: Copy Updated Agent Files

For each file in the "to update" list:
1. Copy from `agents/<name>.md` → `<target>/.claude/agents/<name>.md`
2. Log each file updated

### Phase 5: Update Deployed Skills

For each skill folder that exists in `<target>/.claude/skills/`:
1. Check if a matching skill exists in this repo's `.claude/skills/`
2. If yes, copy `<source>/.claude/skills/<skill>/SKILL.md` → `<target>/.claude/skills/<skill>/SKILL.md`
3. Log each skill updated

Skills to check: `agent-team-kickoff`, `agent-team-update`, `agent-team-manage`, `agent-team-feedback`, `agent-team-onboard`

### Phase 6: Check for New Agents

After updating, check if there are agents in this repo that are NOT in the target:

```
New agents available in claude-team (not yet deployed):
  growth-analytics-engineer.md
  compliance-engineer.md

Run /agent-team-manage to add them.
```

### Phase 7: Report

```
✓ Updated 8 agents in <target>/.claude/agents/
✓ Updated 5 skills in <target>/.claude/skills/
  1 agent skipped (not in source — possibly project-specific)
  2 new agents available — run /agent-team-manage to add them
```
