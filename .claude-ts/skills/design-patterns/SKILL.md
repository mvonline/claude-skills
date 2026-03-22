---
name: design-patterns
description: High-level design patterns for TypeScript and NestJS. Use when designing complex system architectures, implementing extensible components, or applying GoF patterns in a modern TS context.
---

# High Expert Design Patterns (TypeScript/NestJS)

Advanced design patterns and their implementation in modern TypeScript ecosystems.

## Creational Patterns

### Factory (Dynamic Modules)
In NestJS, the Factory pattern is most commonly used for **Dynamic Modules**.
```typescript
@Module({})
export class DatabaseModule {
  static register(options: DatabaseOptions): DynamicModule {
    return {
      module: DatabaseModule,
      providers: [
        {
          provide: 'DATABASE_CONNECTION',
          useValue: createConnection(options),
        },
      ],
      exports: ['DATABASE_CONNECTION'],
    };
  }
}
```

### Builder (Fluent API)
```typescript
class QueryBuilder {
  private query: string = '';
  select(fields: string): this { this.query += `SELECT ${fields} `; return this; }
  from(table: string): this { this.query += `FROM ${table} `; return this; }
  build(): string { return this.query.trim(); }
}
```

## Structural Patterns

### Decorator (Built-in TS/NestJS)
Leveraging decorators to add metadata or behavior.
```typescript
@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    console.log('Before...');
    return next.handle().pipe(tap(() => console.log('After...')));
  }
}
```

## Behavioral Patterns

### Strategy (Injection Tokens)
Using different implementations for the same interface.
```typescript
@Injectable()
export class PaymentService {
  constructor(@Inject('PAYMENT_STRATEGY') private strategy: PaymentStrategy) {}
  process(amount: number) { return this.strategy.pay(amount); }
}
```

### Observer (EventEmitter)
```typescript
@Injectable()
export class OrderService {
  constructor(private eventEmitter: EventEmitter2) {}
  createOrder(order: any) {
    this.eventEmitter.emit('order.created', new OrderCreatedEvent(order.id));
  }
}
```

## Best Practices
- **Singleton**: Handled by NestJS Modules by default.
- **Adapter**: Use to wrap 3rd party libraries into NestJS Injectables.
- **Composition**: Prefer over heavy inheritance hierarchies.
