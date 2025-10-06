# Documentation Directory

This directory contains Product Requirements Documents (PRDs) that specify what should be built.

## Structure

```
docs/
├── README.md              ← This file
└── implementation/        ← PRD storage
    ├── PRD_0_initial.md         ← Initial MVP requirements (human-provided)
    ├── PRD_1_<feature>.md       ← Feature expansion (future, human-provided)
    └── PRD_n_<feature>.md       ← More expansions (future, human-provided)
```

## Purpose

### `/implementation/` Directory

Contains PRDs that describe **what to build**. These are human-created documents that specify:
- Product vision and goals
- User stories and use cases
- Features and functionality
- UI/UX requirements
- Technical constraints
- Success criteria

Each PRD is transformed by the AI into an implementation plan (stored in `/thoughts/`).

## Naming Convention

**Format:** `PRD_<n>_<feature>.md`

- `<n>` is a sequential number starting from 0
- `<feature>` is a short, descriptive name
- `PRD_0_initial.md` is always the MVP/initial implementation

**Examples:**
- `PRD_0_initial.md` - The MVP requirements
- `PRD_1_payments.md` - Payment feature expansion
- `PRD_2_notifications.md` - Notification system expansion
- `PRD_3_analytics.md` - Analytics dashboard expansion

## How PRDs Become Implementation Plans

1. **Human creates PRD** in `docs/implementation/PRD_<n>_<feature>.md`
2. **Human triggers generation** in Cursor: "Generate implementation plan from PRD_<n>_<feature>"
3. **AI transforms PRD** into detailed implementation documentation in `/thoughts/`
4. **AI builds from plan** following the generated documentation

## Creating a PRD

### Option 1: Use Built-in PRD Generator (Recommended)

**For initial MVP (PRD_0_initial.md):**

In Cursor, say:
```
"Generate a PRD"
```

The AI will:
- Interview you with ~30 detailed questions (one at a time)
- Cover all aspects: features, UX, tech stack, data models, APIs, security, testing, deployment
- Generate a comprehensive PRD saved to `docs/implementation/PRD_0_initial.md`

**For feature expansions (PRD_1_feature.md, PRD_2_feature.md, etc.):**

Same process, but focus questions on the new feature and how it integrates with existing functionality.

### Option 2: Use Template

Use `.cursor/rules/templates/PRD_template.md` as a guide and fill in all sections with your project details.

### Option 3: Write from Scratch

Create a detailed document covering:
- Purpose and vision
- Target users
- Core features and functionality
- User experience flows
- Technical requirements
- Design preferences
- Success metrics
- Data models and APIs
- Security and compliance
- Testing and deployment

## Best Practices

- **Be detailed** - The more detail in the PRD, the better the implementation plan
- **Include examples** - Show what you mean with mockups, user flows, etc.
- **Specify constraints** - Technical limitations, budget, timeline
- **Define success** - What does "done" look like?
- **Incremental PRDs** - For feature expansions, focus on the new features and how they integrate with existing functionality

## What Happens Next

After creating a PRD here, use Cursor to generate the implementation plan:

```
"Generate implementation plan from @PRD_<n>_<feature>.md"
```

This creates:
- Implementation file in `/thoughts/implementation_<n>_<feature>.md`
- Updates to architectural documentation in `/thoughts/`
- Task tracking with checkboxes
- Clear dependencies on previous implementations

See the main README.md in the repo root for complete usage instructions.
