# Tech Stack

**Last Updated**: [Date]  
**Version**: 1.0.0

---

## Languages

- **Primary**: [Language + version, e.g., TypeScript 5.3]
- **Build**: [Tool + version, e.g., Vite 5.0]
- **Runtime**: [Node 20 LTS / Python 3.12 / Ruby 3.2]

---

## Framework

- **Backend**: [Framework + version, e.g., Next.js 14 / Django 5.0 / Rails 7.1]
- **Frontend**: [Framework + version, e.g., React 18 / Vue 3 / Angular 17]
- **Testing**: [Framework + version, e.g., Vitest / Jest / pytest]

---

## Database

- **Type**: [PostgreSQL / MySQL / MongoDB]
- **Version**: [e.g., PostgreSQL 16]
- **ORM**: [Prisma / TypeORM / Sequelize / SQLAlchemy / ActiveRecord]
- **Migrations**: [Tool / strategy, e.g., Prisma Migrate / Alembic]

---

## Key Libraries

### State Management
- **Tool**: [Zustand / Redux Toolkit / Context API / Pinia]
- **When to use**: [Define when to reach for global state]

### Forms
- **Tool**: [React Hook Form / Formik / VeeValidate]
- **Validation**: [Zod / Yup / Joi / Valibot]

### API
- **Type**: [REST / GraphQL / tRPC]
- **Client**: [Fetch / Axios / Apollo / tRPC client]

### Styling
- **Tool**: [Tailwind CSS / CSS Modules / styled-components / Sass]
- **Theme**: [shadcn/ui / MUI / Custom]

---

## Naming Conventions

### Files

| Type | Pattern | Example |
|------|---------|---------|
| Component | `<Entity><Action>.tsx` | `CreateUserDialog.tsx` |
| Hook | `use<Entity><Op>.ts` | `useUsersList.ts` |
| API Route | `<entity>.[ts\|py\|rb]` | `users.ts` |
| Schema | `<entity>Schema.ts` | `userSchema.ts` |
| Test | `<name>.test.ts` | `user.test.ts` |
| Server Action | `<action><Entity>Action.ts` | `createUserAction.ts` |
| Server Query | `<query><Entity>Query.ts` | `listUsersQuery.ts` |

### Functions

| Type | Pattern | Example |
|------|---------|---------|
| Component | `PascalCase` | `UserProfile` |
| Hook | `use + PascalCase` | `useUserData` |
| Utility | `camelCase` | `formatDate` |
| Constant | `UPPER_SNAKE` | `MAX_RETRIES` |
| Server Action | `<verb><Entity>` | `createUser` |

### Variables

| Type | Pattern | Example |
|------|---------|---------|
| Boolean | `is/has/can + Noun` | `isActive`, `hasPermission`, `canDelete` |
| Array | `plural` | `users`, `items`, `products` |
| Single | `singular` | `user`, `item`, `product` |
| Handler | `handle + Action` | `handleClick`, `handleSubmit` |

---

## Code Style

- **Formatting**: [Prettier / Black / RuboCop / rustfmt]
- **Linting**: [ESLint / Flake8 / RuboCop / clippy]
- **Type Checking**: [TypeScript strict mode / mypy / Sorbet]
- **Line Length**: [80 / 100 / 120 chars]
- **Quotes**: [Single / Double]
- **Semicolons**: [Required / Optional]

---

## Testing Strategy

### Unit Tests
- **Framework**: [Jest / Vitest / pytest / RSpec]
- **Coverage Target**: [80% / 70% / custom]
- **Location**: [Co-located with source / separate __tests__ folder]

### Integration Tests
- **Framework**: [Same as unit / Supertest / TestClient]
- **Scope**: [API endpoints / Service layer]

### E2E Tests
- **Framework**: [Playwright / Cypress / Selenium]
- **Scope**: [Critical user flows only / Full app]
- **When to run**: [CI / Pre-deploy / Nightly]

---

## Project-Specific Patterns

### Pattern 1: [e.g., CRUD Bridge Pattern]

**When to use**: Creating standard list/detail/create/update/delete flows

**Structure**:
```typescript
// hooks/use<Entity>Crud.ts
const { 
  useList, 
  useItem, 
  useLite, 
  useCreateAction, 
  useUpdateAction, 
  useDeleteAction 
} = createCrudBridge({
  queryKey: "products",
  listServer: listProductsServer,
  itemServer: getProductServer,
  // ...
});
```

### Pattern 2: [Your custom pattern]

**When to use**: [Scenario]

**Example**:
```[language]
[Code example]
```

---

## Anti-Patterns (BANNED)

❌ **Using `any` type without justification**
```typescript
// NEVER
const data: any = fetchData()  // ❌

// INSTEAD
const data: UserData = fetchData()  // ✅
```

❌ **Not validating user input**
```typescript
// NEVER
const createUser = async (data) => {
  await db.user.create({ data })  // ❌ No validation!
}

// INSTEAD
const createUser = async (input: unknown) => {
  const data = createUserSchema.parse(input)  // ✅ Zod validation
  await db.user.create({ data })
}
```

❌ **Mixing data fetching with UI components**
```typescript
// NEVER - fetch in component
const UserList = () => {
  const [users, setUsers] = useState([])
  useEffect(() => {
    fetch('/api/users').then(r => r.json()).then(setUsers)
  }, [])
}

// INSTEAD - use hook
const UserList = () => {
  const { data: users } = useUsersList()
}
```

---

## Environment Variables

### Required
- `DATABASE_URL`: PostgreSQL connection string
- `NEXTAUTH_SECRET`: Auth secret key
- `[YOUR_REQUIRED_VARS]`

### Optional
- `NEXT_PUBLIC_API_URL`: API base URL (defaults to relative)
- `[YOUR_OPTIONAL_VARS]`

### Naming
- Public (client-side): `NEXT_PUBLIC_*` / `VITE_*` / `REACT_APP_*`
- Private (server-only): `DATABASE_*` / `API_*` / `SECRET_*`

---

## Notes

- Keep this file updated when adding new libraries
- Document any deviations from conventions
- Add examples from actual codebase
- Review when onboarding new developers
