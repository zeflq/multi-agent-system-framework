# Project Architecture

**Last Updated**: [Date]  
**Version**: 1.0.0

---

## Pattern: [Your Architecture Pattern]

**Choose one and describe**:
- Feature-First Vertical Slices
- Clean Architecture (Hexagonal)
- Layered Architecture
- Domain-Driven Design
- Microservices
- Modular Monolith

**Description**: [Explain your chosen pattern and why you chose it]

---

## Folder Structure

```
[Show your actual project structure]

Example for feature-first:
src/
├─ features/
│  └─ <entity>/
│     ├─ model/       # Schemas, types, validation
│     ├─ server/      # Backend logic (use cases, repos)
│     ├─ hooks/       # Data fetching hooks
│     ├─ components/  # UI components
│     └─ index.ts     # Public API
├─ lib/               # Shared utilities
└─ app/               # Next.js App Router pages
```

---

## Core Principles

1. **[Principle 1]**: [Description]
   - Example: Feature isolation
   - Rule: No cross-feature internal imports

2. **[Principle 2]**: [Description]
   - Example: Public API contracts
   - Rule: Export through index.ts only

3. **[Principle 3]**: [Description]
   - Example: Dependency flow
   - Rule: Always inward, never outward

---

## Rules

### Rule 1: [Name - e.g., Feature Isolation]

**Description**: Each feature is self-contained with its own models, logic, and UI.

**DO:**
```typescript
// ✅ CORRECT - Import from feature's public API
import { useUsersList } from '@/features/users'
```

**DON'T:**
```typescript
// ❌ FORBIDDEN - Direct import of internals
import { UserRepository } from '@/features/users/server/repositories/userRepository'
```

### Rule 2: [Name - e.g., Layer Boundaries]

**Description**: [What this rule enforces]

**DO:**
```typescript
// ✅ CORRECT
[Your example]
```

**DON'T:**
```typescript
// ❌ FORBIDDEN
[Your anti-pattern]
```

---

## Directory Guidelines

| Directory | Purpose | Allowed | Forbidden |
|-----------|---------|---------|-----------|
| `/features` | Domain features | Feature code | Cross-feature imports |
| `/lib` | Shared utilities | Generic helpers | Business logic |
| `/components` | Shared UI | Reusable components | Feature-specific code |
| `/app` | Next.js routes | Routing, layouts | Business logic |

---

## Examples

### Creating a New Feature

```bash
# 1. Create feature folder
mkdir -p src/features/products

# 2. Create structure
cd src/features/products
mkdir model server hooks components

# 3. Create public API
touch index.ts
```

### Proper Feature Structure

```typescript
// src/features/products/index.ts
// Public API - Only export what other features need

export { useProductsList } from './hooks/useProductsList'
export { useProductItem } from './hooks/useProductItem'
export type { Product } from './model/productSchema'
```

---

## Anti-Patterns (BANNED)

❌ **Cross-feature internal imports**
```typescript
// NEVER do this
import { UserRepository } from '@/features/users/server/repositories/userRepository'
```

❌ **Business logic in UI components**
```typescript
// NEVER do this
const ProductCard = () => {
  const handleDelete = async () => {
    await prisma.product.delete({ where: { id } })  // ❌
  }
}
```

❌ **Shared mutable state between features**
```typescript
// NEVER do this - globals.ts
export const userCache = new Map()  // ❌
```

---

## Notes

- Keep this file updated as architecture evolves
- Add real examples from your codebase
- Document exceptions and why they exist
- Review quarterly and refine
