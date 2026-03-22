---
name: clean-code-php
description: Clean Code principles for PHP. Use when reviewing code, naming variables/functions, or organizing logic in Laravel/PHP projects.
---

# Clean Code PHP Skill

Applying Clean Code and SOLID principles to PHP development.

## Core Concepts

- **Meaningful Names**: Use clear, intent-revealing names for variables and methods.
- **Small Methods**: Methods should be focused and perform a single task.
- **SOLID Principles**: Especially SRP (Single Responsibility) and OCP (Open-Closed).
- **YAGNI**: Don't implement features you don't need yet.

---

## Naming Conventions (PSR-12)

| Entity | Convention | Example |
|--------|------------|---------|
| Variables/Methods | camelCase | `$userData`, `updateProfile()` |
| Classes/Interfaces | PascalCase | `UserRepository`, `PaymentGatewayInterface` |
| Constants | UPPER_SNAKE_CASE | `STATUS_PUBLISHED` |
| Namespaces | PascalCase | `App\Http\Controllers` |
| Files | PascalCase (match class) | `UserController.php` |

---

## SOLID Examples in Laravel

### Single Responsibility (SRP)
Extract logic from Controllers to Services or Action classes.

```php
// Bad: Controller handling logic
public function store(Request $request) {
    $data = $request->validate(/*...*/);
    $user = User::create($data);
    Mail::to($user)->send(new WelcomeMail($user));
    return response()->json($user);
}

// Good: Using an Action or Service
public function store(Request $request, CreateUserAction $action) {
    $user = $action->execute($request->validated());
    return response()->json($user);
}
```

## PHP Specific Clean Code

- **Strict Typing**: Always use `declare(strict_types=1);`.
- **Early Returns**: Reduce nesting levels.
- **Ternary/Null Coalescing**: Use `$val ?: 'default'` or `$val ?? 'default'`.
- **Collection Methods**: Use Laravel Collections instead of complex `foreach` loops.
- **Dependency Injection**: Favor DI over Static Facades where possible for better testability.
