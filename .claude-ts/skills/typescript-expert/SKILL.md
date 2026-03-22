---
name: typescript-expert
description: TypeScript best practices and advanced patterns. Use when writing TS code, defining interfaces/types, using generics, or when user asks about TS configuration, Decorators, or utility types.
---

# TypeScript Expert Skill

Best practices and advanced patterns for modern TypeScript development.

## When to Use
- Writing or refactoring TypeScript code
- Defining complex data structures
- Debugging type-related issues
- Optimizing TS configuration

## Core Principles

- **Strict Mode**: Always enable `strict: true` in `tsconfig.json`.
- **Type Inference**: Let TS infer types where obvious, but be explicit for public APIs.
- **Avoid `any`**: Use `unknown` or specific types/generics instead.
- **Immutability**: Use `readonly` for properties that shouldn't change.

---

## Patterns

### Advanced Types
```typescript
// Use Discriminated Unions for related types
type SuccessResponse<T> = {
  status: 'success';
  data: T;
};

type ErrorResponse = {
  status: 'error';
  message: string;
};

type APIResponse<T> = SuccessResponse<T> | ErrorResponse;

// Use Utility Types
type UserPreview = Pick<User, 'id' | 'username'>;
type OptionalUser = Partial<User>;
type RequiredUser = Required<User>;
```

### Generic Patterns
```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
```

### Functional Patterns
```typescript
// Prefer arrow functions for callbacks to preserve 'this'
const boundMethod = (args: any) => {
  // context is preserved
};
```

## Best Practices

| Practice | Details |
|----------|---------|
| Interfaces vs Types | Use `interface` for public APIs/extensibility, `type` for unions/aliases |
| Explicit Return Types | Always define return types for public service methods |
| Enums | Prefer `const enum` or Union Types (`'A' | 'B'`) over standard `enum` |
| Null Checks | Use Optional Chaining (`?.`) and Nullish Coalescing (`??`) |
| Async Patterns | Use `Promise.all` for parallel operations |
