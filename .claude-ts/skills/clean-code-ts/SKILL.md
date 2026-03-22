---
name: clean-code-ts
description: Clean Code principles for TypeScript. Use when reviewing code, naming variables/functions, or organizing logic in TS projects.
---

# Clean Code TypeScript Skill

Applying Clean Code principles to TypeScript development.

## Core Concepts

- **Meaningful Names**: Variables and functions should reveal intent.
- **Small Functions**: Functions should do one thing (SRP).
- **Avoid Comments**: Code should be self-documenting; use comments only for "why", not "how".
- **DRY (Don't Repeat Yourself)**: Abstract common logic into utilities or decorators.

---

## Naming Conventions

| Entity | Convention | Example |
|--------|------------|---------|
| Variables/Functions | camelCase | `getUserData()`, `isActive` |
| Classes/Interfaces/Types | PascalCase | `UserService`, `UserData` |
| Enums | PascalCase | `UserRole` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT` |
| Files | kebab-case | `user-controller.ts` |

---

## Function Design

### Good (Small, Focused)
```typescript
async function activateUser(userId: number): Promise<void> {
  const user = await userRepository.findById(userId);
  validateUserStatus(user);
  await userRepository.update(userId, { active: true });
  await emailService.sendActivationNotification(user.email);
}
```

### Avoid (Side Effects, Multiple Responsibilities)
```typescript
function processUser(user: any) {
  user.updatedAt = new Date(); // Side effect
  if (user.age > 18) { /* ... logic ... */ }
  saveToDb(user); // Persistence in business logic
  // ... more logic ...
}
```

## TS Specific Clean Code

- **Use Records**: `Record<string, User>` instead of `{[key: string]: User}`.
- **Prefer Map/Filter**: Use functional array methods instead of `for` loops.
- **Early Return**: Avoid deep nesting by returning early.
- **Object Destructuring**: Use for cleaner function arguments and property access.
