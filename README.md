# AI Peer Review Skill for Cursor

AI-powered Peer Review Skill for Cursor that reviews only changed files and generates professional Markdown reports.

A production-ready Cursor Skill that performs a **first-pass peer review** before your Pull Request reaches a human reviewer.

Instead of spending review time pointing out repetitive issues like naming, coding standards, logging, null handling, dependency injection, async usage, or architecture consistency, this Skill reviews the changed files and generates a structured Markdown report.

The goal is **not to replace a senior reviewer**—it's to eliminate repetitive review comments so human reviewers can focus on architecture, business logic, scalability, design decisions, and meaningful technical discussions.

---

## Why This Skill?

Most code reviews contain the same repetitive comments:

- "Please rename this method."
- "Missing CancellationToken."
- "This should use dependency injection."
- "Logging needs more context."
- "This duplicates existing logic."
- "This belongs in the service layer."

These are valuable comments, but they're also predictable.

This Skill helps developers identify those issues **before requesting a review**, making Pull Requests cleaner and allowing reviewers to spend their time on higher-value feedback.

---

## Features

- ✅ Reviews **only the changed files** in the current branch or Pull Request
- ✅ Uses the rest of the repository **only as context** for project conventions
- ✅ Generates a structured Markdown peer review report
- ✅ Identifies repetitive engineering issues before code review
- ✅ Highlights Critical, Warning, and Passed checks
- ✅ Respects existing project conventions instead of enforcing personal preferences
- ✅ Designed to support—not replace—human code reviews

---

## What It Reviews

The Skill evaluates changed files for:

- Naming conventions
- Coding standards
- Project patterns
- Code readability
- Unnecessary or redundant logic
- Better implementation opportunities
- Repository and service usage
- Architecture consistency
- Performance concerns
- Security issues
- Error handling
- Logging
- Dependency Injection
- Async usage
- Null handling
- Duplicate code
- Maintainability
- Code smells
- General engineering best practices

---

## Review Philosophy

This Skill follows a few important principles:

- Review **only the changed files**
- Read the rest of the repository **only for context**
- Respect existing project conventions
- Do not invent issues
- Do not generate generic AI suggestions
- Recommend improvements only when there is a clear engineering benefit

The purpose is consistency—not perfection.

---

## Example Workflow

```text
Developer completes feature
            │
            ▼
Run AI Peer Review Skill
            │
            ▼
Review generated Markdown report
            │
            ▼
Fix identified issues
            │
            ▼
Create Pull Request
            │
            ▼
Human peer review
```

---

## Sample Report

A sample generated report is available here:

```
examples/sample-review-report.md
```

---

## Installation

Installation instructions are available here:

```
docs/installation.md
```

---

## Repository Structure

```text
peer-review-skill/
│
├── README.md
├── LICENSE
│
├── skill/
│   └── peer-review-skill.md
│
├── examples/
│   └── sample-review-report.md
│
└── docs/
    └── installation.md
```

---

## Limitations

This Skill intentionally does **not** review:

- Business requirements
- Product decisions
- Feature scope
- UX decisions
- Long-term product strategy

Those remain the responsibility of the human reviewer.

---

## Contributing

Suggestions and improvements are welcome.

If you find false positives, missing review scenarios, or opportunities to improve the report quality, feel free to open an issue or submit a pull request.

---

## License

This project is licensed under the MIT License.
