---
name: agent-team-onboard
description: Interactive setup wizard for a newly deployed team. Collects Jira, Smartruns, and other integration credentials and writes them to .claude/team-config.json.
argument-hint: "[target-repo-path]"
user-invocable: true
---

# Skill: Team Onboard

## Overview

Run this skill after deploying a team to a new project to configure the credentials and integration settings the agents need. It walks through each integration step by step, validates what's already configured, and writes everything to `.claude/team-config.json`.

Run it from:
- The **target project repo** — configures the current repo
- The **claude-team source repo** — pass the target path as an argument

## Usage

```
/agent-team-onboard
/agent-team-onboard ../wtapi
/agent-team-onboard /absolute/path/to/project
```

## Workflow

### Phase 1: Resolve Target

1. If an argument was provided, use it as the target path.
2. If no argument and there's a `.claude/agents/` folder in the current directory, use the current directory.
3. Otherwise, ask: "Which project would you like to configure? (provide the path)"
4. Verify the path exists and has a `.claude/` folder. If not, suggest running `/agent-team-deploy` first.

### Phase 2: Read Existing Configuration

Check `.claude/team-config.json` in the target:
- If it exists, load it and show what's already configured:
  ```
  Existing configuration found in .claude/team-config.json:
    ✓ jira.org_url — configured
    ✓ jira.api_token — configured
    ✗ smartruns — not configured
  ```
- If it doesn't exist, start fresh.

### Phase 3: Jira / Atlassian Setup

Ask (skip if already configured and the user doesn't want to update):

> **Jira / Atlassian**
> This is used by the product-owner and qa-engineer agents to create issues and manage test cases.
>
> 1. Jira org URL (e.g., `https://yourorg.atlassian.net`):
> 2. Jira email address (the account that owns the token):
> 3. Jira personal API token (create one at https://id.atlassian.com/manage-profile/security/api-tokens):
> 4. Default Jira project key (e.g., `SR`, `PROJ`) — agents will create issues here unless told otherwise:

Validate the connection: attempt a lightweight API call (e.g., fetch `/rest/api/3/myself`) to confirm the credentials work before saving. Report success or failure.

### Phase 4: Smartruns Setup

Ask (skip if already configured):

> **Smartruns (QA Test Case Management)**
> Smartruns uses the same Jira credentials — no separate token needed.
>
> Smartruns is enabled automatically when Jira is configured. The QA agent will
> create test plans and cases linked to Jira issues.
>
> Would you like to enable Smartruns? [y/n]

If yes, record that Smartruns is enabled and note the Jira org URL will be reused.

### Phase 5: Additional Integrations (Optional)

Ask if the team needs any other integrations configured:

> **Other integrations** (optional — press Enter to skip each)
>
> - Slack webhook URL (for agent notifications):
> - GitHub token (if agents need to create PRs or read private repos):
> - Any other API keys or secrets:

For each provided value, store it under the appropriate key in `team-config.json`.

### Phase 6: Write Configuration

Write (or merge into existing) `.claude/team-config.json`:

```json
{
  "jira": {
    "org_url": "https://yourorg.atlassian.net",
    "email": "you@yourorg.com",
    "api_token": "<token>",
    "default_project": "SR"
  },
  "smartruns": {
    "enabled": true
  }
}
```

Only write keys the user provided — don't overwrite existing values the user chose to skip.

### Phase 7: Secure the File

1. Check if `.claude/team-config.json` is in `.gitignore`. If not, add it:
   ```
   # Claude team credentials (do not commit)
   .claude/team-config.json
   ```
2. Confirm: `✓ Added .claude/team-config.json to .gitignore`

### Phase 8: Verify Agent Readiness

Quick sanity check — list deployed agents and flag any that require config that's still missing:

```
Agent readiness check:
  ✓ product-owner — Jira configured
  ✓ qa-engineer — Jira + Smartruns configured
  ✓ ruby-rails-developer — no integration config needed
  ✓ frontend-developer — no integration config needed
  ✗ devops-engineer — no GitHub token configured (optional)
```

### Phase 9: Summary

```
✓ Onboarding complete for <project-name>

Configured:
  ✓ Jira (yourorg.atlassian.net) — connection verified
  ✓ Smartruns enabled
  ✓ .claude/team-config.json written and git-ignored

Your team is ready. Run /agent-team-kickoff to start working.
```

## Notes

- API tokens and secrets are written to `.claude/team-config.json` which is git-ignored. Never commit this file.
- If a connection test fails, show the error and ask the user to re-enter the credentials before saving.
- Agents read `team-config.json` at runtime — no environment variables or shell setup needed.
- Re-running `/agent-team-onboard` on an already-configured project lets you update individual values without losing others.
