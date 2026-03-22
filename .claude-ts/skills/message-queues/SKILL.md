---
name: message-queues
description: Message Queue best practices for TypeScript and NestJS. Use when implementing RabbitMQ, Kafka, or NestJS Microservices for event-driven architectures and background processing.
---

# Message Queue Patterns Skill (TypeScript/NestJS)

Building reliable event-driven and distributed systems.

## When to Use
- Implementing NestJS Microservices with RabbitMQ or Kafka.
- Offloading heavy tasks to background workers.
- Designing asynchronous communication between services.

---

## NestJS Microservices (RabbitMQ)

### Client Configuration
```typescript
ClientsModule.register([
  {
    name: 'MAIL_SERVICE',
    transport: Transport.RMQ,
    options: {
      urls: ['amqp://localhost:5672'],
      queue: 'mail_queue',
      queueOptions: { durable: false },
    },
  },
])
```

### Event Handling
```typescript
@EventPattern('user_created')
async handleUserCreated(data: Record<string, unknown>) {
  // Logic to handle event (e.g., send welcome email)
}
```

---

## Kafka Patterns

### Producer Example
```typescript
async onModuleInit() {
  this.client.subscribeToResponseOf('get_user_info');
  await this.client.connect();
}
```

## Best Practices
- **Idempotency**: Ensure message handlers can be retried safely.
- **Dead Letter Queues (DLQ)**: Implement for messages that consistently fail processing.
- **Ack/Nack**: Use manual acknowledgments for critical tasks to prevent message loss.
- **Payload Size**: Keep messages small; pass IDs rather than large objects.
