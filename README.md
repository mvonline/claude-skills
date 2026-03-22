# Claude Code Templates for Multi-Stack Applications

This repository provides highly optimized, structured starting points for various application stacks, specifically designed for Claude AI's code completion and agentic capabilities. Each configuration includes specialized agents and skills to streamline development, ensure best practices, and enhance productivity.

## Supported Stacks

- **Spring Boot (Java)**: Found in `.claude/`
- **Laravel (PHP)**: Found in `.claude-php/`
- **NestJS (TypeScript)**: Found in `.claude-ts/`

## Project Structure

```shell
.
├── .claude/                # Spring Boot Configuration
│   ├── agents/             # senior-test-engineer.md, stakeholders.md...
│   └── skills/             # meaningful-testing, spring-boot-patterns...
├── .claude-php/            # Laravel Configuration
│   ├── agents/             # senior-test-engineer.md, stakeholders.md...
│   └── skills/             # meaningful-testing, eloqent-patterns...
├── .claude-ts/             # NestJS Configuration
│   ├── agents/             # senior-test-engineer.md, stakeholders.md...
│   └── skills/             # meaningful-testing, prisma-patterns...
├── CLAUDE.md               # Claude-specific project rules
├── README.md               # Project documentation
└── pom.xml                 # Root Maven configuration (example)
```

---

## 🐘 PHP & Laravel Configuration (`.claude-php`)

The PHP configuration is tailored for modern Laravel development, focusing on Eloquent ORM, architectural patterns, and performance.

### Specialized Agents
- **Laravel Architect**: Expert in Laravel structure and service providers.
- **PHP Code Reviewer**: Focuses on PSR standards and PHP-specific best practices.
- **DB Expert**: Optimization for SQL and Eloquent queries.
- **NoSQL & MQ Experts**: Specialized in Redis, MongoDB, and Message Queues.

### Key Skills
- **Eloquent Patterns**: Optimized database interactions and relationships.
- **Clean Code PHP**: PHP-specific design principles.
- **Microservices & Messaging**: Patterns for scalable PHP applications.
- **CI/CD Flows**: Configured for both GitHub and GitLab.

---

## ⚡ TypeScript & NestJS Configuration (`.claude-ts`)

The TypeScript configuration is optimized for NestJS and Prisma, providing a robust environment for enterprise-grade Node.js applications.

### Specialized Agents
- **NestJS Architect**: Expert in modules, decorators, and dependency injection.
- **TS Code Reviewer**: Ensures type safety and modern TS features usage.
- **DB & NoSQL Experts**: Specialized in relational and non-relational data modeling.
- **Github/Gitlab Experts**: CI/CD and workflow specialists.

### Key Skills
- **Prisma Patterns**: Type-safe database access and migrations.
- **NestJS Engineer**: Core backend development patterns.
- **TypeScript Expert**: Advanced TS features and type safety.
- **Message Queues**: Handling asynchronous tasks in Node.js.

---

## ☕ Spring Boot Configuration (`.claude`)

The original Java-based configuration, optimized for enterprise Spring Boot applications.

### Specialized Agents
- **Spring Boot Engineer**: Core Spring framework expert.
- **Java Architect**: High-level system design for JVM.
- **DevOps & Kubernetes**: Cloud-native deployment specialists.

### Key Skills
- **JPA Patterns**: Hibernate and JPA optimization.
- **Spring Security**: Robust authentication and authorization.
- **Testing Patterns**: JUnit/Mockito strategies for enterprise apps.
