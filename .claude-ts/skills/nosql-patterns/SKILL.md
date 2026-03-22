---
name: nosql-patterns
description: NoSQL best practices for TypeScript and NestJS. Use when working with MongoDB (Mongoose), Redis (Caching/Sessions), or designing document-based schemas.
---

# NoSQL Patterns Skill (TypeScript/NestJS)

Efficiently working with non-relational databases in modern Node.js environments.

## When to Use
- Designing MongoDB schemas with `@nestjs/mongoose` or Mongoose directly.
- Implementing Redis caching or session management.
- Designing high-throughput, horizontally scalable data stores.

---

## MongoDB (Mongoose)

### Schema Definition
```typescript
@Schema({ timestamps: true })
export class User {
  @Prop({ required: true, unique: true })
  email: string;

  @Prop()
  name: string;

  @Prop({ type: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Post' }] })
  posts: Post[];
}
```

### Best Practices
- **Indexing**: Always use `index: true` or `@Prop({ index: true })` for searchable fields.
- **Lean Queries**: Use `.lean()` for read-only operations to improve performance (avoids Mongoose document overhead).
- **Populate**: Use `.populate()` sparingly to avoid large join-like operations.

---

## Redis (Caching)

### Pattern: Cache Aside
```typescript
async function getCachedUser(userId: string) {
  const cached = await redis.get(`user:${userId}`);
  if (cached) return JSON.parse(cached);

  const user = await userRepository.findById(userId);
  await redis.set(`user:${userId}`, JSON.stringify(user), 'EX', 3600);
  return user;
}
```

## Best Practices
- **TTL**: Always set an Expiration (TTL) for cache keys.
- **Namespacing**: Use prefixes (`user:1`, `session:abc`) to avoid key collisions.
- **Serialization**: Use `JSON.stringify` or specialized binary serializers for complex objects.
