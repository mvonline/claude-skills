---
name: eloquent-patterns
description: Eloquent ORM best practices and patterns. Use when writing database models, relationships, or querying data in Laravel.
---

# Eloquent Patterns Skill

Efficient database management and querying using Laravel Eloquent.

## When to Use
- Designing Eloquent models and relationships
- Optimizing database queries (N+1 prevention)
- Using Query Scopes and Accessors/Mutators
- Handling model events and observers

---

## Model Setup

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\HasMany;

class User extends Model
{
    use HasFactory;

    protected $fillable = [
        'name',
        'email',
        'password',
    ];

    protected $hidden = [
        'password',
        'remember_token',
    ];

    public function posts(): HasMany
    {
        return $this->hasMany(Post::class);
    }
}
```

## Query Patterns

### Eager Loading (N+1 Prevention)
```php
// Bad: N+1 problem
$users = User::all();
foreach ($users as $user) {
    echo $user->posts; // Runs a query for EACH user
}

// Good: Single query for users and posts
$users = User::with('posts')->get();
```

### Local Scopes
```php
public function scopeActive(Builder $query): Builder
{
    return $query->where('status', 'active');
}

// Usage
$activeUsers = User::active()->get();
```

## Best Practices

| Practice | Details |
|----------|---------|
| Mass Assignment | Use `$fillable` or `$guarded` to prevent security issues |
| Casting | Use `$casts` for automatic type conversion (e.g., `'is_admin' => 'boolean'`) |
| Relationships | Define clear relationships (HasMany, BelongsTo, ManyToMany) with type hints |
| Soft Deletes | Use `SoftDeletes` trait for recoverable data |
| Pagination | Always use `paginate()` for large datasets |
