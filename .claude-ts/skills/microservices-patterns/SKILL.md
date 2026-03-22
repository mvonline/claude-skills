---
name: microservices-patterns
description: Microservices and Modular Monolith architecture patterns for TypeScript/NestJS. Includes a decision framework for choosing between architectures and implementation strategies for both.
---

# Microservices & Modular Monoliths (TypeScript/NestJS)

Strategic architecture selection and implementation patterns for modern Node.js systems.

## ⚖️ The Decision Framework: Microservices vs. Modular Monolith

Use this matrix to decide the best architectural fit for your project:

| Factor | Modular Monolith | Microservices |
|--------|------------------|---------------|
| **Team Size** | 1-3 Small Teams | 3+ Large/Independent Teams |
| **Complexity** | Medium to High | Very High / Hyper-scale |
| **Deployment** | Atomic (All at once) | Independent (Per service) |
| **Data Consistency**| Strict (ACID/Transactions) | Eventual Consistency (Saga Pattern) |
| **Infrastructure** | Simple (Single DB/Server) | Complex (K8s, MQ, Service Mesh) |
| **Cognitive Load** | Lower (Unified codebase) | Higher (Distributed system) |

**Recommendation**: Start with a **Modular Monolith**. It provides the separation of concerns needed to split into Microservices later without the premature overhead of distributed systems.

---

## 🏗️ Modular Monolith Pattern (NestJS)

Implementing strict boundaries within a single repository.

### Implementation Strategy
- **Bounded Contexts**: Each module (`UsersModule`, `BillingModule`) is completely self-contained.
- **Internal APIs**: Modules communicate via internal services, NOT by reaching into each other's databases or internal classes.
- **Shared Kernel**: Use a `CommonModule` for shared types/utilities, but keep it minimal.

```typescript
// BillingModule only depends on UserModule's Service, not its Entity
@Module({
  imports: [UserModule],
  providers: [BillingService],
})
export class BillingModule {}
```

---

## 🌩️ Microservices Pattern (NestJS)

Using NestJS Microservices transport layers.

### Implementation Strategy
- **Transport**: Use RabbitMQ or Kafka for async communication.
- **Gateways**: Use a central API Gateway (NestJS or Kong/Nginx) to route traffic.
- **Data per Service**: Each microservice MUST have its own database.

```typescript
// Integration via Microservice Client
@Injectable()
export class OrderService {
  constructor(@Inject('ORDER_BUS') private client: ClientProxy) {}
  
  createOrder(data: any) {
    return this.client.emit('order_created', data);
  }
}
```

## Best Practices
- **Anti-Corruption Layer**: Use DTOs to map incoming data to internal models.
- **Observability**: Implement distributed tracing (OpenTelemetry) from day one.
- **Contract Testing**: Use Pact to ensure service compatibility.
