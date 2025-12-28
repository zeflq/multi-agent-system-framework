# Templates Directory

**Note**: This file will become `templates/README.md` when you copy it to your GitHub repo.

Ready-to-use templates for multi-agent development system.

---

## 📁 Directory Structure

```
templates/
├─ agents/                          ← Agent specifications
│  ├─ conventions.md                ← Generic dev principles (REQUIRED)
│  ├─ brain-agent.md                ← Orchestrator (REQUIRED)
│  ├─ agent-template.md             ← Blank template for new agents
│  │
│  └─ Examples (ready to use):
│     ├─ ux-agent.md                ← UX/UI specialist
│     ├─ react-agent.md             ← React specialist
│     ├─ nextjs-agent.md            ← Next.js specialist
│     └─ backend-agent.md           ← Backend specialist
│
├─ rules/                           ← Project-specific architecture
│  ├─ 01-architecture.md            ← Your architecture patterns (CUSTOMIZE!)
│  └─ 02-tech-stack.md              ← Your tech stack & conventions (CUSTOMIZE!)
│
└─ docs/adr/                        ← Decision records
   └─ ADR-000-template.md           ← ADR template
```

---

## 🚀 Quick Start

### Step 1: Copy Required Files

```bash
# In your project root:

# Copy core templates
cp templates/agents/conventions.md .claude/agents/_shared/
cp templates/agents/brain-agent.md .claude/agents/

# Copy project rules (MUST CUSTOMIZE THESE!)
cp templates/rules/01-architecture.md .claude/rules/
cp templates/rules/02-tech-stack.md .claude/rules/

# Copy ADR template
cp templates/docs/adr/ADR-000-template.md docs/adr/
```

### Step 2: Add Specialist Agents (Optional)

```bash
# Copy the agents you need:
cp templates/agents/react-agent.md .claude/agents/
cp templates/agents/backend-agent.md .claude/agents/
cp templates/agents/ux-agent.md .claude/agents/
cp templates/agents/nextjs-agent.md .claude/agents/
```

### Step 3: Customize Project Rules

**CRITICAL**: Edit these files with YOUR actual patterns:

1. **`.claude/rules/01-architecture.md`**
   - Replace `[Your Architecture Pattern]` with your choice
   - Add your folder structure
   - Add real examples from your codebase

2. **`.claude/rules/02-tech-stack.md`**
   - Replace all `[placeholders]` with your tech
   - Add your naming conventions
   - Add your project-specific patterns

---

## 📝 File Descriptions

### Core Templates (REQUIRED)

#### `agents/conventions.md`
- **What**: Generic development principles
- **Apply to**: ALL agents, ANY project
- **Customize**: ❌ No - use as-is
- **Purpose**: Shared rules (KISS, YAGNI, slicing, ADR process)

#### `agents/brain-agent.md`
- **What**: Orchestrator agent
- **Apply to**: Every project
- **Customize**: ✅ Update "Agent Roster" section
- **Purpose**: Coordinates specialists, enforces slicing

#### `rules/01-architecture.md`
- **What**: YOUR architecture patterns
- **Apply to**: Your specific project
- **Customize**: ✅✅✅ MUST customize!
- **Purpose**: Defines structure, boundaries, rules

#### `rules/02-tech-stack.md`
- **What**: YOUR tech choices & conventions
- **Apply to**: Your specific project
- **Customize**: ✅✅✅ MUST customize!
- **Purpose**: Languages, frameworks, naming, patterns

#### `docs/adr/ADR-000-template.md`
- **What**: Decision record template
- **Apply to**: All architectural decisions
- **Customize**: ❌ No - use as-is
- **Purpose**: Document important decisions

---

### Specialist Agent Templates (EXAMPLES)

#### `agents/ux-agent.md`
- **What**: UX/UI design specialist
- **When to use**: Projects with UX requirements
- **Customize**: Minimal - update for your design system

#### `agents/react-agent.md`
- **What**: React component specialist
- **When to use**: React/Next.js projects
- **Customize**: Minimal - add project-specific patterns

#### `agents/nextjs-agent.md`
- **What**: Next.js App Router specialist
- **When to use**: Next.js projects
- **Customize**: Minimal - adjust for your routing

#### `agents/backend-agent.md`
- **What**: API & database specialist
- **When to use**: Projects with backend
- **Customize**: Adjust for your backend tech

---

### Blank Template

#### `agents/agent-template.md`
- **What**: Template for creating NEW agents
- **When to use**: Need a custom agent (testing, deployment, etc.)
- **How to use**:
  1. Copy file: `cp agent-template.md my-new-agent.md`
  2. Replace all `[placeholders]`
  3. Add domain-specific rules

---

## ✅ Verification Checklist

After copying templates:

- [ ] `.claude/agents/_shared/conventions.md` exists
- [ ] `.claude/agents/brain-agent.md` exists
- [ ] `.claude/agents/brain-agent.md` has YOUR agent roster updated
- [ ] `.claude/rules/01-architecture.md` exists and is CUSTOMIZED
- [ ] `.claude/rules/02-tech-stack.md` exists and is CUSTOMIZED
- [ ] `docs/adr/ADR-000-template.md` exists
- [ ] At least 2 specialist agents copied

---

## 🎯 What to Customize

### High Priority (MUST DO)

1. **`rules/01-architecture.md`**
   - [ ] Choose architecture pattern
   - [ ] Add your folder structure
   - [ ] Add real code examples
   - [ ] Define your specific rules

2. **`rules/02-tech-stack.md`**
   - [ ] List your actual tech stack
   - [ ] Define naming conventions
   - [ ] Add environment variables
   - [ ] Document patterns

3. **`agents/brain-agent.md`**
   - [ ] Update "Agent Roster" with your agents

### Medium Priority (SHOULD DO)

4. **Specialist agents**
   - [ ] Remove agents you don't need
   - [ ] Add project-specific patterns
   - [ ] Update examples to match your codebase

### Low Priority (NICE TO HAVE)

5. **`agents/conventions.md`**
   - Generally use as-is
   - Only modify if team has strong opinions

---

## 🔄 Usage Workflow

1. **Initial Setup** (Once)
   ```bash
   # Copy all required templates
   # Customize project rules
   # Add specialist agents
   ```

2. **Create Feature** (Ongoing)
   ```bash
   # Ask brain-agent to slice work
   # Specialist agents execute slices
   # Follow handoff contracts
   ```

3. **Add New Agent** (As Needed)
   ```bash
   # Copy agent-template.md
   # Customize for domain
   # Update brain-agent roster
   ```

4. **Update Rules** (Quarterly)
   ```bash
   # Review architecture.md
   # Update tech-stack.md
   # Refine based on learnings
   ```

---

## 📚 Additional Resources

- **Blog Post**: [Link to your blog post]
- **Visual Guide**: `../docs/visual-architecture-guide.md`
- **Quick Start**: `../docs/quick-start-guide.md`

---

## ❓ FAQ

### Q: Which files are required?
**A**: Minimum required:
- `agents/conventions.md`
- `agents/brain-agent.md`
- `rules/01-architecture.md` (customized)
- `rules/02-tech-stack.md` (customized)

### Q: Can I use this with Django/Rails/etc?
**A**: Yes! The core templates (conventions, brain-agent) are tech-agnostic. Just:
1. Skip react/nextjs agents
2. Create your own specialist agents
3. Customize the rules files

### Q: Do I need all specialist agents?
**A**: No. Only copy the agents you need. For example:
- **Backend-only API**: backend-agent + data-agent
- **Frontend SPA**: react-agent + api-integration-agent
- **Full-stack**: All agents

### Q: Can I modify conventions.md?
**A**: You can, but it's not recommended. It's designed to be generic and stable. Better to add project-specific rules in `rules/` folder.

---

**Ready to start?** Follow the Quick Start guide above! 🚀