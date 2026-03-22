---
name: prisma-patterns
description: Prisma ORM best practices and patterns. Use when writing DB schemas, migrations, or querying data with Prisma Client.
---

# Prisma Patterns Skill

Efficient database management and querying using Prisma.

## When to Use
- Designing database schemas in `schema.prisma`
- Writing database migrations
- Optimizing Prisma queries (N+1 prevention)
- Handling database transactions

---

## Schema Design

```prisma
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
  posts     Post[]
  profile   Profile?
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?
  published Boolean  @default(false)
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
}
```

## Query Patterns

### N+1 Prevention
Use `include` or `select` to fetch relations in a single query.

```typescript
// Good: Fetches users and their posts in one go
const usersWithPosts = await prisma.user.findMany({
  include: {
    posts: true,
  },
});
```

### Transactions
```typescript
const result = await prisma.$transaction(async (tx) => {
  const sender = await tx.account.update({
    where: { id: 1 },
    data: { balance: { decrement: 100 } },
  });
  const receiver = await tx.account.update({
    where: { id: 2 },
    data: { balance: { increment: 100 } },
  });
  return { sender, receiver };
});
```

## Best Practices

| Practice | Details |
|----------|---------|
| Typed Queries | Leverage Prisma's auto-generated types for inputs and outputs |
| Middleware | Use for logging, soft deletes, or auditing |
| Raw Queries | Use `$queryRaw` only when necessary for extreme performance/unsupported features |
| Migrations | Always use `prisma migrate dev` for development and `deploy` for production |
| Seeding | Use `prisma/seed.ts` for consistent test data |
