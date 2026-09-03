# SKILL.md

---

name: create-pr-description

description: Generates a Pull Request description based on the changes in the current branch without creating the PR.

disable-model-invocation: true

---

# Generate Pull Request Description

Generate a Pull Request description for the changes in the current branch.

## Instructions

1. Determine the base branch according to the rules below.
2. Analyze the commits and the diff between the current branch and the base branch.
3. Understand the overall purpose of the changes instead of simply describing individual files.
4. Generate a concise description, avoiding unnecessary details.
5. Set `CURRENT_BRANCH_NAME` to the portion of the current branch name after the last slash (`/`).
6. Save the result to `.pull-request/[CURRENT_BRANCH_NAME].md`.
7. Overwrite the file if it already exists.

## Base Branch

When `$ARGUMENTS` is provided, it indicates the name of the base branch using the following format:

`feature/[CURRENT_YEAR]/$ARGUMENTS`

Example:

If `$ARGUMENTS` is `release.2026.1.1`, the base branch will be:

`feature/2026/release.2026.1.1`

The current branch must then be compared against that branch.
If no argument is provided, automatically determine the most appropriate base branch using the Git history and available branches.

## Output Format

The generated file must contain:

* A concise PR title;
* A short description of the PR's purpose (max. 500 characters);
* Changes (as an unordered list);
* Affected functionality.

## Restrictions

* DO NOT create the Pull Request.
* DO NOT push.
* DO NOT create commits.
* DO NOT modify source code files.
* DO NOT invent information that cannot be determined from the code, commits, or diff.
* The only file this skill may create or modify is `.pull-request/[CURRENT_BRANCH_NAME].md`.
* 
