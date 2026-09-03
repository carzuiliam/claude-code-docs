# CLAUDE.md

This file defines the default rules for Claude on this machine and for my user (Carlos Carvalho).

## General Rules

* Always respond in Brazilian Portuguese. Source code must always be written in English.
* Prefer simple solutions, avoiding unnecessary abstractions and complexity.
* Keep responses concise.
* Always briefly explain the changes made and the reason behind them.
* Do not make changes outside the requested scope.
* Do not assume relevant requirements; ask when necessary.
* The prompt always takes precedence over this file.

## Source Code Rules (General)

* Always consider the platform version and take advantage of the features available in that version.
* Always follow the project's existing coding standards and conventions.
* Prefer minimal changes focused on what is necessary.
* Preserve existing names and structures unless there is a reason to change them.
* Extract complex code into functions when doing so improves clarity. Keep simple and short code in the original block when there is no need for reuse.
* Avoid comments that merely describe what the code already makes clear.
* Do not refactor or reformat code unrelated to the task.
* Do not add new dependencies unless necessary.
* Do not run project builds or tests after making changes.

## Source Code Rules (Java)

* The order within classes should be: enums, fields, constructors, methods, static fields, and static methods.
* Within each group defined above, use the following visibility order: public, protected, and private.
* Avoid static methods unless the class does not make sense as an instance.
* Prefer `.builder()` when constructing objects.
* In `.stream()`, keep predicates simple; extract the logic into a method when it involves more than one call or condition.
* Every `catch` block must log the error and return `null` for simple return types, or an empty value for lists and `Optional`.

## Source Code Rules (React/TypeScript/JavaScript)

* Always use semicolons at the end of statements, even when optional.
* The order within components should be: hooks, `useEffect`, functions, additional logic, and finally the `return`.
* The first `useEffect` should always be the component mount effect (with an empty dependency array).
* Always declare functions using `const functionName = (params...) => { /* code */ };`.
* Use `useStyles`/`makeStyles` for styling.
* Avoid `any`, except when following existing code that already uses it.
* Export only what needs to be used outside the file.
