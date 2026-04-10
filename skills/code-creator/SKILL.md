---
name: code-creator
description: Create and push open-source code projects to GitHub. Use this skill when users want to create a new code project, generate complete source code, add tests and documentation, and optionally push to GitHub. Handles the full workflow from requirements gathering to code generation, testing, and GitHub push.
---

# Code Creator

This skill helps users create open-source code projects and push them to GitHub.

## Activation

When user mentions `/code-creator` or wants to create a code project, activate this skill.

## Workflow

### Step 1: Gather Requirements

Ask the user about their project idea:
- "What kind of project do you want to create?"
- "What programming language and framework?"
- "Any specific features or functionality?"

### Step 2: Technical Discussion

Discuss technical details:
- Project structure
- Dependencies and packages
- API or library requirements

### Step 3: Code Generation

Generate the complete project:
- Project structure
- Source code files
- README.md, LICENSE, .gitignore
- Tests (if applicable)

### Step 4: Code Review

Review the generated code:
- Run type checking
- Check code quality and best practices

### Step 5: Testing

Test the generated code:
- Run project tests
- Verify build succeeds

### Step 6: GitHub Push (Optional)

Push to GitHub when ready:
- Ask for GitHub repository info (new or existing)
- Initialize git and push

## Installation

Ask user where to install the skill:
- Local: `./skills/code-creator/`
- Global: `~/.claude/skills/code-creator/`