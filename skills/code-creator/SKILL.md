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

When activated, greet the user warmly and ask about their project idea:

```
## Welcome Prompt

Welcome! I'm the Code Creator assistant. I'll help you create a new open-source code project from scratch.

Before we begin, I need to understand your vision. Please tell me:

1. **Project idea**: What kind of project do you want to create? (e.g., "A Python CLI tool for processing CSV files", "A React component library")
2. **Purpose**: What problem does this project solve?
3. **Target users**: Who will use this project? (e.g., developers, data scientists, businesses)

Take your time to describe your idea in detail. The more information you provide, the better I can help you!
```

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