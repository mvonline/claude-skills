---
name: microservices-patterns
description: Microservices and Modular Monolith architecture patterns for PHP/Laravel. Includes a decision framework for choosing between architectures and implementation strategies for both.
---

# Microservices & Modular Monoliths (PHP/Laravel)

Strategic architecture selection and implementation patterns for modern PHP systems.

## ⚖️ The Decision Framework: Microservices vs. Modular Monolith

| Factor | Modular Monolith | Microservices |
|--------|------------------|---------------|
| **Team Size** | 1-2 Small Teams | Multiple Independent Teams |
| **Infrastructure** | Standard VPS / Simple Docker | Kubernetes / Multi-cloud |
| **Data Integrity** | Database Transactions | Distributed State (Sagas) |
| **Release Cycle** | Synchronized | Independent |
| **Network Latency**| Zero (Local calls) | High (Network overhead) |

**Rule of Thumb**: If your team is less than 20 developers, a **Modular Monolith** is almost always the better choice. It offers 80% of the benefits of Microservices with 20% of the complexity.

---

## 🏗️ Modular Monolith Pattern (Laravel)

Using Domain-Oriented structures within a single Laravel instance.

### Implementation Strategy
- **Namespacing**: Organize code by Domain (`App\Domains\Billing`, `App\Domains\Users`).
- **Service Providers**: Give each domain its own Service Provider to register its own routes, migrations, and bindings.
- **Inter-Domain Communication**: Use **Events** for async communication and **Contracts/Interfaces** for sync communication.

```php
// app/Domains/Billing/Providers/BillingServiceProvider.php
public function register() {
    $this->loadMigrationsFrom(__DIR__.'/../Database/Migrations');
}
```

---

## 🌩️ Microservices Pattern (Laravel)

Building distributed Laravel systems.

### Implementation Strategy
- **Statelessness**: Ensure all services are truly stateless.
- **Communication**: Favor Asynchronous (Queues/RabbitMQ) over Synchronous (HTTP).
- **Service Discovery**: Use Consul or Eureka if managing many services.
- **Shared Libraries**: Package shared DTOs or logic into private Composer packages.

```php
// Dispatching to a remote service via Queue
UpdateInventoryJob::dispatch($orderId)->onQueue('inventory_service');
```

## Best Practices
- **Database per Service**: Never share a database between microservices.
- **API Versioning**: Strict adherence to SemVer for service contracts.
- **Fallbacks**: Implement Circuit Breakers (Resilience4j style, or simple timeouts) for all external calls.
