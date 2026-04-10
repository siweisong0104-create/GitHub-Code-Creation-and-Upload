---
name: code-creator
description: Create and push open-source code projects to GitHub using Ralph automation. This skill handles the complete workflow: requirement analysis, PRD creation, Ralph automation, comprehensive testing (unit, E2E, security, coverage), and GitHub push.
---

# Code Creator

This skill helps users create open-source code projects and push them to GitHub with full automation and comprehensive testing.

## Activation

When user mentions `/code-creator` or wants to create a code project, activate this skill.

## Workflow

### Step 1: Gather Requirements

Ask the user detailed questions about their project:

```
## Welcome to Code Creator!

I'll help you create a complete open-source project with full testing.

1. **Project idea**: What do you want to build?
2. **Purpose**: What problem does this solve?
3. **Target users**: Who will use this?
4. **Key features**: What are the main features?
5. **Language**: Any specific language? (Python, JavaScript, Go, Rust, etc.)
6. **Framework**: Any preferred framework?
```

### Step 2: Create Project Directory

1. Create project directory
2. Initialize git repository (`git init`)
3. Copy Ralph scripts to `./scripts/ralph/`

### Step 3: Generate PRD

Use the PRD skill to generate a detailed Product Requirements Document:

1. Create `tasks/prd-[project-name].md` with:
   - Project overview
   - Goals
   - User stories (small, actionable)
   - Functional requirements
   - Technical considerations

### Step 4: Convert to prd.json

Use the Ralph skill to convert PRD to prd.json format:

1. Convert PRD to `prd.json`
2. Ensure stories are small enough for one iteration each

### Step 5: Run Ralph Automation

Run Ralph to automatically implement the project:

```
./scripts/ralph/ralph.sh --tool claude [iterations]
```

Execute Ralph and monitor progress until completion.

### Step 6: Comprehensive Testing

After Ralph completes, run comprehensive tests.

**For detailed commands by language, see:** [commands.md](references/commands.md)

#### 6.1 Unit Tests

Run tests based on project type (npm test, pytest, go test, cargo test, etc.)

#### 6.2 Coverage

Generate coverage report. Target: 80% threshold.

#### 6.3 Type Check

Run type checks (tsc --noEmit, mypy, go vet, cargo check)

#### 6.4 Linting

Run linters (eslint, pylint, gofmt, clippy)

#### 6.5 Security Scanning

Run security checks (npm audit, bandit, cargo audit)

Fix critical/high vulnerabilities before proceeding.

#### 6.6 E2E Testing

For web projects, set up and run E2E tests.

**For detailed E2E setup guide, see:** [e2e-testing.md](references/e2e-testing.md)

#### 6.7 Build Verification

Verify project builds successfully.

### Step 7: Test Report

Present comprehensive test results:

- Unit Tests: [X] passed
- Coverage: [X]%
- Type Check: PASSED/FAILED
- Linting: PASSED/FAILED
- Security: [X] vulnerabilities fixed
- Build: PASSED/FAILED

Fix any failures before proceeding.

### Step 8: GitHub Push

Push to GitHub:

1. **Check if should push**: Ask user if they want to push to GitHub
2. **New repo**: Create via web or `gh repo create`
3. **Existing repo**: Add remote and push
4. **Push**: `git add . && git commit -m "Complete" && git push -u origin [branch]`

### Step 9: Git Cleanup

After all operations, clean up git state to avoid leaving uncommitted changes:

```
## Git Cleanup

Checking for uncommitted changes...
```

1. **Check git status**: `git status --porcelain`
2. **If there are uncommitted changes**:
   - If user wants to push: commit and push (Step 8)
   - If not pushing: ask user whether to discard or keep changes
3. **For temporary files** (like progress.txt from Ralph):
   - Check if file is needed for future runs
   - If not needed, remove: `rm -f progress.txt`
4. **For working files** that shouldn't be committed:
   - Add to `.gitignore` or
   - Use `git restore` to discard

**Important**: Don't leave uncommitted changes without user consent. Always ask:
- "Do you want to commit and push these changes?"
- Or "Should I discard these changes?"

### Step 10: Summary

Present final results:

- Project name and description
- Files created
- GitHub repository URL (if pushed)
- Testing summary