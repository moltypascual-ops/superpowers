---
name: systematic-debugging
description: "Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes. Core skill for debugging methodology."
metadata: 
   openclaw:
       emoji: "🔍"
---

# Systematic Debugging

## Overview
Random fixes waste time and create new bugs. Quick patches mask underlying issues.

**Core principle:** ALWAYS find root cause before attempting fixes. Symptom fixes are failure.

**Violating the letter of this process is violating the spirit of debugging.**

## The Iron Law

NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST


If you haven't completed Phase 1, you cannot propose fixes.

## When to Use

Use for ANY technical issue:

* Test failures
* Bugs in production
* Unexpected behavior
* Performance problems
* Build failures
* Integration issues

**Use this ESPECIALLY when:**

* Under time pressure (emergencies make guessing tempting)
* "Just one quick fix" seems obvious
* You've already tried multiple fixes
* Previous fix didn't work
* You don't fully understand the issue

**Don't skip when:**

* Issue seems simple (simple bugs have root causes too)
* You're in a hurry (rushing guarantees rework)
* Manager wants it fixed NOW (systematic is faster than thrashing)

## The Four Phases

You MUST complete each phase before proceeding to the next.

### Phase 1: Root Cause Investigation

**BEFORE attempting ANY fix:**

1. **Read Error Messages Carefully**
* Don't skip past errors or warnings
* They often contain the exact solution
* Read stack traces completely using the `read` tool
* Note line numbers, file paths, error codes


2. **Reproduce Consistently**
* Can you trigger it reliably?
* What are the exact steps?
* Does it happen every time?
* If not reproducible → gather more data, don't guess


3. **Check Recent Changes**
* What changed that could cause this?
* Git diff, recent commits (use `exec` to run git commands)
* New dependencies, config changes
* Environmental differences


4. **Gather Evidence in Multi-Component Systems**
**BEFORE proposing fixes, add diagnostic instrumentation:**
* Log what data enters component
* Log what data exits component
* Verify environment/config propagation
* Check state at each layer


5. **Trace Data Flow**
* Where does bad value originate?
* What called this with bad value?
* Keep tracing up until you find the source
* Fix at source, not at symptom



### Phase 2: Pattern Analysis

**Find the pattern before fixing:**

1. **Find Working Examples**
* Locate similar working code in same codebase using `read`


2. **Compare Against References**
* Read reference implementation COMPLETELY


3. **Identify Differences**
* List every difference, however small


4. **Understand Dependencies**
* What other components does this need?



### Phase 3: Hypothesis and Testing

**Scientific method:**

1. **Form Single Hypothesis**
* State clearly: "I think X is the root cause because Y"


2. **Test Minimally**
* Make the SMALLEST possible change to test hypothesis


3. **Verify Before Continuing**
* Did it work? Yes → Phase 4
* Didn't work? Form NEW hypothesis


4. **When You Don't Know**
* Say "I don't understand X". Ask for help or use `web_search`/`browser` if needed.



### Phase 4: Implementation

**Fix the root cause, not the symptom:**

1. **Create Failing Test Case**
* Simplest possible reproduction
* MUST have before fixing
* Read skill `test-driven-development/SKILL.md` for proper methodology


2. **Implement Single Fix**
* Address the root cause identified
* ONE change at a time


3. **Verify Fix**
* Test passes now? (Run tests via `exec`)
* No other tests broken?


4. **If Fix Doesn't Work**
* STOP
* If < 3 fixes tried: Return to Phase 1
* **If ≥ 3: STOP and question the architecture**



## Red Flags - STOP and Follow Process

If you catch yourself thinking:

* "Quick fix for now, investigate later"
* "Just try changing X and see if it works"
* "Skip the test, I'll manually verify"
* **"One more fix attempt" (when already tried 2+)**

**ALL of these mean: STOP. Return to Phase 1.**

## Supporting Techniques

These techniques are part of systematic debugging. You should create them as reference files inside `/skills/systematic-debugging/references/` and read them when needed:

* **`root-cause-tracing.md`** - Trace bugs backward through call stack to find original trigger
* **`defense-in-depth.md`** - Add validation at multiple layers after finding root cause
* **`condition-based-waiting.md`** - Replace arbitrary timeouts with condition polling

**Related skills (Read their SKILL.md files to load them):**

* **`skills/test-driven-development`** - For creating failing test case (Phase 4, Step 1)
* **`skills/verification-before-completion`** - Verify fix worked before claiming success

