# Meaningful Testing with TypeScript and NestJS

This skill provides the blueprint for high-quality testing in NestJS applications using Jest.

## Core Principles
1. **Dependency Injection Power**: use `@nestjs/testing` to mock only what's necessary.
2. **Contract Testing**: verify API request/response shapes against interfaces/DTOs.
3. **Asynchronous Reliability**: ensure all `async/await` flows are properly awaited in tests.
4. **Type-Safe Mocks**: keep mocks in sync with real types to avoid "phantom" passes.

## Implementation Patterns

### 1. Strategy
- **Unit (Isolation)**: Test Services/Controllers by mocking their dependencies.
- **Integration (Slices)**: Test Controllers with their real Services but mocked Repositories.
- **E2E (End-to-End)**: Test the full app instance with a real (test) database.

### 2. Meaningful Assertions (Jest)
```typescript
// BAD: vague
expect(result).toBeDefined();

// GOOD: precise
expect(result).toEqual(expect.objectContaining({
  id: expect.any(Number),
  username: 'testuser',
  email: 'test@example.com'
}));
expect(service.save).toHaveBeenCalledWith(expect.any(CreateDto));
```

### 3. Coverage Strategy (>80%)
- Run `jest --coverage` and inspect the result.
- Focus on "Business Logic" coverage rather than "Framework Boilerplate".
- Ensure Exception Filters and Interceptors are tested for their respective error scenarios.

## Advanced Automation
### UI/E2E Testing (Playwright/Cypress)
- Test full user flows across the frontend and NestJS backend.
- Use Fixtures for clean environment setup and teardown.

### API/Contract Testing
- Use Supertest for fluent API assertions.
- Validate DTOs and validation pipes in integration tests.

### Performance
- Use Jest's `.perf` or specialized benchmarks for high-frequency functions.
- Monitor memory usage in E2E tests for potential leaks.
