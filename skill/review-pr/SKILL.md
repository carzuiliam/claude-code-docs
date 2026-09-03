# SKILL.md

---

name: review-pr

description: Reviews the changes in the current branch against its base branch and identifies relevant issues without modifying the code.

disable-model-invocation: true

---

# Review Pull Request

Review the changes in the current branch against the appropriate base branch.
Focus on identifying issues introduced by the current branch rather than reviewing unrelated existing code.

## Instructions

1. Determine the base branch according to the rules below.
2. Analyze the commits and the complete diff between the current branch and the base branch.
3. Understand the overall purpose of the changes before reviewing individual files.
4. Inspect surrounding code, related methods, classes, and dependencies when necessary to understand the impact of a change.
5. Identify issues introduced by the current branch.
6. Prioritize findings according to the following order:
   * Bugs and incorrect behavior;
   * Breaking behavior changes;
   * Missing or incorrect edge-case handling;
   * Security issues;
   * Data integrity issues;
   * Concurrency issues;
   * Performance regressions;
   * Incorrect error handling;
   * Missing or insufficient tests for relevant behavior changes.
7. For each finding, verify that it is caused by or directly related to the changes in the current branch.
8. Do not report an issue unless there is reasonable evidence that it may cause incorrect or undesirable behavior.

## Base Branch

When `$ARGUMENTS` is provided, it indicates the name of the base branch using the following format:

`release/[CURRENT_YEAR]/$ARGUMENTS`

Example:

If `$ARGUMENTS` is `release.2026.1.1`, the base branch will be:

`release/2026/release.2026.1.1`

The current branch must then be compared against that branch.
If no argument is provided, automatically determine the most appropriate base branch using the Git history and available branches.

## Review Guidelines

* Review only changes introduced by the current branch.
* Use the surrounding code as context, but do not report pre-existing issues unrelated to the diff.
* Follow method calls and dependencies when necessary to determine whether a change is correct.
* Consider how changed code interacts with existing callers and consumers.
* Consider null values, empty collections, optional values, boundary conditions, and unexpected inputs when relevant.
* Consider whether behavior changes may affect existing functionality.
* Consider database, API, event, messaging, and external service interactions when relevant.
* Consider whether tests adequately cover meaningful behavior introduced or changed by the branch.
* Do not assume that code is incorrect solely because it differs from a preferred implementation.
* Do not suggest refactoring unless the current implementation introduces a concrete maintainability or correctness problem.
* Do not report speculative issues without a plausible execution path that demonstrates the problem.

## Do Not Report

Do not report:

* Personal style preferences;
* Minor naming suggestions;
* Formatting issues;
* Import ordering;
* Comments or documentation improvements unless missing documentation causes a concrete problem;
* Opportunities to refactor code that is already correct and reasonably maintainable;
* Pre-existing issues unrelated to the current branch;
* Issues already handled elsewhere in the execution flow;
* Hypothetical problems without reasonable evidence that they can occur.

## Output Format

Start with a short summary of the review.
If issues are found, list each finding using the following format:

### [Severity] Short description

**Location:** `path/to/File.java:line`
**Problem:** Explain what is wrong.
**Impact:** Explain what may happen because of the issue.
**Evidence:** Explain the execution path or condition that demonstrates the problem.
**Suggestion:** Briefly describe how the issue could be addressed.

Use one of the following severity levels:

* `CRITICAL` — May cause severe production failures, security vulnerabilities, or data loss.
* `HIGH` — Likely to cause incorrect behavior or significant regressions.
* `MEDIUM` — Can cause incorrect behavior under specific realistic conditions.
* `LOW` — Minor but concrete issue worth addressing.

Order findings from highest to lowest severity.
If no relevant issues are found, explicitly state that no issues were identified in the changes.

## Restrictions

* DO NOT modify source code.
* DO NOT create or modify files.
* DO NOT create the Pull Request.
* DO NOT push.
* DO NOT create commits.
* DO NOT run builds or tests.
* DO NOT report issues unrelated to the changes in the current branch.
