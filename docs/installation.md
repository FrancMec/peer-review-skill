# Installation

This guide explains how to install and use the **AI Peer Review Skill** in Cursor.

---

## Prerequisites

Before installing the Skill, ensure you have:

- Cursor installed
- A local Git repository
- Git available from the command line

---

## Step 1 — Download the Skill

Download the following file from this repository:

```text
skill/peer-review-skill.md
```

---

## Step 2 — Create a Skills Folder

If your project doesn't already contain a Cursor Skills folder, create one:

```text
.cursor/
└── skills/
```

---

## Step 3 — Copy the Skill

Copy the file into your project:

```text
.cursor/
└── skills/
    └── peer-review-skill.md
```

---

## Step 4 — Open the Project in Cursor

Open your project in Cursor.

The Skill will be available for use within the project.

---

## Step 5 — Run the Skill

Invoke the Skill when your feature is complete and before creating a Pull Request.

Example prompts:

- Review my current branch.
- Run the Peer Review Skill.
- Review the changed files.
- Generate a peer review report.

---

## What the Skill Does

The Skill:

- Reviews only the files changed in the current branch or Pull Request
- Uses the rest of the repository only as context
- Checks for repetitive engineering issues
- Generates a structured Markdown review report

The review includes checks such as:

- Naming conventions
- Coding standards
- Project patterns
- Architecture
- Performance
- Security
- Error handling
- Logging
- Dependency Injection
- Async usage
- Null handling
- Duplicate code
- Maintainability
- Code smells
- Best practices

---

## What the Skill Does NOT Do

This Skill intentionally does not review:

- Business requirements
- Product decisions
- UX decisions
- Feature scope
- Long-term architectural direction

Those remain the responsibility of the human reviewer.

---

## Output

The Skill generates a Markdown report containing:

- Review Summary
- Overall Checklist
- Critical Issues
- Warnings & Suggestions
- Passed Checks
- Category-wise Review
- Final Recommendation

A sample report is available here:

```text
examples/sample-review-report.md
```

---

## Recommended Workflow

```text
Complete Feature
        │
        ▼
Run Peer Review Skill
        │
        ▼
Review Generated Report
        │
        ▼
Fix Identified Issues
        │
        ▼
Create Pull Request
        │
        ▼
Human Code Review
```

---

## Tips

- Run the Skill before every Pull Request.
- Address Critical issues before requesting review.
- Use the report as supporting documentation in your Pull Request or Azure DevOps work item.
- The report helps reviewers focus on architecture and business logic instead of repetitive engineering comments.
