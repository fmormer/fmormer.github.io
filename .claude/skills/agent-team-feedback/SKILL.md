---
name: agent-team-feedback
description: Give feedback on an agent's behavior and have it incorporated directly into the agent's definition so it does better next time.
argument-hint: "<agent-name> <feedback>"
user-invocable: true
---

# Skill: Agent Feedback

## Overview

Use this skill when an agent did something wrong, or when you want to reinforce a behavior that worked well. The feedback is written directly into the agent's definition file so it takes effect on every future invocation — not just remembered for this session.

Works in both the `claude-team` source repo (modifies `agents/<name>.md`) and deployed project repos (modifies `.claude/agents/<name>.md`).

## Usage

```
/agent-team-feedback frontend-developer "stop adding console.log statements — they cause lint failures in CI"
/agent-team-feedback qa-engineer "always check dark mode AND light mode when testing visual changes"
/agent-team-feedback ruby-rails-developer "use strong_parameters for every controller action, never skip it"
/agent-team-feedback product-owner "ask for the sprint goal before writing user stories, so stories are framed around it"
```

Or run `/agent-team-feedback` without arguments and describe the issue interactively.

## Workflow

### Phase 1: Identify Agent and Agent File

1. Determine the agent name from the argument (or ask if missing).
2. Locate the agent file:
   - In a deployed project: `.claude/agents/<name>.md`
   - In the claude-team source repo: `agents/<name>.md`
   - If neither exists, list available agents and ask the user to clarify.
3. Read the current agent file.

### Phase 2: Understand the Feedback

Analyze what the user is describing:
- Is this a **correction** (agent did something wrong)? → Add a rule under a new or existing section.
- Is this a **reinforcement** (agent did something right)? → Strengthen an existing instruction or add emphasis.
- Is this a **new constraint** (something the agent should never do)?  → Add it to a "Constraints" or relevant section with clear DO/DON'T language.
- Does it affect **all tasks** or just a specific context (kickoff, QA phase, etc.)? → Place it in the right section.

### Phase 3: Determine Where to Place the Change

Map the feedback to the right section of the agent file:
- Behavioral rule → `## Responsibilities` or `## Coding Standards` (for code-related agents)
- Context-specific behavior → the relevant section (e.g., `## Kickoff Integration`, `## Smartruns Integration`)
- New "never do this" rule → add a `## Constraints` section if one doesn't exist, or append to an existing one
- Reinforcement of existing behavior → locate the relevant instruction and make it more explicit

### Phase 4: Show the Proposed Change

Before writing, show the user exactly what will change:

```
Agent: frontend-developer
File: agents/frontend-developer.md

Proposed addition to "## Coding Standards":

+ Never add console.log statements — they cause lint failures in CI and must be
+ removed before committing. Use a proper logger or remove debug output entirely.

Apply this change? [y/n]
```

### Phase 5: Write the Change

Once confirmed:
1. Edit the agent file to incorporate the feedback
2. Preserve all existing content — only add or strengthen, never delete other rules
3. Keep the language in the same imperative style as the rest of the agent file

### Phase 6: Propagate (Optional)

If the user is in the claude-team source repo and also has the agent deployed in other projects, ask:

> "Updated `agents/frontend-developer.md`. Would you like to push this to a deployed project? If so, provide the path (or run `/agent-team-update <target>` later)."

### Phase 7: Confirm

```
✓ Updated agents/frontend-developer.md

Added to "## Coding Standards":
  Never add console.log statements — they cause lint failures in CI and must be
  removed before committing. Use a proper logger or remove debug output entirely.

This change takes effect immediately in future sessions.
```

## Notes

- Feedback is written into the agent file permanently — it persists across sessions and projects.
- If the feedback conflicts with an existing rule, show the conflict and ask the user which version to keep.
- For broad changes affecting many agents (e.g., "all agents should do X"), offer to apply the same feedback to multiple agent files.
