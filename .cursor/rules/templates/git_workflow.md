# Git Workflow

> **Purpose:** Define how version control is handled during AI-assisted development
>
> **Recommended Default:** Feature Branch Workflow (safe, professional, works for all project types)

---

## Branching Strategy

**Default approach: Feature branches for all new work**

### Branch Types

**`main`** - Production-ready code
- Always stable and tested
- Protected branch (requires review if working in team)
- Direct commits only for hotfixes

**`feature/<task-name>`** - Feature development
- Created by AI for each major task or stage
- Named after the task from implementation plan
- Examples: `feature/user-authentication`, `feature/stage-1-foundation`

**`fix/<issue-name>`** - Bug fixes
- Created for bugs from bug_tracking.md
- Named after the bug
- Examples: `fix/login-error`, `fix/memory-leak`

---

## Commit Guidelines

### Commit Message Format

```
<type>: <description>

[optional body]

[optional footer]
```

**Types:**
- `feat:` New feature
- `fix:` Bug fix
- `refactor:` Code change that neither fixes a bug nor adds a feature
- `docs:` Documentation changes
- `test:` Adding or updating tests
- `style:` Formatting, missing semicolons, etc.
- `chore:` Maintenance tasks, dependency updates

### Good Commit Messages

✅ **Good:**
```
feat: implement user authentication

- Add login/logout endpoints
- Implement JWT token generation
- Add session management
- Tests included

Completes Stage 2, Task 3 from implementation_0_initial.md
```

❌ **Bad:**
```
update stuff
fixed things
wip
```

---

## AI Commit Behavior

### Default Mode: Feature Branch Workflow ✅ Recommended

**This is the standard workflow for all projects unless you specify otherwise.**

**AI will automatically:**
1. ✅ Create feature branches for new work
2. ✅ Commit after each completed subtask
3. ✅ Write descriptive commit messages
4. ✅ Reference implementation plan tasks
5. ✅ Run tests before committing (if configured)

**AI will NOT (without explicit permission):**
1. ❌ Merge to main
2. ❌ Force push
3. ❌ Delete branches
4. ❌ Rewrite history on shared branches
5. ❌ Push to main directly

### When AI Commits

**Automatic commits after:**
- [ ] Completing a subtask from implementation plan
- [ ] Fixing a bug from bug_tracking.md
- [ ] All tests pass
- [ ] No linter errors

**Commit checklist:**
```bash
# Before committing, AI verifies:
1. Tests pass (npm test)
2. No linter errors (npm run lint)
3. Code follows patterns in coding_standards.md
4. Task is marked complete in implementation file
```

### Workflow Example

```bash
# AI starts new task
AI: "Starting Stage 2, Task 1: User Authentication"
AI: git checkout -b feature/user-authentication

# AI implements feature
[... coding ...]

# AI commits after completing subtask
AI: git add src/services/auth.service.ts src/services/auth.service.test.ts
AI: git commit -m "feat: add authentication service with JWT tokens

- Implement login/register methods
- Add JWT token generation
- Include unit tests
- Handle errors gracefully

Completes Stage 2, Task 1.1 from implementation_0_initial.md"

# AI continues with next subtask
[... more work ...]

# AI makes another commit
AI: git commit -m "feat: add login UI component

- Create LoginForm component
- Add form validation
- Connect to auth service
- Include tests

Completes Stage 2, Task 1.2 from implementation_0_initial.md"

# After all subtasks complete
AI: "Feature complete. Ready to merge to main?"
```

---

## Human Approval Points

### When Human Must Approve

**Before merging to main:**
- Human reviews the code
- Human approves and merges
- Or human says: "merge to main"

**For risky operations:**
- Force push
- Rewriting history
- Deleting branches
- Direct push to main

### Quick Commands

```bash
# Human can say:
"commit this"                    # AI commits current work
"create feature branch for X"    # AI creates branch
"merge to main"                  # AI merges (after confirmation)
"push branch"                    # AI pushes current branch
"create PR"                      # AI creates pull request (if GitHub)
```

---

## Pull Request Workflow (Optional)

If using GitHub/GitLab and want PR workflow:

### AI Can:
1. ✅ Create draft PR after stage completion
2. ✅ Fill PR description with:
   - What was implemented
   - Which tasks completed
   - How to test
   - References to documentation
3. ✅ Request review

### PR Template

```markdown
## Description
Implements Stage 2 (Core Features) from implementation_0_initial.md

## Changes
- ✅ User authentication system
- ✅ Session management  
- ✅ Login/logout endpoints
- ✅ JWT token handling

## Testing
- [x] All unit tests pass (42 tests)
- [x] Manual testing completed
- [x] No linter errors

## Documentation
- Updated api_contracts.md with auth endpoints
- Added patterns to coding_standards.md
- Updated implementation_0_initial.md progress

## Checklist
- [x] Tests included
- [x] Documentation updated
- [x] Follows coding standards
- [x] No breaking changes
```

---

## Alternative: Direct-to-Main Workflow

⚠️ **Use only for rapid solo prototyping. Feature branches are recommended for all other cases.**

For very early prototypes where you want maximum speed:

**Enable by telling AI:**
> "Use direct-to-main workflow. Commit directly to main after each completed task."

**AI will then:**
1. ✅ Commit directly to main after each subtask
2. ✅ Verify tests pass first
3. ✅ Push automatically (optional)

**Only use for:**
- Very early prototypes (first few days)
- Solo experimentation
- Throwaway code

**NOT recommended for:**
- Team projects
- Production applications
- Any code you want to maintain long-term
- Projects with CI/CD pipelines

**Consider switching to Feature Branch workflow once the project becomes real.**

---

## Git Ignore

Essential files to ignore:

```gitignore
# Dependencies
node_modules/
venv/
.env
.env.local

# Build outputs
dist/
build/
.next/
out/

# IDE
.vscode/
.idea/
*.swp
*.swo

# OS
.DS_Store
Thumbs.db

# Logs
*.log
npm-debug.log*

# Testing
coverage/
.nyc_output/

# Keep thoughts directory!
# Do NOT ignore /thoughts/ - it should be version controlled
```

---

## Best Practices

### Commit Often
- Small, focused commits are better than large ones
- Each commit should represent one logical change
- Easier to review and revert if needed

### Meaningful Messages
- Describe *why*, not just *what*
- Reference task from implementation plan
- Include context for future developers

### Keep Main Stable
- Only merge tested, working code
- Run full test suite before merging
- Consider CI/CD to enforce this

### Version Control Documentation
- ✅ **DO** commit `/thoughts/` directory
- ✅ **DO** commit implementation plans
- ✅ **DO** commit architectural docs
- ❌ **DON'T** commit `.env` files
- ❌ **DON'T** commit `node_modules`
- ❌ **DON'T** commit build artifacts

---

## Handling Conflicts

If AI encounters merge conflicts:

1. **AI alerts human:** "Merge conflict detected in file X"
2. **Human resolves** or asks AI to resolve
3. **AI can:** Attempt automatic resolution for simple conflicts
4. **AI cannot:** Make architectural decisions during conflicts

---

## Project-Specific Settings

**Current Project Configuration:**

- **Branch Strategy:** Feature Branch (default)
- **Commit Approval:** Automatic on feature branches
- **Push Behavior:** On request (AI asks first)
- **PR Required:** Recommended (manual merge to main)
- **Protected Branches:** main

> **Note:** This is the recommended safe default. You can customize by telling the AI to change settings.

**To change settings, tell AI:**
```
"Switch to direct-to-main workflow"
"Require manual approval for commits"
"Auto-push after commits"
```

---

## Git Workflow Checklist

**When starting new task:**
- [ ] Create feature branch (or stay on main)
- [ ] Verify on correct branch

**When completing subtask:**
- [ ] Run tests
- [ ] Fix linter errors
- [ ] Stage relevant files
- [ ] Write descriptive commit message
- [ ] Commit

**When completing stage:**
- [ ] Push branch (if using branches)
- [ ] Create PR (if using PR workflow)
- [ ] Request review (if team)
- [ ] Merge to main after approval

**Daily maintenance:**
- [ ] Pull latest changes
- [ ] Resolve any conflicts
- [ ] Keep feature branches up to date with main

