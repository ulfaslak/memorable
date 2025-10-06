# Documentation Templates

This directory contains template files for generating project-specific documentation in the `/thoughts/` directory.

## Purpose

These templates serve as:
1. **Reference examples** - Show what comprehensive documentation looks like
2. **Structure guides** - Provide consistent format across projects
3. **Starting points** - Can be copied and adapted for new projects

## Templates Available

### PRD Template
- **`PRD_template.md`** - Comprehensive Product Requirements Document template

### Implementation Documentation Templates
- **`implementation_\<n\>_\<feature\>.md`** - Implementation stages, tasks, and progress tracking
- **`architecture_decisions.md`** - ADR (Architecture Decision Record) format
- **`api_contracts.md`** - API endpoints, data models, and interfaces
- **`coding_standards.md`** - Code patterns with examples
- **`project_structure.md`** - File and folder organization
- **`ui_ux.md`** - Design system and UX specifications
- **`bug_tracking.md`** - Error logging and resolution format
- **`git_workflow.md`** - Version control workflow and commit guidelines

### Output Templates (Not Generated as Base Docs)
- **`docs_health_check.md`** - Template for health check reports (created when running documentation verification)

## How They're Used

### PRD Template
When `generate_PRD.mdc` is invoked:
1. AI uses this as a structure guide for comprehensive PRDs
2. User answers ~30 questions about their project
3. AI generates a filled PRD in `/docs/implementation/PRD_0_initial.md`

### Implementation Documentation Templates
When `generate_implementation.mdc` is invoked:
1. AI reads these templates to understand structure and format
2. AI creates **NEW** project-specific files in `/thoughts/`
3. Templates are filled with content from the PRD and architectural decisions
4. Project-specific patterns and decisions replace template examples

## Important Notes

- **These are templates, not project documentation** - Don't edit these for project-specific needs
- **Templates are version-controlled** - They improve across projects
- **Projects get their own copies** - Each project's `/thoughts/` directory is independent
- **Keep templates generic** - They should work for various project types

## Improving Templates

As you work on multiple projects, you may discover:
- Missing sections that should be in every project
- Better ways to structure information
- More helpful examples to include

Update these templates to benefit future projects!

## Usage in Starter Kit

This repo serves as a starter kit for building apps with AI assistance. When starting a new project:

1. **Clone this repository** structure
2. **Generate PRD**: Say "Generate a PRD" → Answer questions → PRD created
3. **Generate implementation**: Say "Generate implementation plan from @PRD_0_initial.md" → 9 doc files created
4. **Begin development**: AI follows workflow rules and established patterns

The templates ensure consistency and completeness across all your AI-assisted projects.

