# Multi-Agent System: Quick Start Guide

Get your multi-agent system running in **30 minutes**.

---

## Step 1: Create Directory Structure (5 min)

```bash
mkdir -p .claude/agents/_shared
mkdir -p .claude/rules
mkdir -p docs/adr

touch .claude/CLAUDE.md
touch .claude/agents/_shared/conventions.md
touch .claude/agents/brain-agent.md
touch .claude/rules/01-architecture.md
touch .claude/rules/02-tech-stack.md
touch docs/adr/ADR-000-template.md
```

---

## Step 2: Create Core Files (10 min)

### `.claude/CLAUDE.md`

```markdown
# [Your Project Name]

**Architecture**: [Feature-first / Modular monolith / Microservices]
**Tech Stack**: [Your primary technologies]

---

## Quick Overview

This project uses a multi-agent development system:
- **brain-agent**: Orchestrates work, enforces decisions
- **[your-agent-1]**: Owns [domain]
- **[your-agent-2]**: Owns [domain]

---

## Rules

All agents follow:
- Generic conventions: `.claude/agents/_shared/conventions.md`
- Project patterns: `.claude/rules/*.md` (auto-loaded)

---

## Getting Started

1. Review architecture: `.claude/rules/01-architecture.md`
2. Check tech stack: `.claude/rules/02-tech-stack.md`
3. Use brain-agent for new features: `brain-agent: [your request]`
```

---

### `.claude/agents/_shared/conventions.md`

Copy from the blog post or use this minimal version:

```markdown
---
name: _shared-conventions
description: Generic development principles for all agents
---

# Shared Development Conventions

## 1. Core Principles
- KISS: Simplest solution that works
- YAGNI: Don't build for hypothetical needs
- Explicit over implicit

## 2. Small Slices
- XS: 1-2 hours
- S: 0.5-1 day
- Each slice: one goal, one owner

## 3. Contracts Required
- Never assume behavior
- Document all boundaries
- Explicit handoffs between agents

## 4. Change Safety
- Prefer additive changes
- Breaking changes require approval
- Avoid touching unrelated code

## 5. ADR for Structural Decisions
When a change affects architecture or shared contracts:
- Create ADR in `docs/adr/`
- Status: Proposed → wait for approval → Accepted
- Low-risk decisions don't need ADR

## 6. Integration Checkpoints
Every slice ends with: `Integrated: Yes / No`
```

---

### `.claude/rules/01-architecture.md`

**Customize this for YOUR project**:

```markdown
# Project Architecture

## Pattern: [Your Pattern Here]

[Describe your architecture]

Example:
- Feature-First Vertical Slices
- Clean Architecture (Hexagonal)
- Domain-Driven Design
- Layered Architecture
- Microservices

## Folder Structure

```
[Show your actual structure]
```

## Key Rules

1. **[Rule 1]**: [Description]
2. **[Rule 2]**: [Description]
3. **[Rule 3]**: [Description]

## Examples

```typescript
// ✅ CORRECT
[Your example]

// ❌ FORBIDDEN
[Anti-pattern]
```
```

---

### `.claude/rules/02-tech-stack.md`

**Fill in YOUR tech stack**:

```markdown
# Tech Stack

## Framework
- **Primary**: [Next.js / Django / Rails / etc.]
- **Version**: [Version number]

## Database
- **Type**: [PostgreSQL / MySQL / MongoDB]
- **ORM**: [Prisma / TypeORM / SQLAlchemy]

## Languages
- **Backend**: [TypeScript / Python / Ruby]
- **Frontend**: [TypeScript + React / Vue / etc.]

## Key Libraries
- **State Management**: [Zustand / Redux / etc.]
- **Forms**: [React Hook Form / Formik]
- **Validation**: [Zod / Yup / Joi]
- **API**: [tRPC / REST / GraphQL]

## Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| Component | `<Entity><Action>` | `CreateUserDialog` |
| Hook | `use<Entity><Op>` | `useUsersList` |
| API Endpoint | `/api/<entity>` | `/api/users` |
| Database Table | `<entity>s` | `users` |

[Add more patterns specific to your stack]

## Code Style
- **Formatting**: Prettier
- **Linting**: ESLint
- **Type Checking**: TypeScript strict mode

## Testing
- **Unit**: [Jest / Vitest / pytest]
- **E2E**: [Playwright / Cypress]
- **Coverage**: Minimum 70% for critical paths
```

---

## Step 3: Create Your First Agent (10 min)

Choose based on your project:

### Option A: Full-Stack (Next.js/React)

Create these agents:
- `brain-agent.md` (orchestrator)
- `react-agent.md` (UI components)
- `next-agent.md` (routing, server actions)
- `backend-agent.md` (API, database)

### Option B: Backend-Only (API)

Create these agents:
- `brain-agent.md` (orchestrator)
- `api-agent.md` (endpoints, contracts)
- `data-agent.md` (database, migrations)
- `service-agent.md` (business logic)

### Option C: Frontend-Only (SPA)

Create these agents:
- `brain-agent.md` (orchestrator)
- `ui-agent.md` (components, state)
- `data-agent.md` (API integration, caching)

---

### Minimal Agent Template

```markdown
---
name: [agent-name]
description: Owns [responsibilities]. Delivers [outputs].
---

You are **[agent-name]** (senior-level).

You own **[domain]** with focus on:
- [quality 1]
- [quality 2]
- [quality 3]

You MUST follow:
- `/.claude/agents/_shared/conventions.md`
- `/.claude/rules/*.md`

---

## Scope

**You own:**
- [Responsibility 1]
- [Responsibility 2]

**You do NOT own:**
- [Boundary 1] → [other-agent]
- [Boundary 2] → [other-agent]

---

## Key Rules

### [Category 1]
- Rule 1
- Rule 2

### [Category 2]
- Rule 1
- Rule 2

---

## ADR Triggers

Propose ADR when:
- [Trigger 1]
- [Trigger 2]

---

## Handoff Contract

```markdown
### HANDOFF
**From**: [agent-name]
**To**: [target-agent]
**Slice-ID**: SLC-###

**Goal**: (1 sentence)
**Scope**: [What's included]
**Out of scope**: [What's not]
**Files changed**: [List]
**Public contract**: [API/props/types]
**How to test**: [Steps]
**Integrated**: Yes / No
```
```

---

### Create `brain-agent.md`

Use the brain-agent template from the blog post, or this minimal version:

```markdown
---
name: brain-agent
description: Orchestrates multi-agent development
---

You are **brain-agent** (Lead Architect).

You turn user requests into:
1. Small slices (XS: 1-2h, S: 0.5-1d)
2. Agent assignments
3. Handoff contracts
4. Integration plan

You MUST enforce:
- `/.claude/agents/_shared/conventions.md`
- `/.claude/rules/*.md`

---

## Agent Roster

- **[agent-1]**: Owns [domain]
- **[agent-2]**: Owns [domain]
- **[agent-3]**: Owns [domain]

---

## Output Format

For every request, provide:

1. **Clarified Goal**: (1-2 sentences)
2. **Slices**: (XS or S only, with Slice-IDs)
3. **Assignments**: (which agent owns which slice)
4. **ADR Check**: (is ADR needed?)
5. **Handoff Contracts**: (for each agent)
6. **Integration Plan**: (how slices connect)
7. **Definition of Done**: (acceptance criteria)
8. **Risks**: (top 3-5)

---

## Sizing Rules

**XS (1-2h)**:
- One component or endpoint
- Minimal cross-agent coordination

**S (0.5-1d)**:
- Full screen or CRUD flow
- Limited integration

**Anything larger**: Split into multiple slices

---

## ADR Enforcement

If a slice:
- Affects architecture
- Changes shared contracts
- Introduces new patterns

→ Require ADR with status `Proposed`
→ Wait for user approval
→ Mark as `Accepted` before proceeding
```

---

## Step 4: Create ADR Template (5 min)

### `docs/adr/ADR-000-template.md`

```markdown
# ADR-XXX: [Title]

**Status**: Proposed | Accepted | Superseded  
**Date**: YYYY-MM-DD  
**Author**: [Name]

---

## Context

What problem are we solving?

---

## Decision

What are we deciding to do?

---

## Consequences

**Positive**:
- ✅ [Benefit 1]

**Negative**:
- ❌ [Trade-off 1]

**Risks**:
- ⚠️ [Risk 1]

---

## Alternatives Considered

**Option 1**: [Name]
- Rejected because: [Reason]

---

## Implementation

- [Key step 1]
- [Key step 2]
```

---

## Step 5: Test Your System (5 min)

### Create First Feature

Ask brain-agent:

```
brain-agent: Create a user profile page with name and email fields
```

Brain-agent should:
1. ✅ Break into small slices
2. ✅ Assign to appropriate agents
3. ✅ Provide handoff contracts
4. ✅ Define integration plan

### Validate Output

Check that brain-agent's response includes:
- [ ] Slice IDs (SLC-001, SLC-002, etc.)
- [ ] Agent assignments
- [ ] Handoff contracts with all required fields
- [ ] Clear testing instructions

---

## Common First-Time Issues

### Issue 1: Agents Don't Follow Your Patterns

**Problem**: Agents generate generic code, not your specific patterns

**Fix**: Ensure `.claude/rules/` files are detailed with examples

### Issue 2: Too Many Agents

**Problem**: Started with 10 agents, routing is confusing

**Fix**: Start with 3-4 core agents, add more only when needed

### Issue 3: Handoffs Too Vague

**Problem**: Contracts missing critical details

**Fix**: Use handoff checklist from blog post

---

## Next Steps

### Week 1: Foundation
- ✅ Set up file structure
- ✅ Create conventions.md
- ✅ Define architecture rules
- ✅ Create 3 core agents

### Week 2: First Feature
- Build one complete feature with agents
- Refine handoff contracts based on learnings
- Add missing fields to templates

### Week 3: Iteration
- Add project-specific rules
- Expand agent capabilities
- Create first ADR

### Week 4: Scale
- Add specialist agents as needed
- Document patterns in rules files
- Train team on agent system

---

## Resources

- **Full Blog Post**: [Link to comprehensive guide]
- **Templates**: All templates in one place
- **Example Project**: [GitHub repo]
- **Community**: [Discord/Forum]

---

## Troubleshooting

### "Agent doesn't know our architecture"

→ Add examples to `.claude/rules/01-architecture.md`

### "Brain-agent not routing correctly"

→ Update agent roster in `brain-agent.md`

### "Slices too large"

→ Enforce XS/S sizing in brain-agent rules

### "No integration between slices"

→ Add integration slice at end of epic

---

**You're ready!** Start with brain-agent and iterate.
