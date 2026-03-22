# Meaningful Testing with Java and Spring Boot

This skill provides patterns and best practices for writing high-impact, meaningful tests in a Java/Spring Boot environment, aiming for >80% coverage.

## Core Principles
1. **Behavioral Testing**: focus on what the system does, not how it's implemented.
2. **Clear Assertions**: use `assertThat` (Hamcrest/AssertJ) for readable, precise assertions.
3. **Realistic Data**: Avoid trivial `new Object()` data; use meaningful domain-relevant test data.
4. **Environment Isolation**: ensure tests are independent and don't leak state.

## Implementation Patterns

### 1. The Testing Pyramid
- **Unit Tests (Internal Logic)**: JUnit 5 + Mockito. Fast, isolated, no Spring context.
- **Integration Tests (Slices)**: `@DataJpaTest`, `@WebMvcTest`. Verifies interaction with layers.
- **System/E2E Tests**: `@SpringBootTest`. Verifies the full application flow.

### 2. Meaningful Assertions
```java
// BAD: meaning-less assertion
assertTrue(response.isOk());

// GOOD: meaningful assertion
assertThat(response.getStatus(), is(200));
assertThat(response.getBody(), containsString("User created successfully"));
assertThat(userRepository.findByEmail(email), is(notNullValue()));
```

### 3. Coverage Strategy (>80%)
- **Line Coverage**: baseline requirement.
- **Branch Coverage**: ensure all `if/else` and `switch` paths are tested.
- **Edge Cases**: test with empty inputs, nulls, long strings, and maximum/minimum numeric values.

## Advanced Automation
### UI Testing (Selenium/Playwright)
- Use **Page Object Model (POM)** for maintainable locators.
- Implement explicit waits (Avoid `Thread.sleep`).
- Verify visual consistency with screenshot regression.

### API/Contract Testing (RestAssured)
- Validate JSON schemas against OpenAPI specs.
- Test error responses (4xx, 5xx) with specific messages.
- Use Data-Driven testing for bulk input validation.

### Performance (JMeter/Gatling)
- Establish performance baselines for critical endpoints.
- Automate load tests in CI/CD with threshold checks.
