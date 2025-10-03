# Documentation Health Check

> **Purpose:** Periodic review to ensure documentation stays accurate and useful.
> **Frequency:** Run after completing each stage or every 2 weeks

---

## Last Health Check
- **Date:** [YYYY-MM-DD]
- **Reviewer:** [AI/Human]
- **Status:** [✅ Healthy / ⚠️ Needs Attention / ❌ Outdated]

---

## Automated Checks

### 1. Architecture Decisions vs Code Reality
**Check:** Do current architectural decisions match actual implementation?

- [ ] Review each decision in `architecture_decisions.md`
- [ ] Verify decision is still followed in codebase
- [ ] Flag any deviations or abandoned patterns

**Findings:**
- [List any mismatches]

---

### 2. API Contracts vs Actual APIs
**Check:** Do documented interfaces match actual code?

- [ ] Review interfaces in `api_contracts.md`
- [ ] Search codebase for actual implementations
- [ ] Verify signatures, types, and return values match

**Findings:**
- [List any mismatches]

**How to Check (AI can run this):**
```bash
# For each interface in api_contracts.md, grep for its usage
grep -r "UserService.findById" src/
grep -r "interface User" src/types/
```

---

### 3. Coding Standards Consistency
**Check:** Is the codebase following documented patterns?

- [ ] Pick 5 random files from each category (components, services, utils)
- [ ] Verify they follow patterns in `coding_standards.md`
- [ ] Check for pattern drift

**Findings:**
- [List any inconsistencies]

---

### 4. Current Working State Accuracy
**Check:** Does "Current Working State" reflect reality?

- [ ] Review each implementation_<n>_<feature>.md
- [ ] Verify checked items are actually complete
- [ ] Check if in-progress items are actually being worked on

**Findings:**
- [List any inaccuracies]

---

### 5. Bug Tracking Relevance
**Check:** Are logged bugs still relevant?

- [ ] Review bugs in `bug_tracking.md`
- [ ] Verify which are resolved but not marked as such
- [ ] Archive old/irrelevant bugs

**Findings:**
- [List bugs to archive]

---

### 6. Project Structure Drift
**Check:** Does actual folder structure match `project_structure.md`?

- [ ] Run `tree` or `ls -R` command
- [ ] Compare with documented structure
- [ ] Note any new folders or reorganization

**Findings:**
- [List structural changes]

**Auto-check command:**
```bash
tree -L 3 -I 'node_modules|dist|build' > /tmp/current_structure.txt
```

---

### 7. Dead Reference Check
**Check:** Are there references to files/functions that no longer exist?

- [ ] Search docs for file paths
- [ ] Verify files still exist
- [ ] Search for function/class names
- [ ] Verify they still exist in codebase

**Findings:**
- [List dead references]

---

### 8. Documentation Completeness
**Check:** Are new features documented?

For each recent feature addition:
- [ ] Is it in an implementation plan?
- [ ] Are new APIs documented in `api_contracts.md`?
- [ ] Are new patterns in `coding_standards.md`?
- [ ] Is UI documented in `ui_ux.md`?

**Findings:**
- [List undocumented features]

---

## Health Score

Calculate based on findings above:

| Category | Status | Weight |
|----------|--------|--------|
| Architecture Decisions | ✅/⚠️/❌ | 15% |
| API Contracts | ✅/⚠️/❌ | 20% |
| Coding Standards | ✅/⚠️/❌ | 15% |
| Working State | ✅/⚠️/❌ | 15% |
| Bug Tracking | ✅/⚠️/❌ | 10% |
| Project Structure | ✅/⚠️/❌ | 10% |
| Dead References | ✅/⚠️/❌ | 10% |
| Completeness | ✅/⚠️/❌ | 5% |

**Overall Health:** [0-100]%

---

## Action Items

Based on findings, create action items:

**High Priority:**
- [ ] [Fix critical mismatch]
- [ ] [Update outdated contract]

**Medium Priority:**
- [ ] [Document new pattern]
- [ ] [Archive resolved bugs]

**Low Priority:**
- [ ] [Minor documentation tweaks]

---

## Next Health Check

**Scheduled for:** [Date]
**Trigger:** [After Stage X completion / 2 weeks from now]

---

## AI Execution Instructions

When human says "Run documentation health check":

1. Read this template
2. For each check, run the verification steps
3. Use `grep`, `codebase_search`, and `read_file` to verify
4. Document findings inline
5. Calculate health score
6. Report results to human
7. Ask if human wants to fix issues now or create tasks

**Example commands AI should run:**
```bash
# Check if User interface matches docs
grep -n "interface User" src/types/user.ts
grep -n "class UserService" src/services/user.service.ts

# Check project structure
tree -L 2 src/

# Find potential dead references (files mentioned in docs)
# (AI would parse docs and check each reference)
```

