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

### Option 1: Write Manually

Create a detailed document covering:
- Purpose and vision
- Target users
- Core features and functionality
- User experience flows
- Technical requirements
- Design preferences
- Success metrics

### Option 2: Generate with AI (Recommended)

1. Start a chat with an AI and say:
   > "I am making the following application: <expanded-elevator-pitch>. I want you to generate a highly detailed PRD for the [MVP/feature]. In order to do this, you must first understand the application fully, covering all key aspects of how the application will work, including but not limited to: purpose, UX, design, features, and tech stack. Please quiz me on these details, one question at a time, until you have a complete understanding of the application. Once you have a complete understanding, generate a PRD."

2. Answer the questions thoroughly

3. Paste the generated PRD into `docs/implementation/PRD_<n>_<feature>.md`

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
