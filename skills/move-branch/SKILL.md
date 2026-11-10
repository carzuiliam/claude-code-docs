---
name: move-branch
description: Recreates the current branch from a different base branch while preserving its changes and leaving them uncommitted.
disable-model-invocation: true
---

# Recreate Branch

Recreate the current branch from a different destination base branch.
Preserve only the changes introduced by the current branch and apply them to a new branch without preserving commit history.

## Instructions

1. Determine the current branch name.
2. Determine the current base branch and destination base branch according to the rules below.
3. Verify that the working tree is clean before making any changes.
4. Fetch the latest remote branch references.
5. Analyze the complete diff between the current branch and its current base branch.
6. Preserve only the changes introduced by the current branch.
7. Create a new branch from the destination base branch using the current branch name followed by `-new`.
8. Apply the preserved changes to the new branch.
9. Leave all resulting changes uncommitted and unstaged.
10. Verify that the resulting working tree contains the expected changes.

## Base Branches

`$ARGUMENTS` must contain the current base branch and destination base branch using the following format:

`<current-base> <destination-base>`

Each argument must be the full branch name, used exactly as provided.

Example:

If `$ARGUMENTS` is:

`release/2026/release.2026.1.1.p1 release/2026/release.2026.1.1.p2`

The current base branch will be:

`release/2026/release.2026.1.1.p1`

The destination base branch will be:

`release/2026/release.2026.1.1.p2`

Both arguments are required.

If either argument is missing, do not continue.

## Change Detection

Compare the current branch against its current base branch using the Git merge base.

Use the equivalent of:

`git diff --binary <current-base>...HEAD`

The three-dot comparison must be used so that only changes introduced by the current branch since it diverged from the base branch are preserved.
The preserved changes must include:

* Modified files;
* Added files;
* Deleted files;
* Renamed files;
* Binary files.

Do not preserve:

* Commit history;
* Commit messages;
* Commit authors;
* Merge commits;
* Changes introduced only by the current base branch.

## New Branch

Determine the new branch name by appending `-new` to the current branch name.

Example:

If the current branch is:

`feature/ABC-123`

The new branch will be:

`feature/ABC-123-new`

Create the new branch directly from the latest available destination base branch.

Prefer:

`origin/<destination-base>`

after fetching remote references.
If the generated branch already exists locally, do not overwrite or modify it.

## Applying Changes

Apply the complete preserved diff to the new branch.

Prefer a three-way patch application when possible.

The equivalent Git operation may use:

`git apply --3way`

If the changes are applied successfully:

* Leave all changes uncommitted;
* Leave all changes unstaged;
* Do not push;
* Do not create a Pull Request.

If applying the changes produces conflicts:

* Do not automatically resolve semantic conflicts;
* Keep the new branch checked out;
* Preserve the conflicting state for manual resolution;
* Report the conflicting files;
* Do not commit;
* Do not push.

## Safety Guidelines

Before creating or switching branches:

* Verify that there are no staged changes;
* Verify that there are no unstaged changes;
* Verify that there are no untracked files;
* Verify that the repository is not currently performing a merge, rebase, or cherry-pick;
* Verify that the current base branch exists;
* Verify that the destination base branch exists;
* Verify that the generated `-new` branch does not already exist.

If any safety check fails, stop without modifying the repository.

## Output Format

Start with a short summary of the operation.
Report:

* Original branch;
* Current base branch;
* Destination base branch;
* New branch;
* Whether the changes were applied successfully;
* Any conflicts that require manual resolution;
* Current Git status.

If the operation succeeds, explicitly state that the changes were left uncommitted for manual review.

## Restrictions

* DO NOT modify the original branch.
* DO NOT rebase the original branch.
* DO NOT merge branches.
* DO NOT cherry-pick commits.
* DO NOT create commits.
* DO NOT push.
* DO NOT create the Pull Request.
* DO NOT delete branches.
* DO NOT overwrite an existing branch.
* DO NOT stash changes automatically.
* DO NOT automatically resolve semantic conflicts.
* DO NOT run builds or tests.
