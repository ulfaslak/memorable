# Documentation Health Check Command

## When to Use This Command

**Recommended frequency:**
- After completing each implementation stage
- Every 2 weeks during active development
- Before starting a new feature expansion
- When noticing documentation drift

---

## Execution Protocol

When triggered, perform the following checks systematically:

### 1. Architecture Decisions Verification
**Goal:** Ensure documented decisions match actual implementation

**Steps:**
1. Read `/thoughts/architecture_decisions.md`
2. For each decision, use `codebase_search` to verify pattern is followed
3. Flag any deviations

**Example:**
```
Decision says: "Using repository pattern for data access"
Verify: Search for repositories in codebase, check if pattern is used
```

### 2. API Contracts Verification
**Goal:** Ensure documented interfaces match actual code

**Steps:**
1. Read `/thoughts/api_contracts.md`
2. For each interface/model, use `grep` to find actual definitions
3. Compare documented vs actual signatures
4. Report mismatches

**Example:**
```typescript
// Documented in api_contracts.md
interface User {
  id: string;
  name: string;
  email: string;
}

// Search and verify
grep -A 5 "interface User" src/types/user.ts
```

### 3. Coding Standards Compliance
**Goal:** Verify codebase follows documented patterns

**Steps:**
1. Read `/thoughts/coding_standards.md`
2. Select 5 random files from each category
3. Check if they follow documented patterns
4. Report pattern drift

**Tool:** Use `codebase_search` and `read_file`

### 4. Current Working State Accuracy
**Goal:** Ensure implementation progress tracking is accurate

**Steps:**
1. Read each `implementation_<n>_<feature>.md`
2. Check "Current Working State" section
3. For items marked "✅ Completed", spot-check that they actually work
4. Flag any inaccuracies

### 5. Bug Tracking Relevance
**Goal:** Clean up resolved bugs

**Steps:**
1. Read `/thoughts/bug_tracking.md`
2. For each open bug, check if still relevant
3. Suggest archiving resolved bugs

### 6. Project Structure Alignment
**Goal:** Ensure folder structure matches docs

**Steps:**
1. Read `/thoughts/project_structure.md`
2. Run `list_dir` to see actual structure
3. Compare and note differences
4. Update docs if structure has evolved intentionally

### 7. Dead Reference Detection
**Goal:** Find references to non-existent files/functions

**Steps:**
1. Extract file paths and function names from all `/thoughts/*.md` files
2. Use `read_file` to verify they exist
3. Report dead references

### 8. Documentation Completeness
**Goal:** Ensure new features are documented

**Steps:**
1. Check recent git history or implementation progress
2. For each new feature, verify it's documented in:
   - `implementation_<n>_<feature>.md` (task)
   - `api_contracts.md` (if it has APIs)
   - `coding_standards.md` (if it introduces new patterns)
   - `ui_ux.md` (if it has UI)

---

## Reporting Format

After performing all checks, create a report in `/thoughts/docs_health_check.md`:

```markdown
# Documentation Health Check Report

**Date:** 2025-10-03
**Triggered by:** [Human/Stage completion]

## Executive Summary
Overall Health: 85/100 ⚠️

## Findings

### ✅ Healthy
- API Contracts: All interfaces match code
- Bug Tracking: Up to date

### ⚠️ Needs Attention  
- Architecture Decisions: Repository pattern not used in PaymentService
- Coding Standards: 3/10 files missing proper error handling

### ❌ Critical Issues
- Dead Reference: `UserProfile.tsx` mentioned in ui_ux.md doesn't exist

## Recommended Actions

**High Priority:**
1. Fix PaymentService to use repository pattern
2. Remove reference to non-existent UserProfile.tsx

**Medium Priority:**
1. Add error handling to 3 files flagging pattern violations
2. Update coding_standards.md with more examples

## Next Check
**Scheduled:** 2025-10-17 (2 weeks)
```

---

## After Health Check

1. **Report findings to user**
2. **Ask if they want to:**
   - Fix issues immediately
   - Create tasks for later
   - Ignore certain findings (with reason)
3. **Update `/thoughts/docs_health_check.md`**
4. **Set reminder for next check**

---

## Integration with Workflow

Add this reminder to implementation templates:

> **📋 Documentation Health Reminder**
> After completing this stage, run: "Check documentation health"

---

## Example Usage

```
Human: "Run documentation health check"

AI: 
1. [Reads all documentation files]
2. [Performs 8 verification checks]
3. [Generates health report]
4. [Presents findings]
5. "I found 3 issues: 
   - ⚠️ User interface in api_contracts.md is outdated
   - ✅ All patterns in coding_standards.md are followed
   - ❌ Dead reference to removed component
   
   Would you like me to fix these now?"
```

---

## Automation Potential

**For true background checks**, add to project:

Create `.github/workflows/docs-health.yml` (for GitHub Actions):
```yaml
name: Weekly Docs Health Check
on:
  schedule:
    - cron: '0 9 * * 1'  # Every Monday at 9am
  workflow_dispatch:

jobs:
  health-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Check for dead references
        run: |
          # Add script to check file references
          ./scripts/check-docs-health.sh
      - name: Create issue if problems found
        run: |
          # Create GitHub issue with findings
```

Or use a simpler `package.json` script:
```json
{
  "scripts": {
    "docs:check": "node scripts/check-docs-health.js"
  }
}
```

Then run manually: `npm run docs:check`

---

## Notes

- This check is semi-automated (AI-assisted, human-triggered)
- For full automation, would need separate tooling
- The more specific your documentation, the easier to verify
- Health checks become more valuable as project grows
