# Project Structure

> **Purpose:** Define the file and folder organization for the entire project.

---

## Root Directory Structure

```
project-name/
├── .cursor/              # Cursor IDE configuration
│   └── rules/           # AI agent rules and templates
├── src/                 # Source code
├── public/              # Static assets
├── tests/               # Test files
├── docs/                # Documentation
├── thoughts/            # Implementation planning docs
├── config/              # Configuration files
├── scripts/             # Build and utility scripts
└── [framework-specific] # Additional framework folders
```

---

## Source Code Organization

### Frontend Structure (if applicable)

```
src/
├── components/          # Reusable UI components
│   ├── common/         # Shared components (Button, Input, etc.)
│   ├── layout/         # Layout components (Header, Footer, etc.)
│   └── features/       # Feature-specific components
├── pages/              # Page/route components
├── hooks/              # Custom React hooks (or similar)
├── services/           # API and business logic services
│   ├── api/           # API client functions
│   └── [domain]/      # Domain-specific services
├── utils/              # Utility functions
│   ├── helpers/       # Helper functions
│   └── validators/    # Validation functions
├── types/              # TypeScript type definitions
│   ├── models/        # Data models
│   └── interfaces/    # Interface definitions
├── constants/          # Application constants
├── config/             # Runtime configuration
├── styles/             # Global styles
│   ├── globals.css    # Global CSS
│   └── theme/         # Theme configuration
├── assets/             # Images, fonts, etc.
├── store/              # State management (if applicable)
│   ├── slices/        # Redux slices (or similar)
│   └── actions/       # Action creators
├── contexts/           # React contexts (if applicable)
└── lib/                # Third-party library configurations
```

### Backend Structure (if applicable)

```
src/
├── controllers/        # Request handlers
├── services/           # Business logic
├── repositories/       # Data access layer
├── models/             # Data models/entities
├── middlewares/        # Express/Koa middlewares (or similar)
├── routes/             # API route definitions
├── utils/              # Utility functions
├── config/             # Configuration
├── types/              # TypeScript types
├── validators/         # Input validation schemas
├── database/           # Database-related code
│   ├── migrations/    # Database migrations
│   ├── seeders/       # Database seed data
│   └── config.ts      # Database configuration
└── lib/                # Third-party integrations
```

---

## Configuration Files

### Root Level Configuration

- **`package.json`** - Dependencies and scripts
- **`tsconfig.json`** - TypeScript configuration
- **`.env.example`** - Environment variable template
- **`.env.local`** - Local development environment variables (gitignored)
- **`.gitignore`** - Git ignore patterns
- **`.eslintrc.json`** - ESLint configuration
- **`.prettierrc`** - Prettier configuration
- **`README.md`** - Project overview and setup instructions

### Framework-Specific Config

- **`next.config.js`** - Next.js configuration (if applicable)
- **`vite.config.ts`** - Vite configuration (if applicable)
- **`tailwind.config.js`** - Tailwind CSS configuration (if applicable)

---

## File Naming Conventions

### Components
- **PascalCase** for component files: `UserProfile.tsx`
- **PascalCase** for component folders: `UserProfile/`
- Include tests alongside: `UserProfile.test.tsx`

### Utilities & Services
- **camelCase** for utility files: `formatDate.ts`
- **camelCase** for service files: `userService.ts`
- Group related utilities in folders

### Types & Interfaces
- **PascalCase** for type files: `User.ts`
- Use descriptive names: `UserDTO.ts`, `AuthResponse.ts`

### Constants
- **camelCase** for file names: `apiEndpoints.ts`
- **SCREAMING_SNAKE_CASE** for constant names: `API_BASE_URL`

### Tests
- Same name as file being tested with `.test` or `.spec` suffix
- Example: `userService.ts` → `userService.test.ts`

---

## Module Organization Patterns

### Feature-Based Organization (Alternative)

For larger projects, consider organizing by feature:

```
src/
├── features/
│   ├── auth/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── types/
│   │   └── utils/
│   ├── users/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── types/
│   │   └── utils/
│   └── dashboard/
│       └── ...
├── shared/             # Shared across features
│   ├── components/
│   ├── hooks/
│   └── utils/
└── core/               # Core app functionality
    ├── config/
    ├── lib/
    └── types/
```

---

## Asset Organization

```
public/               # Static assets served directly
├── images/
│   ├── icons/
│   ├── logos/
│   └── backgrounds/
├── fonts/
└── locales/         # i18n translation files (if applicable)
```

```
src/assets/          # Assets imported in code
├── images/
├── icons/
└── videos/
```

---

## Test Organization

```
tests/
├── unit/            # Unit tests
│   ├── components/
│   ├── services/
│   └── utils/
├── integration/     # Integration tests
├── e2e/             # End-to-end tests
├── fixtures/        # Test data fixtures
├── mocks/           # Mock implementations
└── setup.ts         # Test configuration
```

---

## Documentation Organization

```
docs/
├── api/             # API documentation
├── architecture/    # Architecture diagrams and docs
├── deployment/      # Deployment guides
└── user-guide/      # User documentation
```

```
thoughts/            # Development planning (not user-facing)
├── implementation_\<n\>_\<feature\>.md
├── architecture_decisions.md
├── api_contracts.md
├── coding_standards.md
├── project_structure.md  # This file
├── ui_ux.md
└── bug_tracking.md
```

---

## Environment-Specific Files

```
config/
├── development.json
├── staging.json
├── production.json
└── test.json
```

Or use environment variables:
- `.env.development`
- `.env.staging`
- `.env.production`
- `.env.test`

---

## Build & Deployment Structure

```
dist/                # Production build output (gitignored)
build/               # Alternative build folder name
out/                 # Next.js build output

scripts/
├── build.sh         # Build scripts
├── deploy.sh        # Deployment scripts
└── seed-db.js       # Database seeding scripts
```

---

## Import Path Aliases

Configure path aliases in `tsconfig.json`:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"],
      "@components/*": ["src/components/*"],
      "@services/*": ["src/services/*"],
      "@utils/*": ["src/utils/*"],
      "@types/*": ["src/types/*"],
      "@hooks/*": ["src/hooks/*"]
    }
  }
}
```

Usage:
```typescript
import { Button } from '@components/common/Button';
import { userService } from '@services/user.service';
```

---

## Notes

- Adjust structure based on specific framework requirements
- Keep related files close together
- Use barrel exports (index.ts) for cleaner imports
- Document deviations from this structure in architecture_decisions.md
- Update this file as the project structure evolves

