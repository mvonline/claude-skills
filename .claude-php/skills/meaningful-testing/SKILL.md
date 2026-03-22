# Meaningful Testing with PHP and Laravel

This skill defines the standards for meaningful testing in Laravel applications using Pest or PHPUnit.

## Core Principles
1. **Scenario-Based**: tests should read like user stories or requirements.
2. **Data Factories**: use Laravel Factories for realistic, consistent test data.
3. **Database Integrity**: use Transaction-based testing for speed and consistency.
4. **Outcome over Process**: assert the final state/response, not individual function calls.

## Implementation Patterns

### 1. Feature vs Unit
- **Feature Tests**: most Laravel tests should be Feature tests, verifying the HTTP request -> DB -> Response flow.
- **Unit Tests**: reserved for isolated utility classes or complex domain logic.

### 2. Meaningful Assertions (Pest)
```php
// BAD: shallow test
it('works', function () {
    $this->get('/')->assertOk();
});

// GOOD: meaningful test
it('creates a new task with valid data', function () {
    $user = User::factory()->create();
    
    $response = $this->actingAs($user)
        ->post('/tasks', ['title' => 'Learn Pest']);
        
    $response->assertStatus(201)
        ->assertJsonPath('data.title', 'Learn Pest');
        
    expect(Task::count())->toBe(1);
});
```

### 3. Coverage Strategy (>80%)
- Run `php artisan test --coverage` regularly.
- Ensure all Controller actions and Service patterns have high-coverage tests.
- Don't skip the "sad path": test validation failures (422) and unauthorized access (403/401).

## Advanced Automation
### UI Testing (Laravel Dusk)
- Automated browser testing of complex SPA/Livewire components.
- Use Dusk Page objects to centralize selectors.

### API Testing
- Assert JSON structure and specific data types.
- Mock external APIs using `Http::fake()`.

### Performance
- Use `laravel-debugbar` or Clockwork in tests to monitor query count.
- Prevent N+1 issues by asserting lazy loading is avoided.
