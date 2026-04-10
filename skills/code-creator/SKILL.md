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

I'll help you create a complete open-source project with full testing. Let's start with some questions.

1. **Project idea**: What do you want to build? (e.g., "A Python CLI tool for processing CSV files")
2. **Purpose**: What problem does this solve?
3. **Target users**: Who will use this?
4. **Key features**: What are the main features?
5. **Language preference**: Any specific language? (Python, JavaScript, Go, Rust, etc.)
6. **Framework**: Any preferred framework?
7. **Testing preference**: Any specific testing frameworks?
```

### Step 2: Create Project Directory

Create the project directory and initialize git:

```
## Setting Up Project

Creating project structure...
```

1. Create project directory
2. Initialize git repository (`git init`)
3. Copy Ralph scripts to `./scripts/ralph/`

### Step 3: Generate PRD

Use the PRD skill to generate a detailed Product Requirements Document:

```
## Creating PRD

Generating detailed requirements document...
```

1. Create `tasks/prd-[project-name].md` with:
   - Project overview
   - Goals
   - User stories (small, actionable)
   - Functional requirements
   - Technical considerations

### Step 4: Convert to prd.json

Use the Ralph skill to convert PRD to prd.json format:

```
## Converting to Ralph Format

Creating task list for automated implementation...
```

1. Convert PRD to `prd.json`
2. Ensure stories are small enough for one iteration each

### Step 5: Run Ralph Automation

Run Ralph to automatically implement the project:

```
## Running Ralph

Starting automated code generation...

This will:
1. Create a feature branch
2. Implement each user story
3. Run quality checks (typecheck, tests)
4. Commit automatically
5. Repeat until all stories pass

Run: ./scripts/ralph/ralph.sh --tool claude [iterations]
```

Execute Ralph and monitor progress until completion.

### Step 6: Comprehensive Testing

After Ralph completes, run comprehensive tests:

```
## Comprehensive Testing

Now let's run thorough testing to ensure code quality.
```

#### 6.1 Unit Tests

Run unit tests based on project type:

| Language | Command |
|----------|---------|
| JavaScript/TypeScript | `npm test` or `yarn test` |
| Python | `pytest` or `python -m unittest` |
| Go | `go test ./...` |
| Rust | `cargo test` |
| Java | `mvn test` or `gradle test` |
| Ruby | `bundle exec rspec` |

#### 6.2 Test Coverage

Generate coverage report:

| Language | Command |
|----------|---------|
| JavaScript/TypeScript | `npm test -- --coverage` or `jest --coverage` |
| Python | `pytest --cov=. --cov-report=html` |
| Go | `go test -coverprofile=coverage.out ./...` |
| Rust | `cargo tarpaulin` or `cargo coverage` |

Report coverage percentage and ensure it meets threshold (default: 80%).

#### 6.3 Type Checking

Run type checks:

| Language | Command |
|----------|---------|
| TypeScript | `tsc --noEmit` |
| Python | `mypy .` or `pyright` |
| Go | `go vet ./...` |
| Rust | `cargo check` |

#### 6.4 Linting

Run linters:

| Language | Command |
|----------|---------|
| JavaScript/TypeScript | `eslint .` or `npm run lint` |
| Python | `pylint .` or `flake8` |
| Go | `gofmt -d .` |
| Rust | `cargo clippy` |

#### 6.5 Security Scanning

Run security checks:

| Language | Command |
|----------|---------|
| JavaScript/TypeScript | `npm audit` or `npm audit --audit-level=high` |
| Python | `bandit -r .` or `safety check` |
| Go | `gosec ./...` |
| Rust | `cargo audit` |

Fix any critical or high severity vulnerabilities.

#### 6.6 E2E Testing (for Web Projects)

For web projects, run E2E tests:

```
## E2E Testing

Running end-to-end tests...
```

1. Check if E2E tests exist (e.g., Playwright, Cypress)
2. If not, create basic E2E test structure
3. Run E2E tests
4. Verify in browser using dev-browser skill for manual verification

#### 6.7 Build Verification

Verify the project builds successfully:

| Language | Command |
|----------|---------|
| JavaScript/TypeScript | `npm run build` or `yarn build` |
| Python | `python setup.py build` |
| Go | `go build -o main .` |
| Rust | `cargo build --release` |

### Step 7: Test Report

Generate and present a comprehensive test report:

```
## Test Report

### Unit Tests
- Status: [PASSED/FAILED]
- Tests run: [X]
- Passed: [X]
- Failed: [X]

### Coverage
- Percentage: [X]%
- Threshold: 80%
- Status: [PASSED/FAILED]

### Type Check
- Status: [PASSED/FAILED]
- Errors: [X]

### Linting
- Status: [PASSED/FAILED]
- Issues: [X]

### Security
- Vulnerabilities found: [X]
- Critical: [X]
- High: [X]
- Fixed: [X]

### E2E Tests (if applicable)
- Status: [PASSED/FAILED]
- Tests run: [X]

### Build
- Status: [PASSED/FAILED]

### Overall Status: [GREEN/RED]
```

If any tests fail, fix them before proceeding.

### Step 8: GitHub Push

Push to GitHub:

```
## GitHub Push

Let's push your project to GitHub!

1. **New or existing repo?**
   - If new: Create repo with `gh repo create [name] --public`
   - If existing: Add remote and push

2. **Push process:**
   ```
   git add .
   git commit -m "Complete project with tests"
   git remote add origin https://github.com/username/repo.git
   git push -u origin main
   ```
```

### Step 9: Summary

Present final results:

```
## Project Complete! 🎉

Your project has been created and pushed!

- **Project**: [name]
- **Description**: [description]
- **Files created**: [list]
- **GitHub**: [repo URL]
- **Branch**: [branch name]

### Testing Summary
- Unit Tests: [X] passed
- Coverage: [X]%
- Type Check: [PASSED/FAILED]
- Linting: [PASSED/FAILED]
- Security: [X] vulnerabilities fixed
- Build: [PASSED/FAILED]

Would you like any modifications?
```
