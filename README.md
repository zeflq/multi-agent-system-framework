# Multi-Agent Development System Framework

**A production-ready framework for building AI-powered multi-agent development systems**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

---

## 🎯 What Is This?

A complete framework for implementing **multi-agent AI development systems** with:
- ✅ Clear separation of concerns (specialist agents)
- ✅ Explicit contracts between agents (handoffs)
- ✅ Architectural governance (brain-agent orchestration)
- ✅ Ready-to-use templates
- ✅ Works with ANY tech stack

---

## 📖 Read the Guide

**📝 [Complete Blog Post on dev.to](https://dev.to/zeflq/stop-fighting-context-limits-how-multi-agent-systems-solved-my-development-chaospart-1-2a4a)**

The blog post covers:
- Why multi-agent systems solve development complexity
- Complete architecture breakdown
- Step-by-step implementation
- Real-world examples
- Best practices and lessons learned

---

## ⚡ Quick Start

Get your multi-agent system running in **30 minutes**:

```bash
# 1. Clone this repo
git clone https://github.com/zeflq/multi-agent-system-framework.git
cd multi-agent-system-framework

# 2. Copy templates to your project
cp -r templates/agents /path/to/your-project/.claude/agents
cp -r templates/rules /path/to/your-project/.claude/rules
cp -r templates/docs/adr /path/to/your-project/docs/adr

# 3. Customize for your project
# Edit .claude/rules/*.md with your architecture
# Update .claude/agents/brain-agent.md with your agent roster

# 4. Test with brain-agent
# Ask: "brain-agent: create a user profile page"
```

**Full guide**: [docs/quick-start-guide.md](./docs/quick-start-guide.md)

---

## 📂 What's Included

### Templates (Ready to Copy)

```
templates/
├─ agents/
│  ├─ conventions.md           ← Generic dev principles
│  ├─ brain-agent.md           ← Orchestrator
│  ├─ agent-template.md        ← Blank template for new agents
│  │
│  └─ Examples (ready to use):
│     ├─ ux-agent.md           ← UX specialist
│     ├─ react-agent.md        ← React specialist
│     ├─ nextjs-agent.md       ← Next.js specialist
│     └─ backend-agent.md      ← Backend specialist
│
├─ rules/
│  ├─ 01-architecture.md       ← Your architecture patterns
│  └─ 02-tech-stack.md         ← Your tech stack & conventions
│
└─ docs/adr/
   └─ ADR-000-template.md      ← Decision template
```

**See full templates guide**: [templates/README.md](./templates/README.md)

### Documentation

- **[Quick Start Guide](./docs/quick-start-guide.md)** - 30-min setup
- **[Visual Architecture Guide](./docs/visual-architecture-guide.md)** - Diagrams and flows

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────┐
│  brain-agent (Orchestrator)             │
│  • Slices work into XS/S chunks         │
│  • Routes to specialists                │
│  • Enforces ADR for big decisions       │
└─────────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────────┐
│  Specialist Agents                      │
│  • ux-agent (flows, states)             │
│  • react-agent (components, hooks)      │
│  • backend-agent (API, database)        │
│  • [Your custom agents...]             │
└─────────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────────┐
│  Shared Foundation                      │
│  • conventions.md (generic rules)       │
│  • project-rules/ (your architecture)   │
│  • docs/adr/ (decisions)                │
└─────────────────────────────────────────┘
```

**[See full diagrams →](./docs/visual-architecture-guide.md)**

---

## 🎓 Learn More

### Core Concepts

| Concept | What It Is | Example |
|---------|-----------|---------|
| **Slice** | Small, shippable work unit (XS: 1-2h, S: 0.5-1d) | Create login form |
| **Handoff** | Contract between agents | react-agent → next-agent |
| **ADR** | Architectural decision record | Auth strategy decision |
| **brain-agent** | Orchestrator that routes work | Coordinates all agents |

### Key Benefits

- ✅ **Separation of Concerns**: Each agent is a domain expert
- ✅ **Explicit Contracts**: No assumptions between layers
- ✅ **Architectural Governance**: ADRs prevent drift
- ✅ **Scalable**: Add agents as complexity grows
- ✅ **Tech-Agnostic**: Works with any stack

---

## 📚 Documentation

### Getting Started
- [Quick Start Guide (30 min)](./docs/quick-start-guide.md)
- [Visual Architecture Guide](./docs/visual-architecture-guide.md)
- [Templates Guide](./templates/README.md)

### Reference
- [Generic Agent Template](./templates/agents/agent-template.md)
- [Brain Agent Template](./templates/agents/brain-agent.md)
- [Conventions Template](./templates/agents/conventions.md)
- [ADR Template](./templates/docs/adr/ADR-000-template.md)

### Specialist Agents (Examples)
- [UX Agent](./templates/agents/ux-agent.md)
- [React Agent](./templates/agents/react-agent.md)
- [Next.js Agent](./templates/agents/nextjs-agent.md)
- [Backend Agent](./templates/agents/backend-agent.md)

---

## 🛠️ Customization

This framework is a **starting point**, not a rigid prescription.

### For Your Tech Stack

The templates work with:
- ✅ Next.js / React / Vue / Angular
- ✅ Django / Flask / FastAPI
- ✅ Rails / Laravel / Phoenix
- ✅ Spring Boot / ASP.NET
- ✅ Microservices / Monoliths
- ✅ Any combination!

### For Your Architecture

Support for:
- ✅ Feature-first vertical slices
- ✅ Clean Architecture (Hexagonal)
- ✅ Domain-Driven Design
- ✅ Layered Architecture
- ✅ Microservices
- ✅ Modular Monoliths

**Customize**: `templates/rules/01-architecture.md` with your patterns

---

## 🤝 Contributing

Contributions welcome! Here's how:

### Share Your Implementation

Have you used this framework? Share your example:

1. Fork this repo
2. Add your example to `examples/your-stack/`
3. Include README with:
   - Your tech stack
   - Agent configuration
   - Learnings and challenges
4. Submit PR

### Improve Templates

Found a better way? Improve the templates:

1. Update templates in `templates/`
2. Document your reasoning
3. Test with a real project
4. Submit PR

### Report Issues

Found a bug or have a suggestion?

- [Open an issue](https://github.com/zeflq/multi-agent-system-framework/issues)
- Describe your use case
- Include error messages if applicable

---

## 📊 Success Stories

*Want to be featured here? Share your implementation!*

Projects using this framework:
- **Your project could be here!** - Submit a PR to add your success story

---

## 📝 License

MIT License - see [LICENSE](./LICENSE) file

**TL;DR**: Use freely, adapt for your needs, attribution appreciated but not required.

---

## 🙏 Acknowledgments

Inspired by:
- Clean Architecture (Robert C. Martin)
- Domain-Driven Design (Eric Evans)
- Vertical Slice Architecture (Jimmy Bogard)
- Feature Slices (various)

Built with learnings from real production systems.

---

## 📮 Stay Updated

- ⭐ Star this repo for updates
- 👀 Watch for new examples
- 🐦 Follow [@flq](https://x.com/flq) *(optional - remove if not applicable)*
- 📝 Read the blog: [dev.to/zeflq](https://dev.to/zeflq)

> **Note**: Update social media links with your actual handles or remove if not applicable

---

## 💬 Community

- **Questions?** [Open a discussion](https://github.com/zeflq/multi-agent-system-framework/discussions)
- **Issues?** [Report here](https://github.com/zeflq/multi-agent-system-framework/issues)
- **Chat?** *(Add Discord/Slack link if you create one, otherwise remove this line)*

---

## 🚀 Quick Links

- 📖 [Read the full blog post](https://dev.to/zeflq/building-production-ready-ai-agent-systems)
- ⚡ [Quick Start (30 min)](./docs/quick-start-guide.md)
- 🎨 [Visual Architecture](./docs/visual-architecture-guide.md)
- 📋 [Copy Templates](./templates/)
- 💡 [Share Your Example](https://github.com/zeflq/multi-agent-system-framework/issues/new)

**Ready to build your multi-agent system?** [Start here →](./docs/quick-start-guide.md)