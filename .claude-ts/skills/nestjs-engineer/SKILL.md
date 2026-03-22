---
name: nestjs-engineer
description: NestJS best practices and patterns. Use when creating modules, controllers, providers, or when user asks about NestJS architecture, Dependency Injection, Middleware, Pipes, Guard, and Interceptors.
---

# NestJS Engineer Skill

Best practices and patterns for building scalable NestJS applications.

## When to Use
- User says "create nestjs module" / "add controller" / "NestJS help"
- Reviewing NestJS code
- Setting up new NestJS project structure

## Project Structure (Standard)

```
src/
├── app.module.ts            # Root module
├── main.ts                  # Entry point
├── common/                  # Shared utilities, decorators, filters
│   ├── decorators/
│   ├── filters/
│   ├── guards/
│   ├── interceptors/
│   └── pipes/
├── modules/                 # Functional modules
│   └── users/
│       ├── users.module.ts
│       ├── users.controller.ts
│       ├── users.service.ts
│       ├── dto/
│       │   ├── create-user.dto.ts
│       │   └── update-user.dto.ts
│       └── entities/
│           └── user.entity.ts
└── config/                  # Configuration management
```

---

## Controller Patterns

### REST Controller Template
```typescript
import { Controller, Get, Post, Body, Put, Param, Delete, HttpCode, HttpStatus } from '@nestjs/common';
import { CreateUserDto } from './dto/create-user.dto';
import { UpdateUserDto } from './dto/update-user.dto';
import { UsersService } from './users.service';

@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Post()
  @HttpCode(HttpStatus.CREATED)
  create(@Body() createUserDto: CreateUserDto) {
    return this.usersService.create(createUserDto);
  }

  @Get()
  findAll() {
    return this.usersService.findAll();
  }

  @Get(':id')
  findOne(@Param('id') id: string) {
    return this.usersService.findOne(+id);
  }

  @Patch(':id')
  update(@Param('id') id: string, @Body() updateUserDto: UpdateUserDto) {
    return this.usersService.update(+id, updateUserDto);
  }

  @Delete(':id')
  @HttpCode(HttpStatus.NO_CONTENT)
  remove(@Param('id') id: string) {
    return this.usersService.remove(+id);
  }
}
```

## Best Practices

| Practice | Details |
|----------|---------|
| Dependency Injection | Use constructor-based DI |
| DTOs | Use `class-validator` and `class-transformer` |
| Pipes | Use `ValidationPipe` globally for automated validation |
| Async/Await | Always return Promises/Observables and use async/await |
| Error Handling | Use built-in `HttpException` or custom filters |
| Interceptors | Use for response mapping and logging |
| Guards | Use for authentication and authorization (e_PERMISSION_DENIED) |
