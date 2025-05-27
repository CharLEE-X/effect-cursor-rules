# Effect Cursor Rules

A comprehensive collection of Cursor IDE rules for building modern TypeScript applications with Effect-TS, React Router v7, and AWS infrastructure.

## 🚀 Quick Start

1. Browse the [rules directory](./rules/) to find the patterns you need
2. Copy the `.mdc` files to your project's `.cursorrules/rules` directory
3. Cursor will pick them up automatically

## 📋 Available Rules

### Core Architecture
- **[effect-service-architecture.mdc](./rules/effect-service-architecture.mdc)** - Service layer patterns with Effect-TS
- **[effect-store-patterns.mdc](./rules/effect-store-patterns.mdc)** - Data access layer patterns
- **[effect-handler-patterns.mdc](./rules/effect-handler-patterns.mdc)** - HTTP handler patterns
- **[effect-usecase-patterns.mdc](./rules/effect-usecase-patterns.mdc)** - Business logic patterns
- **[effect-testing-patterns.mdc](./rules/effect-testing-patterns.mdc)** - Testing strategies with Effect-TS

### Frontend Development
- **[react-router-v7-patterns.mdc](./rules/react-router-v7-patterns.mdc)** - React Router v7 resource routes
- **[responsive-design-patterns.mdc](./rules/responsive-design-patterns.mdc)** - Mobile-first responsive design
- **[frontend-translation-management.mdc](./rules/frontend-translation-management.mdc)** - i18n patterns

### Infrastructure & DevOps
- **[infrastructure-stack-patterns.mdc](./rules/infrastructure-stack-patterns.mdc)** - AWS CDK patterns
- **[nx-rules.mdc](./rules/nx-rules.mdc)** - Nx monorepo patterns

### API & Testing
- **[api-client-patterns.mdc](./rules/api-client-patterns.mdc)** - API client architecture
- **[api-client-testing.mdc](./rules/api-client-testing.mdc)** - API testing strategies
- **[schema-validation.mdc](./rules/schema-validation.mdc)** - Data validation patterns

### Code Quality & Maintenance
- **[code-style.mdc](./rules/code-style.mdc)** - TypeScript code style guide
- **[cursor-rule-maintainer.mdc](./rules/cursor-rule-maintainer.mdc)** - Maintaining cursor rules
- **[readme-maintenance.mdc](./rules/readme-maintenance.mdc)** - Documentation patterns
- **[ai-tools-maintenance.mdc](./rules/ai-tools-maintenance.mdc)** - AI-assisted development

## 🏗️ Architecture Philosophy

These rules promote:

- **Effect-TS First**: Functional programming with Effect-TS for type-safe, composable code
- **Layered Architecture**: Clear separation between handlers, usecases, and stores
- **Type Safety**: Comprehensive TypeScript patterns with Effect Schema validation
- **Testing**: Property-based testing and dependency injection for reliable code
- **Modern React**: React Router v7 with resource routes and server-side rendering
- **AWS Native**: CDK-based infrastructure with serverless patterns

## 📁 Project Structure

The rules assume this project structure:

```
src/
├── components/          # React components (pure, presentational)
├── routes/             # React Router v7 routes
│   ├── api/           # Server-side route handlers
│   └── ui/            # Client-side route components
├── hooks/             # Effect-based React hooks
├── .server/           
│   ├── services/      # Effect-TS service implementations
│   ├── stores/        # Effect-based state management
│   ├── config/        # Effect-TS Config management
│   └── errors/        # Tagged error types
├── __types/           # Shared TypeScript types
├── tests/             # Tests co-located with source
└── e2e/               # Playwright E2E tests
```

## 🎯 Key Patterns

### Service Architecture
```typescript
export class BlogStore extends Effect.Service<BlogStore>()('BlogStore', {
  dependencies: [DynamoDBService, ConfigService],
  effect: Effect.gen(function* () {
    const dynamodb = yield* DynamoDBService
    const config = yield* ConfigService
    
    return {
      create: (blogPost: BlogPost) => Effect.gen(function* () {
        // Implementation
      }),
      getById: (id: BlogPostId) => Effect.gen(function* () {
        // Implementation  
      }),
    }
  }),
}) {}
```

### Error Handling
```typescript
export class NotFoundError extends Data.TaggedError('NotFoundError')<{
  readonly resource: string
  readonly id: string
}> {}

// Usage
Effect.catchTags({
  NotFoundError: (error) => notFoundResponse(error.message),
  ConflictError: (error) => conflictResponse(error.message),
})
```

### React Router v7 Resource Routes
```typescript
export async function loader({ params }: LoaderFunctionArgs) {
  const blogPost = await getBlogPostUsecase(params.id).pipe(
    Effect.provide(BlogStore.Default),
    Effect.runPromise
  )
  return json({ blogPost })
}
```

## 🧪 Testing Approach

- **Unit Tests**: Every service with Effect-TS dependency injection
- **Property Tests**: Pure functions with fast-check
- **E2E Tests**: Critical paths with Playwright
- **Mocking**: Effect services with test layers

## 🚀 Getting Started

1. **Choose Your Rules**: Select the `.mdc` files relevant to your project
2. **Configure Cursor**: Place rules in your `.cursorrules` directory
3. **Adapt Patterns**: Modify rules to match your specific needs
4. **Contribute Back**: Share improvements via pull requests

## 📖 Documentation

Each rule file includes:
- ✅ **Correct patterns** with examples
- ❌ **Anti-patterns** to avoid
- 📝 **Detailed explanations** of architectural decisions
- 🔧 **Configuration examples**

## 🤝 Contributing

Contributions are welcome! Please:

1. Follow the existing pattern format
2. Include both positive and negative examples
3. Add clear explanations for architectural decisions
4. Test rules with real projects before submitting

## 📄 License

This project is released under the [MIT License](./LICENCE.md). You are free to use, modify, and distribute these rules without any limitations.

## 🙏 Acknowledgments

These rules are based on real-world experience building production applications with:
- [Effect-TS](https://effect.website/) - Functional programming library
- [React Router v7](https://reactrouter.com/) - Full-stack React framework
- [AWS CDK](https://aws.amazon.com/cdk/) - Infrastructure as code
- [Cursor IDE](https://cursor.sh/) - AI-powered code editor

---

**Happy coding!** 🎉
