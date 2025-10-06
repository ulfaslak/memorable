# AI-Assisted Development Starter Kit

A comprehensive framework for building applications with AI assistance that maintains code quality throughout the entire development lifecycle.

## The Problem This Solves

When building projects with AI coding assistants, everything starts well. But as the context window fills up and chat history gets compressed, the AI starts:
- Forgetting architectural decisions
- Hallucinating APIs that don't exist
- Breaking established patterns
- Making the same mistakes repeatedly
- Writing inconsistent code

**This starter kit solves that problem.**

## How It Works

The key insight: **Chat context degrades, but documentation files persist.**

This starter kit uses Cursor's rules system to:
1. **Generate comprehensive documentation** from your PRD
2. **Force AI agents to consult documentation** before making decisions
3. **Maintain a persistent knowledge base** that survives context compression
4. **Establish clear patterns** with concrete examples
5. **Track what's working** vs what's not started

## Project Structure

```
your-project/
├── .cursor/
│   ├── rules/
│   │   ├── workflow.mdc                        # Always-on development rules
│   │   ├── generate_PRD.mdc                    # Interactive PRD generator
│   │   ├── generate_implementation.mdc         # PRD → documentation generator
│   │   └── templates/                          # Documentation templates
│   │       ├── implementation_\<n\>_\<feature\>.md
│   │       ├── architecture_decisions.md
│   │       ├── api_contracts.md
│   │       ├── coding_standards.md
│   │       ├── project_structure.md
│   │       ├── ui_ux.md
│   │       ├── bug_tracking.md
│   │       └── git_workflow.md
│   └── commands/
│       └── healthcheck.md                      # Documentation health check
├── .github/
│   └── workflows/                              # CI/CD workflows (optional)
├── docs/
│   └── implementation/                         # PRD storage
│       ├── PRD_0_initial.md                   # Initial MVP requirements
│       ├── PRD_1_<feature>.md                 # Feature expansion (future)
│       └── PRD_n_<feature>.md                 # More expansions (future)
├── thoughts/                                   # Project-specific documentation
│   ├── implementation_0_initial.md            # Generated from PRD_0
│   ├── implementation_\<n\>_\<feature\>.md        # Generated from PRD_<n> (future)
│   ├── architecture_decisions.md              # Generated initially, grows over time
│   ├── api_contracts.md                       # Generated initially, grows over time
│   ├── coding_standards.md                    # Generated initially, grows over time
│   ├── project_structure.md                   # Generated initially, updated as needed
│   ├── ui_ux.md                               # Generated initially, updated as needed
│   ├── bug_tracking.md                        # Generated initially, populated during dev
│   └── README.md                              # Explains the directory
└── README.md                                   # This file
```

## Getting Started

### 1. Clone This Repository

```bash
git clone <this-repo-url> your-project-name
cd your-project-name
```

### 2. Create Your Initial PRD

**Option A: Use Built-in PRD Generator (Recommended)**

In Cursor, start a chat and say:

> "Generate a PRD"

The AI will:
- Quiz you with detailed questions about your app (one at a time)
- Cover: features, UX, tech stack, data models, APIs, security, etc.
- Generate a comprehensive PRD in `docs/implementation/PRD_0_initial.md`

This takes 5-10 minutes but produces a highly detailed specification.

**Option B: Write Manually**

Use the template at `.cursor/rules/templates/PRD_template.md` and fill it in with your project details.

### 3. Generate Documentation

In Cursor, start a chat and say:

> "Generate the implementation plan and all documentation from `@PRD_0_initial.md`"

The AI will:
- Read PRD_0_initial.md
- Research appropriate tech stack
- Create comprehensive documentation in `/thoughts/`
- Set up the project structure
- Define architectural patterns
- Document APIs and data models
- Establish coding standards

This creates **8 documentation files**:
- `implementation_0_initial.md` - MVP task tracking
- `architecture_decisions.md` - Why decisions were made
- `api_contracts.md` - API schemas and interfaces
- `coding_standards.md` - Code patterns with examples (includes testing)
- `project_structure.md` - File organization
- `ui_ux.md` - Design system
- `bug_tracking.md` - Error logging template
- `git_workflow.md` - Version control workflow

### 4. Start Building

Now just start building! The `workflow.mdc` rules are always active, so the AI will:
- Consult documentation before making decisions
- Follow established patterns
- Update documentation as it learns
- Track progress in `implementation_\<n\>_\<feature\>.md`
- Document bugs and solutions
- Maintain consistency

### 5. Context Refresh (When Needed)

If you notice the AI forgetting patterns or making mistakes:

> "Trigger context refresh protocol"

The AI will re-read all documentation and get back on track.

## Table of Contents

1. [Quick Start](#getting-started)
2. [Documentation System](#the-documentation-system)
3. [Daily Workflow](#daily-workflow)
4. [Adding Features](#adding-features-iteratively)
5. [Rules System](#the-rules-system)
6. [Troubleshooting](#troubleshooting)
7. [Advanced Usage](#advanced-usage)

---

## The Documentation System

### `/thoughts/` Directory

This is your **persistent knowledge base**. It contains:

#### `implementation_\<n\>_\<feature\>.md` (Multiple Files)
- **implementation_0_initial.md** - MVP implementation tracking
- **implementation_1_<feature>.md** - First feature expansion
- **implementation_2_<feature>.md** - Second feature expansion
- Each tracks its own features, stages, and progress
- Later implementations can depend on earlier ones
- **Current Working State** - what's done, in progress, not started

#### `architecture_decisions.md`
- **WHY** decisions were made (not just what)
- Framework/library choices with rationale
- Architectural patterns (repository, MVC, etc.)
- Alternatives considered and rejected
- Consequences and trade-offs

#### `api_contracts.md`
- Data models with TypeScript interfaces
- API endpoint schemas
- Service interface definitions
- Component prop types
- Database schemas
- Validation rules

**Prevents API hallucination!**

#### `coding_standards.md`
- File naming conventions
- Code patterns with ❌ Bad and ✅ Good examples
- Error handling patterns
- Component structure templates
- Import ordering
- Testing patterns

**Maintains consistency!**

#### `project_structure.md`
- Folder hierarchy
- File organization patterns
- Import path aliases
- Module organization

#### `ui_ux.md`
- Design system (colors, typography, spacing)
- Component guidelines
- User flows
- Responsive breakpoints
- Accessibility requirements

#### `bug_tracking.md`
- Error logs
- Root cause analysis
- Solutions and prevention
- Common error patterns

## The Rules System

### `workflow.mdc` (Always Active)

Guides AI through development:
- **Before tasks:** Check active implementation file for current stage
- **Before coding:** Verify patterns in architecture_decisions.md and coding_standards.md
- **Before APIs:** Check api_contracts.md
- **Before UI:** Consult ui_ux.md
- **Before structure changes:** Check project_structure.md
- **Before marking complete:** Verify completion checklist
- **When uncertain:** Trigger context refresh
- **Multiple implementations:** Handles dependencies between feature sets

### `generate_PRD.mdc` (Manual Activation)

Interactive quiz that generates a comprehensive PRD through Socratic questioning.

**Usage:**
- Say: "Generate a PRD" or "Create a product requirements document"
- AI asks questions one at a time about your app
- Covers: features, UX, tech stack, data models, APIs, etc.
- Generates detailed PRD in `docs/implementation/PRD_0_initial.md`

### `generate_implementation.mdc` (Manual Activation)

**Two Modes:**
1. **Initial Setup (Mode 1):** Creates all base docs + implementation_0_initial.md
2. **Feature Expansion (Mode 2):** Creates implementation_\<n\>_\<feature\>.md + updates base docs

Used whenever you have a PRD to transform into an implementation plan.

---

## Daily Workflow

### Starting Work

```
"What's the next task in implementation_0_initial?"
```

Or for a specific feature:
```
"Work on payments feature"
```

The AI will:
1. Read the implementation file
2. Find next unchecked task
3. Check dependencies
4. Tell you what to build

### During Implementation

The AI **automatically**:
- ✅ Checks architecture_decisions.md for WHY patterns exist
- ✅ Checks coding_standards.md for HOW to write code
- ✅ Checks api_contracts.md for interface definitions
- ✅ Checks ui_ux.md for design specifications
- ✅ Checks project_structure.md for where files go
- ✅ Checks bug_tracking.md for known issues

### When AI Seems Lost

```
"Trigger context refresh protocol"
```

AI will re-read all documentation and get back on track.

### Documenting Bugs

```
"Document this bug in bug_tracking.md with root cause and solution"
```

### Completing Tasks

AI will automatically:
1. Change `- [ ] Task` to `- [x] Task` in implementation file
2. Update "Current Working State" section
3. Move to next task

---

## Best Practices

### During Development

1. **Update "Current Working State"** regularly in active implementation file
2. **Document bugs immediately** in `bug_tracking.md`
3. **Record new patterns** in `coding_standards.md` when established
4. **Update API contracts** when adding new endpoints/models
5. **Document major decisions** in `architecture_decisions.md`
6. **Check dependencies** before starting new implementations

### Adding Features Iteratively

1. **Build MVP first** using implementation_0_initial.md
2. **When ready for expansion:**
   - Create `docs/implementation/PRD_1_<feature>.md`
   - Say: "Generate implementation plan from PRD_1_<feature>"
   - Build using the new implementation file
3. **Repeat** for each feature expansion

### When AI Gets Lost

If the AI starts making mistakes:

1. Ask it to "trigger context refresh"
2. Point it to specific documentation: "Check coding_standards.md for our error handling pattern"
3. Specify which implementation you're working on: "We're on implementation_1_payments"
4. Update documentation if patterns have evolved
5. Be specific: "This breaks the pattern in coding_standards.md section X"

### Growing Your Documentation

As your project evolves:
- Add more examples to `coding_standards.md`
- Document common bugs in `bug_tracking.md`
- Add new architectural decisions
- Expand API contracts
- Update UI/UX patterns

The richer the documentation, the better the AI performs late in the project.

## Why This Works

Traditional AI coding:
```
Human → AI (with degrading chat context) → Code
```

This system:
```
Human → AI → Reads persistent docs → Code
                ↓
         Updates docs for next time
```

The documentation acts as a **stable memory system** that doesn't degrade like chat context.

## Using This as a Template

This repo is designed to be cloned for each new project:

1. Clone → New project folder
2. Replace PRD → Your project requirements
3. Generate docs → AI creates project-specific documentation
4. Build → AI follows your project's patterns
5. (Optional) Improve templates → Better for next project

## Advanced Usage

### Multi-Stage Projects

For large projects, work through stages sequentially:
1. Complete Stage 1 (Foundation)
2. Update "Current Working State" in implementation_\<n\>_\<feature\>.md
3. Start Stage 2
4. Repeat

### Team Projects

- Commit `/thoughts/` to version control
- Team members' AI assistants read the same documentation
- Everyone follows the same patterns
- Onboarding is faster

### Continuous Improvement

As you build multiple projects:
- Improve templates in `.cursor/rules/templates/`
- Add sections that were missing
- Better examples
- Clearer instructions

Each project gets better than the last.

### Switching Between Features

```bash
# Work on specific feature
"Work on payments"

# Check status of all implementations
"What implementations exist and what's their status?"

# Continue where you left off
"What should I work on next?"
```

---

## Common Scenarios

### Scenario: Starting Fresh
```
You: "What should I build first?"
AI: [Reads implementation_0_initial.md]
AI: "Stage 1, Task 1: Set up development environment..."
```

### Scenario: AI Breaks Pattern
```
You: "This doesn't follow the pattern in coding_standards.md section 'Error Handling'"
AI: [Re-reads coding_standards.md]
AI: [Fixes code to match the ✅ Good example]
```

### Scenario: Completing a Feature
```
You: "Authentication is complete and tested. Mark it complete."
AI: [Updates checkbox and Current Working State]
```

### Scenario: After Long Break
```
You: "Trigger context refresh. What's the current state?"
AI: "Implementation 0 (MVP) is 60% complete. Stage 2/4. Next task: Implement user profile management."
```

### Scenario: Adding Feature After MVP
```
You: [Creates PRD_2_notifications.md]
You: "Generate implementation plan from PRD_2_notifications"
AI: [Creates implementation_2_notifications.md]
You: "Start working on notifications"
```

---

## File Reference Guide

| When You Need To... | Check This File |
|---------------------|----------------|
| See what to build next (MVP) | `implementation_0_initial.md` |
| See what to build next (feature) | `implementation_<n>_<feature>.md` |
| Understand why a decision was made | `architecture_decisions.md` |
| Check an API signature or data model | `api_contracts.md` |
| See the code pattern to follow | `coding_standards.md` |
| Know where files should go | `project_structure.md` |
| Check design specs or UI components | `ui_ux.md` |
| See if bug was encountered before | `bug_tracking.md` |
| Understand git/commit workflow | `git_workflow.md` |
| Verify documentation accuracy | Run "Check documentation health" |

---

## Troubleshooting

### Problem: AI ignores the rules
**Solution:**
- Verify `workflow.mdc` has `alwaysApply: true` in the header
- Check that documentation exists in `/thoughts/`
- Try explicit instruction: "Follow the workflow rules"
- Trigger context refresh

### Problem: AI hallucinates APIs
**Solution:**
- Ensure `api_contracts.md` is up to date
- Tell AI explicitly: "Check api_contracts.md for the User interface"

### Problem: AI uses inconsistent patterns
**Solution:**
- Add clear examples to `coding_standards.md`
- Use ❌ Bad and ✅ Good format
- Point AI to specific section: "Check coding_standards.md section X"

### Problem: AI forgets architectural decisions
**Solution:**
- Document the decision in `architecture_decisions.md`
- Trigger context refresh: "Trigger context refresh protocol"

### Problem: AI doesn't check off completed tasks
**Solution:**
- Explicitly ask: "Mark task X as complete and update Current Working State"
- Remind: "Use search_replace to change the checkbox"

### Problem: Working on wrong implementation
**Solution:**
- Specify which one: "Work on implementation_1_payments"
- Or: "Work on payments feature"

### Problem: Documentation is outdated
**Solution:**
- Update relevant docs
- Tell AI: "We've changed the pattern, update coding_standards.md"
- Keep docs in sync with reality

## Contributing

If you improve the templates or rules, consider:
1. Testing across multiple project types
2. Documenting the improvement
3. Sharing back to the community

## License

[Your License Here]

## Credits

Built for developers frustrated with late-stage AI coding quality degradation.

---

**Remember:** The documentation is your source of truth. Keep it updated, and your AI assistant will maintain quality throughout the entire project lifecycle.

