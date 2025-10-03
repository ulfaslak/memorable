# Thoughts Directory

This directory contains project-specific implementation planning and architectural documentation.

## Purpose

The `/thoughts/` directory serves as a **persistent knowledge base** that survives AI context compression. When building a project with AI assistance, documentation here becomes the source of truth as chat context degrades over time.

## How It Works

1. **Start new project:** AI reads templates from `.cursor/rules/templates/`
2. **Generate docs:** AI creates project-specific documentation here
3. **During development:** AI consults these files before making decisions
4. **Context refresh:** When uncertain, AI re-reads these files
5. **Documentation grows:** Files get updated with project-specific patterns and decisions

## Files Created During Project Setup

When you start a new project using the `generate` rules, the following files will be created:

- **`implementation_0_initial.md`** - Implementation stages, tasks, and current state tracking
- **`architecture_decisions.md`** - Record of WHY architectural decisions were made
- **`api_contracts.md`** - API endpoints, data models, and interface definitions
- **`coding_standards.md`** - Project-specific patterns with examples
- **`project_structure.md`** - File and folder organization guidelines
- **`ui_ux.md`** - Design system, components, and UX flows
- **`bug_tracking.md`** - Error log and resolution documentation

## For New Projects

This directory should be **empty** (except this README) when starting fresh. Documentation will be generated based on your PRD.

## For Existing Projects

If you're adding this system to an existing project:
1. Review templates in `.cursor/rules/templates/`
2. Create project-specific versions of needed documentation
3. Populate with current project patterns and decisions
4. Reference during development and when onboarding AI agents

## Integration with Cursor Rules

The `.cursor/rules/workflow.mdc` file contains rules that instruct AI agents to:
- Consult these files before making decisions
- Update them when patterns change
- Use them as the source of truth when context is lost
- Follow established patterns rather than improvising

## Best Practices

- **Keep documentation updated** as the project evolves
- **Be specific** with examples, not just abstract descriptions
- **Link between docs** to maintain consistency
- **Update "Current Working State"** in implementation_\<n\>_\<feature\>.md regularly
- **Document bugs and solutions** in bug_tracking.md
- **Record WHY, not just what** in architecture_decisions.md

