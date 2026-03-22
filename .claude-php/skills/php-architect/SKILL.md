---
name: php-architect
description: PHP 8.3+ best practices and architectural patterns. Use when designing PHP systems, writing core classes, or when user asks about PHP versions, PSR standards, and advanced PHP features.
---

# PHP Architect Skill

Designing and building enterprise-grade PHP 8.3+ applications.

## When to Use
- Designing new systems or modules in PHP
- Reviewing core PHP code and architectural decisions
- Optimizing PHP performance and type safety
- Ensuring compliance with PSR standards

## Core Principles (PHP 8.3+)

- **Strict Typing**: Always use `declare(strict_types=1);` in all PHP files.
- **Modern Syntax**: Leverage constructor property promotion, readonly classes, and enums.
- **PSR Standards**: Adhere to PSR-1, PSR-4 (autoloading), and PSR-12 (coding style).
- **Composer**: Use `composer.json` for dependency management and PSR-4 autoloading.

---

## Modern PHP Patterns

### Readonly Class with Constructor Promotion
```php
<?php

declare(strict_types=1);

namespace App\Core\Data;

readonly class UserProfile
{
    public function __construct(
        public int $id,
        public string $username,
        public string $email,
        public DateTimeImmutable $createdAt,
    ) {}
}
```

### Enums
```php
<?php

declare(strict_types=1);

namespace App\Core\Enums;

enum UserStatus: string
{
    case ACTIVE = 'active';
    case INACTIVE = 'inactive';
    case PENDING = 'pending';

    public function label(): string
    {
        return match($this) {
            self::ACTIVE => 'Active User',
            self::INACTIVE => 'Disabled User',
            self::PENDING => 'Awaiting Approval',
        };
    }
}
```

## Best Practices

| Practice | Details |
|----------|---------|
| Strict Types | Enforce `declare(strict_types=1)` for predictable behavior |
| Enums | Use for type-safe constant groups |
| Readonly | Use `readonly` for immutable objects/classes |
| Attributes | Use PHP 8+ attributes for metadata over docblocks |
| Match Expression | Use `match` over `switch` for cleaner condition handling |
| Fibers | Use for concurrency in I/O bound tasks if appropriate |
