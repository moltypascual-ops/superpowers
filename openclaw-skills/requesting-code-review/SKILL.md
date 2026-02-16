---
name: requesting-code-review
description: "Use when completing tasks, implementing major features, or before merging - verifies work meets requirements through code review"
metadata:
  openclaw:
    emoji: "👀"
---

# Requesting Code Review

Dispatch a code review subagent to catch issues before they cascade.

**Core principle:** Review early, review often.

## When to Request Review

**Mandatory:**
- After each task in subagent-driven development
- After completing major feature
- Before merge to main

**Optional but valuable:**
- When stuck (fresh perspective)
- Before refactoring (baseline check)
- After fixing complex bug

## How to Request

**1. Get git SHAs:**
```bash
BASE_SHA=$(git rev-parse HEAD~1)  # or origin/main
HEAD_SHA=$(git rev-parse HEAD)
```

**2. Dispatch code-reviewer subagent:**

Use `sessions_spawn` (or equivalent subagent spawning mechanism) with the following context:

**Template for code review request:**
```
You are a code reviewer. Review the changes between BASE_SHA and HEAD_SHA.

WHAT_WAS_IMPLEMENTED: [What you just built]
PLAN_OR_REQUIREMENTS: [What it should do - reference to plan file or requirements]
BASE_SHA: [Starting commit SHA]
HEAD_SHA: [Ending commit SHA]
DESCRIPTION: [Brief summary of changes]

Review for:
1. Correctness - Does it do what it should?
2. Code quality - Is it clean, maintainable?
3. Tests - Are they adequate?
4. Security - Any vulnerabilities?
5. Performance - Any concerns?

Format your response as:
- Strengths: [What's good]
- Issues (Critical/Important/Minor): [Problems found]
- Assessment: Ready to proceed / Needs fixes
```

**3. Act on feedback:**
- Fix Critical issues immediately
- Fix Important issues before proceeding
- Note Minor issues for later
- Push back if reviewer is wrong (with reasoning)

## Example

```
[Just completed Task 2: Add verification function]

You: Let me request code review before proceeding.

BASE_SHA=$(git log --oneline | grep "Task 1" | head -1 | awk '{print $1}')
HEAD_SHA=$(git rev-parse HEAD)

[Spawn subagent with code review instructions]
  WHAT_WAS_IMPLEMENTED: Verification and repair functions for conversation index
  PLAN_OR_REQUIREMENTS: Task 2 from docs/plans/deployment-plan.md
  BASE_SHA: a7981ec
  HEAD_SHA: 3df7661
  DESCRIPTION: Added verifyIndex() and repairIndex() with 4 issue types

[Subagent returns]:
  Strengths: Clean architecture, real tests
  Issues:
    Important: Missing progress indicators
    Minor: Magic number (100) for reporting interval
  Assessment: Ready to proceed

You: [Fix progress indicators]
[Continue to Task 3]
```

## Integration with Workflows

**Subagent-Driven Development:**
- Review after EACH task
- Catch issues before they compound
- Fix before moving to next task

**Executing Plans:**
- Review after each batch (3 tasks)
- Get feedback, apply, continue

**Ad-Hoc Development:**
- Review before merge
- Review when stuck

## Red Flags

**Never:**
- Skip review because "it's simple"
- Ignore Critical issues
- Proceed with unfixed Important issues
- Argue with valid technical feedback

**If reviewer wrong:**
- Push back with technical reasoning
- Show code/tests that prove it works
- Request clarification

## Quick Reference

| When | Review Type | Criticality |
|------|-------------|-------------|
| After each task | Quick review | High |
| Before merge | Full review | Mandatory |
| When stuck | Fresh perspective | Optional |
| After bugfix | Targeted review | Recommended |

## Tools Used

- `exec` - Run git commands to get SHAs
- Subagent spawning mechanism - Dispatch reviewer with context
- `read` - Reference plan files and requirements
