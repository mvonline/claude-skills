---
name: laravel-engineer
description: Laravel best practices and patterns. Use when creating controllers, models, migrations, or when user asks about Laravel architecture, Eloquent, Service Providers, and Middlewares.
---

# Laravel Engineer Skill

Best practices and patterns for building robust Laravel 11+ applications.

## When to Use
- User says "create laravel controller" / "add model" / "Laravel help"
- Reviewing Laravel code
- Setting up new Laravel project structure

## Project Structure (Laravel 11+)

```
app/
├── Http/
│   ├── Controllers/
│   ├── Middleware/
│   └── Requests/            # Custom Form Requests
├── Models/                  # Eloquent Entities
├── Providers/               # Service Providers
├── Services/                # Custom Business Logic
└── View/
bootstrap/
config/
database/
├── factories/
├── migrations/
└── seeders/
routes/
├── api.php
└── web.php
```

---

## Controller Patterns

### REST Controller Template
```php
<?php

namespace App\Http\Controllers;

use App\Http\Requests\StoreUserRequest;
use App\Http\Requests\UpdateUserRequest;
use App\Models\User;
use App\Services\UserService;
use Illuminate\Http\JsonResponse;

class UserController extends Controller
{
    public function __construct(
        protected UserService $userService
    ) {}

    public function index(): JsonResponse
    {
        return response()->json($this->userService->getAll());
    }

    public function store(StoreUserRequest $request): JsonResponse
    {
        $user = $this->userService->create($request->validated());
        return response()->json($user, 201);
    }

    public function show(User $user): JsonResponse
    {
        return response()->json($user);
    }

    public function update(UpdateUserRequest $request, User $user): JsonResponse
    {
        $user = $this->userService->update($user, $request->validated());
        return response()->json($user);
    }

    public function destroy(User $user): JsonResponse
    {
        $this->userService->delete($user);
        return response()->json(null, 204);
    }
}
```

## Best Practices

| Practice | Details |
|----------|---------|
| Dependency Injection | Use constructor injection in controllers and services |
| Form Requests | Use for validation to keep controllers clean |
| Service Layer | Extract business logic from controllers into dedicated Services |
| Eloquent Scopes | Use for reusable query logic in Models |
| Resource Classes | Use API Resources for JSON response mapping |
| Type Hinting | Always use PHP 8.3+ strict typing |
