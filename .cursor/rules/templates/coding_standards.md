# Coding Standards & Patterns

> **Purpose:** Document project-specific patterns and conventions with concrete examples to maintain consistency.
>
> **Note:** This template shows React/TypeScript examples. When generating project documentation, the AI will replace ALL code examples with the actual language/framework from your PRD (Python, Go, Rust, etc.). The structure stays the same, but syntax will match your tech stack.

---

## File Organization

### Naming Conventions
- **Components:** PascalCase - `UserProfile.tsx`
- **Utilities:** camelCase - `formatDate.ts`
- **Hooks:** camelCase with 'use' prefix - `useAuth.ts`
- **Constants:** SCREAMING_SNAKE_CASE - `API_BASE_URL`
- **Types/Interfaces:** PascalCase - `UserDTO.ts`

### Directory Structure
```
src/
├── components/     # React components
├── hooks/          # Custom React hooks
├── services/       # Business logic & API calls
├── utils/          # Pure utility functions
├── types/          # TypeScript type definitions
├── constants/      # App constants
└── pages/          # Page components (routing)
```

---

## Code Patterns

### Error Handling

#### ❌ Bad - Generic catch-all
```typescript
try {
  await fetchUser(id);
} catch (error) {
  console.log('error');
}
```

#### ✅ Good - Specific error handling
```typescript
try {
  const user = await userService.findById(id);
  if (!user) {
    throw new NotFoundError(`User ${id} not found`);
  }
  return user;
} catch (error) {
  if (error instanceof NotFoundError) {
    logger.warn('User not found', { userId: id });
    throw error;
  }
  logger.error('Failed to fetch user', { error, userId: id });
  throw new DatabaseError('Failed to fetch user');
}
```

---

### Async/Await Pattern

#### ❌ Bad - Mixed promises and async
```typescript
const data = fetchData().then(result => {
  return processData(result);
});
```

#### ✅ Good - Consistent async/await
```typescript
const data = await fetchData();
const processed = await processData(data);
return processed;
```

---

### Component Structure

#### ✅ Standard Component Format
```typescript
// 1. Imports
import React, { useState, useEffect } from 'react';
import { UserService } from '@/services/user.service';
import { Button } from '@/components/Button';

// 2. Types
interface UserProfileProps {
  userId: string;
}

// 3. Component
export const UserProfile: React.FC<UserProfileProps> = ({ userId }) => {
  // 3a. Hooks
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);

  // 3b. Effects
  useEffect(() => {
    loadUser();
  }, [userId]);

  // 3c. Handlers
  const loadUser = async () => {
    try {
      const data = await UserService.findById(userId);
      setUser(data);
    } catch (error) {
      console.error('Failed to load user', error);
    } finally {
      setLoading(false);
    }
  };

  // 3d. Render
  if (loading) return <div>Loading...</div>;
  if (!user) return <div>User not found</div>;

  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  );
};
```

---

### Import Order

```typescript
// 1. External libraries
import React from 'react';
import { useQuery } from 'react-query';

// 2. Internal services/utils
import { userService } from '@/services/user.service';
import { formatDate } from '@/utils/date';

// 3. Components
import { Button } from '@/components/Button';

// 4. Types
import type { User } from '@/types/user';

// 5. Styles
import styles from './UserProfile.module.css';
```

---

## State Management

### Pattern: [Define your state management approach]

#### ❌ Bad
```typescript
// Example of what NOT to do
```

#### ✅ Good
```typescript
// Example of correct pattern
```

---

## API Calls

### Pattern: Service Layer

#### ✅ Services handle all API logic
```typescript
// services/user.service.ts
export class UserService {
  private static baseUrl = '/api/users';

  static async findById(id: string): Promise<User> {
    const response = await fetch(`${this.baseUrl}/${id}`);
    if (!response.ok) {
      throw new Error('Failed to fetch user');
    }
    return response.json();
  }
}
```

#### ✅ Components use services
```typescript
// components/UserProfile.tsx
const loadUser = async () => {
  const user = await UserService.findById(userId);
  setUser(user);
};
```

---

## Testing Patterns

### Testing Philosophy
- **Write tests alongside implementation**, not as an afterthought
- **Test behavior, not implementation details**
- **Each feature should have tests before being marked complete**
- Aim for high coverage on business logic, moderate on UI

### Test File Organization
```
src/
├── services/
│   ├── user.service.ts
│   └── user.service.test.ts       # Co-located with source
├── components/
│   ├── UserProfile.tsx
│   └── UserProfile.test.tsx
└── utils/
    ├── validation.ts
    └── validation.test.ts
```

### Unit Test Structure (Arrange-Act-Assert)

#### ✅ Good - Clear AAA pattern
```typescript
describe('UserService', () => {
  describe('findById', () => {
    it('should return user when found', async () => {
      // Arrange
      const userId = '123';
      const mockUser = { id: userId, name: 'Test' };
      jest.spyOn(api, 'get').mockResolvedValue(mockUser);
      
      // Act
      const user = await UserService.findById(userId);
      
      // Assert
      expect(user).toEqual(mockUser);
      expect(api.get).toHaveBeenCalledWith('/users/123');
    });

    it('should throw NotFoundError when user does not exist', async () => {
      // Arrange
      jest.spyOn(api, 'get').mockRejectedValue(new Error('404'));
      
      // Act & Assert
      await expect(UserService.findById('999'))
        .rejects
        .toThrow(NotFoundError);
    });
  });
});
```

#### ❌ Bad - Unclear structure, missing edge cases
```typescript
it('works', async () => {
  const user = await UserService.findById('123');
  expect(user).toBeTruthy();
});
```

### Component Testing

#### ✅ Good - Tests user behavior
```typescript
describe('UserProfile', () => {
  it('should display user information after loading', async () => {
    // Arrange
    const mockUser = { id: '1', name: 'John', email: 'john@example.com' };
    jest.spyOn(UserService, 'findById').mockResolvedValue(mockUser);
    
    // Act
    render(<UserProfile userId="1" />);
    
    // Assert
    expect(screen.getByText('Loading...')).toBeInTheDocument();
    await waitFor(() => {
      expect(screen.getByText('John')).toBeInTheDocument();
      expect(screen.getByText('john@example.com')).toBeInTheDocument();
    });
  });

  it('should display error message when user not found', async () => {
    // Arrange
    jest.spyOn(UserService, 'findById').mockRejectedValue(new NotFoundError());
    
    // Act
    render(<UserProfile userId="999" />);
    
    // Assert
    await waitFor(() => {
      expect(screen.getByText('User not found')).toBeInTheDocument();
    });
  });
});
```

#### ❌ Bad - Tests implementation details
```typescript
it('should call useState', () => {
  const spy = jest.spyOn(React, 'useState');
  render(<UserProfile userId="1" />);
  expect(spy).toHaveBeenCalled(); // Implementation detail!
});
```

### Integration Test Pattern

```typescript
describe('User Registration Flow', () => {
  beforeEach(async () => {
    await clearDatabase();
  });

  it('should create user and send welcome email', async () => {
    // Arrange
    const userData = { email: 'test@example.com', password: 'secure123' };
    
    // Act
    const response = await request(app)
      .post('/api/users/register')
      .send(userData);
    
    // Assert
    expect(response.status).toBe(201);
    expect(response.body).toHaveProperty('id');
    
    // Verify user in database
    const user = await db.users.findByEmail(userData.email);
    expect(user).toBeDefined();
    expect(user.emailVerified).toBe(false);
    
    // Verify email sent
    expect(emailService.sendWelcome).toHaveBeenCalledWith(user);
  });
});
```

### What to Test

**High Priority (Always Test):**
- ✅ Business logic and calculations
- ✅ Data transformations
- ✅ API endpoints (request/response)
- ✅ Error handling paths
- ✅ Authentication/authorization
- ✅ Data validation

**Medium Priority (Test When Complex):**
- ⚠️ Component rendering logic
- ⚠️ User interactions (clicks, form submissions)
- ⚠️ State management
- ⚠️ Routing logic

**Low Priority (Usually Skip):**
- ❌ Simple getters/setters
- ❌ Pure UI components with no logic
- ❌ Third-party library internals
- ❌ Configuration files

### Test Coverage Guidelines

- **Aim for 80%+ coverage on services/business logic**
- **Aim for 60%+ coverage on components**
- **100% coverage is not the goal** - focus on critical paths

### Mocking Best Practices

#### ✅ Good - Mock external dependencies
```typescript
// Mock external API
jest.mock('@/services/external-api', () => ({
  fetchData: jest.fn()
}));

// Mock only what you need
jest.spyOn(UserService, 'findById').mockResolvedValue(mockUser);
```

#### ❌ Bad - Over-mocking
```typescript
// Don't mock everything - test real logic
jest.mock('@/utils/validation'); // This should be tested, not mocked!
```

### Test Naming Convention

**Format:** `should [expected behavior] when [condition]`

#### ✅ Good - Descriptive
```typescript
it('should return empty array when no users exist', async () => {
  // ...
});

it('should throw ValidationError when email is invalid', () => {
  // ...
});
```

#### ❌ Bad - Vague
```typescript
it('works', () => {}); 
it('test user', () => {});
```

### Running Tests

```bash
# Run all tests
npm test

# Run tests in watch mode (development)
npm test -- --watch

# Run tests with coverage
npm test -- --coverage

# Run specific test file
npm test user.service.test.ts
```

### Pre-Commit Testing

**Before marking any task complete:**
- [ ] All existing tests pass
- [ ] New tests written for new features
- [ ] Tests cover happy path and error cases
- [ ] No console errors or warnings in tests

---

## Comments & Documentation

### When to Comment
- Complex algorithms that aren't immediately obvious
- Business logic that has specific requirements
- Workarounds for known issues/limitations
- Public API functions

### When NOT to Comment
- Obvious code (e.g., `// set user name`)
- Restating what the code does
- Outdated information

#### ✅ Good Comment
```typescript
// Using setTimeout instead of setInterval because we want to wait
// for the API call to complete before scheduling the next one.
// This prevents request pileup if the API is slow.
setTimeout(pollData, 5000);
```

---

## TypeScript Standards

### Type Definitions
- Prefer `interface` for object shapes
- Use `type` for unions, intersections, and primitives
- Always type function parameters and return values
- Avoid `any` - use `unknown` if truly needed

#### ✅ Good Typing
```typescript
interface User {
  id: string;
  name: string;
}

type UserRole = 'admin' | 'user' | 'guest';

function getUser(id: string): Promise<User> {
  return userService.findById(id);
}
```

---

## Performance Patterns

### React Optimization
- Use `React.memo()` for expensive pure components
- Use `useMemo()` for expensive calculations
- Use `useCallback()` for handlers passed to memoized children
- Avoid inline object/array creation in render

---

## Security Patterns

### Authentication
- Always validate tokens on the server
- Never store sensitive data in localStorage
- Use httpOnly cookies for tokens when possible

### Data Validation
- Validate all user input
- Sanitize data before displaying
- Use parameterized queries for database access

---

## Notes

- Update this document when establishing new patterns
- Include both ❌ Bad and ✅ Good examples
- Link to specific files as reference implementations
- Keep examples concise but complete

