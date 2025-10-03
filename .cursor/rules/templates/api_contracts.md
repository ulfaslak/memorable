# API Contracts & Interface Definitions

> **Purpose:** Document function signatures, data models, and interfaces to prevent hallucination of APIs when context degrades.

---

## Data Models

### User Model
```typescript
interface User {
  id: string;
  email: string;
  name: string;
  createdAt: Date;
  updatedAt: Date;
}
```

**Usage:** Core user entity used throughout the application

---

## API Endpoints

### Authentication

#### POST /api/auth/login
```typescript
Request: {
  email: string;
  password: string;
}

Response: {
  user: User;
  token: string;
}

Errors:
  - 401: Invalid credentials
  - 400: Validation error
```

---

## Service Interfaces

### UserService
```typescript
interface UserService {
  findById(id: string): Promise<User | null>;
  findByEmail(email: string): Promise<User | null>;
  create(data: CreateUserDTO): Promise<User>;
  update(id: string, data: UpdateUserDTO): Promise<User>;
  delete(id: string): Promise<void>;
}
```

**Location:** `/services/user.service.ts`  
**Implementation:** `UserServiceImpl`

---

## Component Props

### Button Component
```typescript
interface ButtonProps {
  variant: 'primary' | 'secondary' | 'danger';
  size?: 'sm' | 'md' | 'lg';
  disabled?: boolean;
  onClick: () => void;
  children: React.ReactNode;
}
```

**Location:** `/components/Button.tsx`

---

## Database Schema

### users table
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  name VARCHAR(255) NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

---

## Event Schemas

### UserCreatedEvent
```typescript
interface UserCreatedEvent {
  type: 'user.created';
  timestamp: Date;
  data: {
    userId: string;
    email: string;
  };
}
```

---

## Validation Rules

### User Registration
- Email: Valid email format, max 255 chars
- Password: Min 8 chars, must contain uppercase, lowercase, number
- Name: Min 2 chars, max 255 chars

---

## Notes

- All IDs use UUID v4 format
- Timestamps are stored in UTC
- All async operations return Promises
- Error handling follows standard Error objects with message and code

