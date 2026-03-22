---
name: message-queues
description: Message Queue best practices for PHP and Laravel. Use when implementing Laravel Queues, RabbitMQ, or background processing with Jobs and Events.
---

# Message Queue Patterns Skill (PHP/Laravel)

Building reliable background processing and event-driven systems in Laravel.

## When to Use
- Offloading long-running tasks to Laravel Queues (Redis, RabbitMQ, SQS).
- Implementing event-driven architectures with Listeners and Job chains.
- Scaling PHP applications by decoupling heavy processing.

---

## Laravel Queues & Jobs

### Job Implementation
```php
class ProcessOrder implements ShouldQueue
{
    use Dispatchable, InteractsWithQueue, Queueable, SerializesModels;

    public function __construct(public Order $order) {}

    public function handle(OrderService $service): void
    {
        $service->process($this->order);
    }
}
```

### Dispatching with Chains
```php
Bus::chain([
    new ProcessOrder($order),
    new NotifyCustomer($order),
])->dispatch();
```

---

## RabbitMQ Integration

### Configuration
Use `vyuldashev/laravel-queue-rabbitmq` for full RabbitMQ support.

## Best Practices
- **Idempotency**: Ensure Jobs can be retried safely (`tries` property).
- **Timeouts**: Define reasonable timeouts and memory limits for workers.
- **Batching**: Use `Bus::batch()` for sets of independent tasks with progress tracking.
- **DLQ**: Monitor failed jobs in the `failed_jobs` table or dedicated MQ queues.
