---
name: design-patterns
description: High-level design patterns for PHP 8.3+ and Laravel. Use when designing robust Laravel architectures, implementing extensible service layers, or applying GoF patterns "The Laravel Way".
---

# High Expert Design Patterns (PHP/Laravel)

Advanced design patterns tailored for modern PHP and the Laravel ecosystem.

## Creational Patterns

### Factory (Service Providers)
The Service Container is the ultimate Factory in Laravel.
```php
public function register(): void
{
    $this->app->singleton(PaymentGateway::class, function ($app) {
        return new StripePaymentGateway(config('services.stripe.key'));
    });
}
```

### Builder (Eloquent & Fluent)
```php
$users = User::query()
    ->where('active', true)
    ->orderBy('created_at')
    ->limit(10)
    ->get(); // Standard Eloquent Builder
```

## Structural Patterns

### Decorator (Middleware)
Laravel Middleware implements a variant of the Decorator/Chain of Responsibility pattern.
```php
public function handle(Request $request, Closure $next): Response
{
    // Pre-processing
    $response = $next($request);
    // Post-processing
    return $response;
}
```

### Adapter (Cloud Storage)
Laravel's `Storage` facade is a classic Adapter for different filesystem drivers (Local, S3, etc.).

## Behavioral Patterns

### Strategy (Conditional Binding)
```php
$this->app->bind(SmsProvider::class, function ($app) {
    if (config('app.env') === 'production') {
        return new TwilioSmsProvider();
    }
    return new LogSmsProvider();
});
```

### Observer (Model Observers)
```php
class UserObserver
{
    public function created(User $user): void
    {
        // Logic after user is created
    }
}
```

### Template Method (Base Action)
```php
abstract class BaseAction
{
    final public function execute(array $data)
    {
        $this->validate($data);
        return $this->handle($data);
    }
    abstract protected function handle(array $data);
}
```

## Best Practices
- **Facades**: Use sparingly in complex logic; prefer Dependency Injection for testability.
- **Traits**: Use for horizontal code reuse across models/controllers.
- **Contracts**: Always code to an Interface (Contract) to allow for strategy swaps.
