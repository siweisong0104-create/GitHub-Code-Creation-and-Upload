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

Now that I understand your project vision, let's discuss the technical details. Please answer:

```
## Technical Discussion

Great! Now let's dive into the technical details.

1. **Programming language**: What language(s) will you use? (e.g., Python, JavaScript, Go, Rust)
2. **Framework**: Do you have a preferred framework? (e.g., React, Django, Express, Vue)
3. **Tech stack**: Any specific libraries or tools?
4. **Project structure**: Do you have a specific structure in mind?
5. **Additional requirements**: Any specific features or requirements?

Feel free to share as much or as little as you like - I'm here to help!
```

After receiving answers, summarize and confirm:
```
## Discussion Summary

Based on our discussion:
- Language: [summary]
- Framework: [summary]
- Tech stack: [summary]
- Structure: [summary]

Does this look correct? We'll use these details to generate your code.
```

Record all discussion results in the conversation for use in code generation.

### Step 3: Code Generation

Generate the complete project based on gathered requirements and technical discussion. Use this prompt to guide the code generation:

```
## Code Generation

Based on our discussion, I'll now generate the complete project code.

### Requirements Summary
- Project: [project idea from Step 1]
- Language: [from Step 2]
- Framework: [from Step 2]
- Tech stack: [from Step 2]

### Generation Process

1. **Create project structure**:
   - Determine appropriate directory structure for the language/framework
   - Create necessary directories (src/, tests/, docs/, etc.)
   - Set up package.json, requirements.txt, or equivalent

2. **Generate source code**:
   - Create main entry point files
   - Implement core functionality based on project purpose
   - Add utility functions and helpers as needed
   - Follow best practices for the specific language/framework

3. **Generate configuration files**:
   - README.md with project description, installation, usage
   - LICENSE (default: MIT)
   - .gitignore appropriate for the language
   - Any framework-specific configs (tsconfig.json, pyproject.toml, etc.)

4. **Generate tests** (if applicable):
   - Create test files matching source files
   - Include basic test cases
   - Follow testing best practices for the language

Please generate all files now. Start with the project structure, then create each source file with complete, working code.
```

After generating, confirm completion:
```
## Generation Complete

I've generated the following:
- Project structure: [list directories]
- Source files: [list files created]
- Config files: [README.md, LICENSE, .gitignore]
- Tests: [list test files if any]

All files are ready in the project directory. Ready to proceed to code review?
```

### Step 4: Code Review

Review the generated code for quality and best practices. Use this prompt to guide the code review:

```
## Code Review

Now let's review the generated code to ensure quality and best practices.

### Review Process

1. **Run type checking**:
   - For TypeScript/JS: Run `tsc --noEmit` or `npm run typecheck`
   - For Python: Run `mypy` or `pyright`
   - For Go: Run `go vet` and `gofmt`
   - For Rust: Run `cargo check`
   - Note any type errors and fix them

2. **Check code quality**:
   - Review code for readability and clarity
   - Check for proper error handling
   - Verify naming conventions are consistent
   - Look for code duplication that could be refactored

3. **Check best practices**:
   - Security: No hardcoded secrets, proper input validation
   - Performance: No obvious inefficiencies
   - Maintainability: Clear comments, good documentation

4. **Provide review report**:
   - Summary of findings
   - Issues found (if any)
   - Recommendations for improvement
```

After reviewing, present findings:
```
## Code Review Complete

Type checking: [PASSED/FAILED - list any errors]
Code quality: [summary of quality review]
Best practices: [summary of compliance]

[If issues found]: I've fixed the following issues:
- [list fixes applied]

The code is now ready for testing. Proceed to Step 5?
```

### Step 5: Testing

Test the generated code to ensure it works correctly. Use this prompt to guide testing:

```
## Testing

Now let's test the generated code to ensure it works correctly.

### Testing Process

1. **Run project tests**:
   - For Node.js/TypeScript: Run `npm test` or `yarn test`
   - For Python: Run `pytest` or `unittest`
   - For Go: Run `go test`
   - For Rust: Run `cargo test`
   - Record test results and any failures

2. **Verify build succeeds**:
   - For Node.js: Run `npm run build` or `yarn build`
   - For Python: Verify package installs correctly (`pip install -e .`)
   - For Go: Run `go build`
   - For Rust: Run `cargo build`
   - Ensure no build errors

3. **Test basic functionality**:
   - If applicable, run the main entry point
   - Verify basic operations work as expected
   - Check that dependencies are properly configured

4. **Provide test report**:
   - Test suite results (passed/failed/total)
   - Build status
   - Any issues found
```

After testing, present results:
```
## Testing Complete

Test results: [X passed, Y failed]
Build status: [SUCCESS/FAILED]
Functional check: [PASSED/FAILED]

[If issues found]: I've fixed the following:
- [list fixes applied]

All tests pass. Ready to proceed to GitHub push?
```

### Step 6: GitHub Push (Optional)

Push the code to GitHub when the user is ready. Use this prompt to guide the GitHub push:

```
## GitHub Push

Now let's push your code to GitHub. First, I need some information.

### Repository Setup

1. **Ask: New or existing repository?**
   - "Do you want to create a new GitHub repository or push to an existing one?"

2. **If New Repository**:
   - Ask for repository name (default: project name from Step 1)
   - Ask if repository should be public or private
   - Ask for optional description
   - Ask if user wants to add a .gitignore (usually yes)

3. **If Existing Repository**:
   - Ask for the existing repository URL (e.g., https://github.com/username/repo)
   - Ask if they want to add the remote or replace existing

### Push Process

1. **Initialize Git** (if not already initialized):
   ```
   git init
   git add .
   git commit -m "Initial commit"
   ```

2. **Create repository** (if new):
   - Use GitHub CLI: `gh repo create [repo-name] --public` or `--private`
   - Or provide manual instructions for web creation

3. **Add remote**:
   ```
   git remote add origin https://github.com/username/repo.git
   ```

4. **Push to GitHub**:
   ```
   git push -u origin main
   ```

5. **Verify push**:
   - Confirm repository exists at the expected URL
   - List pushed files

After pushing, confirm:
```
## GitHub Push Complete

Repository: [URL]
Branch: main
Files pushed: [count]

Your project is now live on GitHub! 
- View at: [repo URL]
- Clone with: git clone [repo URL]

Would you like me to help with anything else?
```
```

If user skips GitHub push:
```
## GitHub Push Skipped

No problem! Your project is ready locally at [project directory].

When you're ready to push to GitHub:
1. Create a repository at https://github.com/new
2. Run: git remote add origin [your-repo-url]
3. Run: git push -u origin main

Is there anything else you'd like to do with your project?
```

## Installation

Ask user where to install the skill:
- Local: `./skills/code-creator/`
- Global: `~/.claude/skills/code-creator/`