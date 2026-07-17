---
name: peer-review
description: Reviews only the changed files in the current branch or pull request for repetitive engineering issues (naming, standards, patterns, architecture, performance, security, error handling, logging, DI, async, null handling, duplication, maintainability) and produces a Markdown report so a senior reviewer can focus on architecture and business logic. Use when the user asks to run a peer review, pre-review a branch, review a PR before requesting review, or generate a peer review report.
---

# Peer Review Skill

## Purpose

This Skill performs the repetitive, non-judgment checks a developer can catch before asking a senior engineer for review — naming conventions, coding standards, project patterns, readability, unnecessary code, architecture consistency, performance, security, error handling, logging, dependency injection, async usage, null handling, duplication, maintainability, and general code smells.

It does NOT replace a senior reviewer. Its only job is to clear repetitive issues out of the way before a human review starts, so that review can focus on architecture, business logic, scalability, trade-offs, and design decisions instead of repeating the same coding-standard comments every time.

## Scope — read this before doing anything else

- Review ONLY the files changed in the current branch or pull request (the diff against the target branch).
- Never review the entire repository. Do not open, scan, or comment on files that are not part of the current diff.
- The rest of the repository may be read ONLY for context — to check whether the changed code is consistent with existing patterns, naming, and conventions already used elsewhere in the project. Nothing found in that context read should be added to the report as an issue in its own right; it exists only to judge the changed files correctly.
- If it is not possible to determine the diff (no branch/target information available), ask the user for the source and target branch before proceeding. Do not fall back to reviewing the whole repository.

## What to check

For every changed file, evaluate against exactly these categories — no others:

1. **Naming conventions** — method, variable, class, and boolean names; consistency with the casing and naming style already used in the surrounding module.
2. **Coding standards** — formatting and style consistency with the rest of the codebase.
3. **Project patterns** — whether the change follows existing patterns already established in the project (e.g. repository pattern, service layering).
4. **Code readability** — whether the code is clear and easy to follow as written.
5. **Whether the implemented logic is actually needed** — redundant checks, dead branches, logic that duplicates something the runtime or framework already guarantees.
6. **Simpler or better approaches** — only flag when there's a clear, concrete engineering benefit; do not suggest alternatives for the sake of having a suggestion.
7. **Repository or service usage** — direct data-access calls that bypass an existing repository/service abstraction; new methods built from scratch when an existing one already covers the need.
8. **Architecture violations** — business logic in the wrong layer (e.g. in a controller instead of a service); dependencies pointing the wrong direction.
9. **Performance concerns** — queries inside loops (N+1), unnecessary materialization before filtering, synchronous calls in otherwise-async code paths.
10. **Security issues** — injection vectors, hardcoded secrets or connection strings, missing input validation on new endpoints.
11. **Error handling** — unhandled exceptions around external calls, swallowed exceptions, missing compensation for partial failures.
12. **Logging** — missing log entries on catch blocks, log entries without useful identifying context.
13. **Dependency Injection** — manual instantiation (`new ServiceClass()`) inside business logic instead of constructor injection.
14. **Async usage** — inconsistent or missing async/await, blocking calls in async code paths.
15. **Null handling** — missing null checks on fields the rest of the codebase treats as optional; redundant checks on values already guaranteed non-null.
16. **Duplicate code** — logic blocks that closely mirror existing code elsewhere in the changed files or in the referenced context, that should be extracted instead of copied.
17. **Maintainability** — anything that will clearly cause friction for future changes if left as-is.
18. **Code smells** — general indicators of poor structure not already covered above.
19. **Best practices** — deviations from established best practice for the language/framework in use, where relevant to this diff.

## Review discipline — hard constraints

- Do not invent issues. If a category has nothing to report, it passes — do not manufacture a suggestion to fill space.
- Do not generate generic AI feedback ("consider adding comments," "this could be improved") without a specific file, line, and concrete reason.
- Do not praise code unnecessarily. Passed checks are stated plainly as passed, not complimented.
- Respect existing project conventions. If the project already does something a certain way, consistency with that convention takes priority over a theoretically "better" alternative.
- Only recommend an improvement when there is a clear, specific engineering benefit — not a stylistic preference.
- Every issue must reference the specific file and, where applicable, the line or method it applies to.

## Workflow

1. Identify the changed files between the source branch and the target branch.
2. For each changed file, run through every category in "What to check."
3. Read other parts of the repository only as needed to judge consistency with existing patterns and conventions — never to generate findings about files outside the diff.
4. Classify each finding as Critical, Warning, or Passed.
5. Generate the Markdown report using the exact structure and status model below.
6. Recommend that the report be attached directly to the Azure DevOps story or the pull request itself, so the reviewer knows what has already been verified before opening the diff.

## Status model

Overall Status (one of):
- ✅ Approved
- ⚠️ Approved with Suggestions
- ❌ Request Changes

Per-check status (used in the Overall Checklist table):
- 🟢 Passed
- 🟡 Warning
- 🔴 Critical

Overall Status rules:
- ❌ Request Changes if any 🔴 Critical issue exists.
- ⚠️ Approved with Suggestions if there are no Critical issues but at least one 🟡 Warning.
- ✅ Approved if every check is 🟢 Passed.

## Report format

Produce the report in exactly this structure. Omit a subsection's content only if there is genuinely nothing to report for it (still include the heading, with "No issues found.").

```markdown
# Review Summary

- **Review Date:** <date>
- **Reviewer:** AI Peer Review Skill
- **Source Branch:** <source branch>
- **Target Branch:** <target branch>
- **Files Reviewed:** <count>
- **Overall Status:** <✅ Approved | ⚠️ Approved with Suggestions | ❌ Request Changes>

---

## Overall Checklist

| Check | Status |
|---|---|
| Naming Conventions | <🟢/🟡/🔴> |
| Code Quality | <🟢/🟡/🔴> |
| Architecture | <🟢/🟡/🔴> |
| Performance | <🟢/🟡/🔴> |
| Security | <🟢/🟡/🔴> |
| Maintainability | <🟢/🟡/🔴> |
| Error Handling | <🟢/🟡/🔴> |
| Logging | <🟢/🟡/🔴> |

---

## Critical Issues

### 🔴 <short issue title>
`<file>`, line <n> — <specific description of the problem>.
**Suggestion:** <concrete fix>.

(Repeat per critical issue. If none: "No critical issues found.")

---

## Warnings & Suggestions

### 🟡 <short issue title>
`<file>`, line <n> — <specific description>.

(Repeat per warning. If none: "No warnings.")

---

## Passed Checks

- ✅ <specific thing that passed, stated plainly>
- ✅ <specific thing that passed, stated plainly>

---

## Naming Convention Review
<Findings specific to naming, or "No issues found." plus one line of confirmation of consistency with existing conventions.>

## Code Quality Review
<Findings on readability, unnecessary code, coding standards.>

## Architecture Review
<Findings on project patterns, layering, repository/service usage.>

## Performance Review
<Findings on N+1 queries, unnecessary materialization, blocking calls.>

## Security Review
<Findings on injection, secrets, input validation.>

## Maintainability Review
<Findings on duplication, code smells, future friction.>

---

## Final Recommendation

<Overall status emoji + label> — <one to two sentences: what must be fixed before merge if anything is Critical, and what is safe to address as fast-follow if only Warnings exist.>
```

## Final reminder

This Skill exists to save review time on repetitive issues, not to be a comprehensive audit. Stay inside the diff, stay inside the listed categories, and stop there. Anything about whether the feature is the right feature, whether the approach fits the product direction, or whether a "clever" solution will be a maintenance problem later is a human reviewer's call — not something this Skill should attempt to answer.
