# Claude Code Docs

This project contains the files I use to customize Claude Code, like my default rules and some custom skills that I use in my daily work.

## Contents

- **`CLAUDE.md`**, which defines my default rules for Claude, including general behavior and coding standards for Java and React/TypeScript/JavaScript;
- **`skills/create-pr-description`**, which generates a Pull Request description based on the changes in the current branch, without creating the PR;
- **`skills/move-branch`**, which recreates the current branch from a different base branch, preserving its changes and leaving them uncommitted;
- **`skills/review-pr`**, which reviews the changes in the current branch against its base branch and points out relevant issues, without modifying the code.

## How to Use

1. Copy `CLAUDE.md` to `~/.claude/CLAUDE.md` to apply the rules to all projects;
2. Copy the folders inside `skills` to `~/.claude/skills/`;
3. Invoke the skills manually in Claude Code, like `/review-pr`. They are not invoked automatically by the model.

## Additional Info

This project will always be under construction, since I keep adjusting these files as I use them. Don't worry if anything on it changes. 😅

## License

The available source codes here are under the MIT License (see the attached `LICENSE` file for more details). Any questions can be submitted to my email: carloswilldecarvalho@outlook.com.
