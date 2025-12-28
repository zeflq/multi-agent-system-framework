# Multi-Agent System: Visual Architecture Guide

Reference diagrams for understanding the system.

---

## 1. System Architecture (Three-Layer Model)

```
╔═══════════════════════════════════════════════════════════════╗
║  LAYER 1: ORCHESTRATION                                       ║
║                                                               ║
║  ┌─────────────────────────────────────────────────────────┐  ║
║  │  brain-agent (Orchestrator)                             │  ║
║  │  • Receives user request                                │  ║
║  │  • Breaks into slices (XS/S)                            │  ║
║  │  • Routes to specialists                                │  ║
║  │  • Enforces ADR                                         │  ║
║  │  • Validates integration                                │  ║
║  └─────────────────────────────────────────────────────────┘  ║
╚═══════════════════════════════════════════════════════════════╝
                            ↓  ↓  ↓
╔═══════════════════════════════════════════════════════════════╗
║  LAYER 2: SPECIALIST AGENTS                                   ║
║                                                               ║
║  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐            ║
║  │ ux-agent    │  │react-agent  │  │ next-agent  │            ║
║  │             │  │             │  │             │            ║
║  │ • Flows     │  │ • Components│  │ • Routing   │            ║
║  │ • States    │  │ • Hooks     │  │ • SSR/CSR   │            ║
║  │ • Content   │  │ • Forms     │  │ • Actions   │            ║
║  │ • A11y      │  │ • State     │  │ • Caching   │            ║
║  └─────────────┘  └─────────────┘  └─────────────┘            ║
║                                                               ║
║  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐            ║
║  │backend-agent│  │ data-agent  │  │test-agent   │            ║
║  │             │  │             │  │             │            ║
║  │ • APIs      │  │ • Schema    │  │ • E2E       │            ║
║  │ • DTOs      │  │ • Migrations│  │ • Integration│           ║
║  │ • Auth      │  │ • Queries   │  │ • Coverage  │            ║
║  │ • Validation│  │ • Indexes   │  │ • Fixtures  │            ║
║  └─────────────┘  └─────────────┘  └─────────────┘            ║
╚═══════════════════════════════════════════════════════════════╝
                            ↓  ↓  ↓
╔═══════════════════════════════════════════════════════════════╗
║  LAYER 3: SHARED FOUNDATION                                   ║
║                                                               ║
║  ┌────────────────────────────────────────────────────────┐   ║
║  │  conventions.md (Generic Principles)                   │   ║
║  │  • KISS, SOLID, YAGNI                                  │   ║
║  │  • Small slices                                        │   ║
║  │  • Explicit contracts                                  │   ║
║  │  • ADR process                                         │   ║
║  └────────────────────────────────────────────────────────┘   ║
║                                                               ║
║  ┌────────────────────────────────────────────────────────┐   ║
║  │  project-rules/ (Architecture Patterns)                │   ║
║  │  • 01-architecture.md (Structure)                      │   ║
║  │  • 02-tech-stack.md (Tools & conventions)              │   ║
║  │  • 03-security.md (Auth, authz, multi-tenant)          │   ║
║  │  • 04-naming.md (Conventions)                          │   ║
║  │  • 05-anti-patterns.md (Banned patterns)               │   ║
║  └────────────────────────────────────────────────────────┘   ║
║                                                               ║
║  ┌────────────────────────────────────────────────────────┐   ║
║  │  docs/adr/ (Architectural Decisions)                   │   ║
║  │  • ADR-001: Multi-agent system                         │   ║
║  │  • ADR-002: Auth strategy                              │   ║
║  │  • ADR-003: [Your decisions...]                        │   ║
║  └────────────────────────────────────────────────────────┘   ║
╚═══════════════════════════════════════════════════════════════╝
```

---

## 2. Request Flow

```
┌────────────────────────────────────────────────────────────────┐
│  User Request                                                  │
│  "Create a user profile page with email and password"          │
└────────────────────────────────────────────────────────────────┘
                            ↓
┌────────────────────────────────────────────────────────────────┐
│  brain-agent (Analyze & Slice)                                 │
│                                                                │
│  1. Clarify goal                                               │
│  2. Check ADR needed?                                          │
│  3. Break into slices:                                         │
│     • SLC-001 (XS): UX flow & states                           │
│     • SLC-002 (S): Backend API + validation                    │
│     • SLC-003 (S): UI form + submission                        │
│     • SLC-004 (XS): Integration & E2E test                     │
└────────────────────────────────────────────────────────────────┘
                            ↓
        ┌───────────────────┴───────────────────┐
        ↓                                       ↓
┌───────────────────┐                  ┌───────────────────┐
│  SLC-001          │                  │  SLC-002          │
│  ux-agent         │  ────handoff──>  │  backend-agent    │
│                   │                  │                   │
│  • User flow      │                  │  • API endpoint   │
│  • States         │                  │  • Validation     │
│  • Error messages │                  │  • Error codes    │
│  • A11y spec      │                  │  • DTOs           │
│                   │                  │                   │
│  Integrated: Yes  │                  │  Integrated: Yes  │
└───────────────────┘                  └───────────────────┘
        ↓                                       ↓
        └───────────────────┬───────────────────┘
                            ↓
                  ┌───────────────────┐
                  │  SLC-003          │
                  │  react-agent      │
                  │                   │
                  │  • Form component │
                  │  • Validation UX  │
                  │  • Submit handler │
                  │  • Error display  │
                  │                   │
                  │  Integrated: Yes  │
                  └───────────────────┘
                            ↓
                  ┌───────────────────┐
                  │  SLC-004          │
                  │  test-agent       │
                  │                   │
                  │  • E2E test       │
                  │  • Happy path     │
                  │  • Error cases    │
                  │                   │
                  │  Integrated: Yes  │
                  └───────────────────┘
                            ↓
                  ┌───────────────────┐
                  │  ✅ COMPLETE      │
                  │  Feature shipped  │
                  └───────────────────┘
```

---

## 3. Handoff Flow

```
┌──────────────────────────────────────────────────────────────┐
│  Agent A (Source)                                            │
│                                                              │
│  Completes work on SLC-XXX                                   │
│  ↓                                                           │
│  Creates handoff contract:                                   │
│  • Goal                                                      │
│  • Files changed                                             │
│  • Public contract (API/props/types)                         │
│  • Edge cases                                                │
│  • Test steps                                                │
│  • Integrated: Yes/No                                        │
└──────────────────────────────────────────────────────────────┘
                            ↓
┌──────────────────────────────────────────────────────────────┐
│  brain-agent (Validate)                                      │
│                                                              │
│  Checks:                                                     │
│  ☐ Contract complete?                                        │
│  ☐ Tests provided?                                           │
│  ☐ Integration clear?                                        │
│  ☐ Risks documented?                                         │
│                                                              │
│  If incomplete → request clarification                       │
│  If complete → approve handoff                               │
└──────────────────────────────────────────────────────────────┘
                            ↓
┌──────────────────────────────────────────────────────────────┐
│  Agent B (Target)                                            │
│                                                              │
│  Receives contract                                           │
│  ↓                                                           │
│  Reviews:                                                    │
│  • Public contract (knows what to expect)                    │
│  • Assumptions (validates or challenges)                     │
│  • Edge cases (ensures coverage)                             │
│  ↓                                                           │
│  Implements next slice (SLC-XXX+1)                           │
│  • Uses contract as spec                                     │
│  • Integrates with Agent A's work                            │
│  • Creates own handoff for next agent                        │
└──────────────────────────────────────────────────────────────┘
```

---

## 4. ADR Decision Flow

```
                    ┌─────────────────────┐
                    │  Agent identifies   │
                    │  architectural      │
                    │  decision needed    │
                    └─────────────────────┘
                            ↓
                ┌───────────┴───────────┐
                ↓                       ↓
        ┌───────────────┐       ┌───────────────┐
        │  Informational│       │  Blocking     │
        │  ADR          │       │  ADR          │
        │               │       │               │
        │  • Internal   │       │  • Affects    │
        │  • Low risk   │       │    multiple   │
        │  • Refactor   │       │  • Shared     │
        │               │       │    contracts  │
        │  No approval  │       │  • Security   │
        │  needed       │       │               │
        └───────────────┘       │  Approval     │
                ↓               │  REQUIRED     │
        ┌───────────────┐       └───────────────┘
        │  Document     │               ↓
        │  in ADR       │       ┌───────────────┐
        │               │       │  Agent creates│
        │  Status:      │       │  ADR          │
        │  Accepted     │       │               │
        └───────────────┘       │  Status:      │
                ↓               │  Proposed     │
        ┌───────────────┐       └───────────────┘
        │  Proceed with │               ↓
        │ implementation│       ┌───────────────┐
        └───────────────┘       │  brain-agent  │
                                │  presents to  │
                                │  user         │
                                └───────────────┘
                                        ↓
                            ┌───────────┴───────────┐
                            ↓                       ↓
                    ┌───────────────┐       ┌───────────────┐
                    │  User         │       │  User         │
                    │  approves     │       │  rejects      │
                    └───────────────┘       └───────────────┘
                            ↓                       ↓
                    ┌───────────────┐       ┌───────────────┐
                    │  Status:      │       │  Status:      │
                    │  Accepted     │       │  Rejected     │
                    │               │       │               │
                    │  Proceed with │       │  Find         │
                    │ implementation│       │  alternative  │
                    └───────────────┘       └───────────────┘
```

---

## 5. Agent Routing Decision Tree

```
                    User Request
                         ↓
                    brain-agent
                         ↓
        ┌────────────────┴────────────────┐
        │ What's the primary need?        │
        └────────────────┬────────────────┘
                         ↓
        ┌────────────────┴────────────────┐
        │                                 │
        ↓                                 ↓
┌──────────────┐                  ┌──────────────┐
│ UX unclear?  │ → Yes →          │ Flow/states/ │
│ Screens?     │                  │ content      │
│ States?      │                  │ needed       │
└──────────────┘                  └──────────────┘
        ↓ No                              ↓
┌──────────────┐                  ┌──────────────┐
│ UI component?│ → Yes →          │ ux-agent     │
│ Client state?│                  └──────────────┘
│ Forms?       │
└──────────────┘
        ↓ No
┌──────────────┐
│ Routing?     │ → Yes →
│ SSR/CSR?     │
│ Caching?     │
└──────────────┘
        ↓ No                      ┌──────────────┐
┌──────────────┐                  │ react-agent  │
│ API endpoint?│ → Yes →          └──────────────┘
│ Database?    │
│ Validation?  │
└──────────────┘
        ↓ No                      ┌──────────────┐
┌──────────────┐                  │ next-agent   │
│ Schema       │ → Yes →          └──────────────┘
│ change?      │
│ Migration?   │
└──────────────┘                  ┌──────────────┐
        ↓ No                      │backend-agent │
┌──────────────┐                  └──────────────┘
│ E2E tests?   │ → Yes →
│ Integration? │                  ┌──────────────┐
└──────────────┘                  │ data-agent   │
        ↓ No                      └──────────────┘
┌──────────────┐
│ Define new   │                  ┌──────────────┐
│ specialist   │                  │ test-agent   │
│ agent        │                  └──────────────┘
└──────────────┘
```

---

## 6. File Structure Visualization

```
your-project/
│
├─ .claude/                                  ← Claude-specific config
│  │
│  ├─ CLAUDE.md                              ← Project overview
│  │  • Architecture summary
│  │  • Agent roster
│  │  • Quick reference
│  │
│  ├─ agents/                                ← Agent specifications
│  │  │
│  │  ├─ _shared/
│  │  │  └─ conventions.md                   ← Generic principles
│  │  │     • KISS, SOLID, YAGNI
│  │  │     • Small slices
│  │  │     • ADR process
│  │  │     • Applies to ANY project
│  │  │
│  │  ├─ brain-agent.md                      ← Orchestrator
│  │  │  • Slicing rules
│  │  │  • Agent roster
│  │  │  • Output format
│  │  │  • ADR enforcement
│  │  │
│  │  ├─ ux-agent.md                         ← UX specialist
│  │  ├─ react-agent.md                      ← React specialist
│  │  ├─ next-agent.md                       ← Next.js specialist
│  │  ├─ backend-agent.md                    ← Backend specialist
│  │  └─ [custom-agent].md                   ← Your agents
│  │
│  └─ rules/                                 ← Project architecture
│     ├─ 01-architecture.md                  ← Structure patterns
│     │  • Feature-first / Clean / etc.
│     │  • Folder structure
│     │  • Boundaries
│     │
│     ├─ 02-tech-stack.md                    ← Tech choices
│     │  • Frameworks & versions
│     │  • Libraries & tools
│     │  • Naming conventions
│     │
│     ├─ 03-security.md                      ← Security rules
│     │  • Auth strategy
│     │  • Multi-tenant enforcement
│     │  • Input validation
│     │
│     ├─ 04-naming.md                        ← Conventions
│     │  • Files, functions, variables
│     │  • Project-specific patterns
│     │
│     └─ 05-anti-patterns.md                 ← Banned patterns
│        • What NOT to do
│        • Common mistakes
│
├─ docs/
│  └─ adr/                                   ← Architecture decisions
│     ├─ ADR-000-template.md                 ← Template
│     ├─ ADR-001-multi-agent-system.md       ← System itself
│     ├─ ADR-002-auth-strategy.md            ← Auth approach
│     └─ ADR-XXX-[decision].md               ← Your decisions
│
└─ [your project files]
   • src/
   • tests/
   • etc.
```

---

## 7. Integration Checkpoint Flow

```
    Slice 1 (SLC-001)
    ┌─────────────────┐
    │  ux-agent       │
    │  • Define flow  │
    │  • States       │
    │  • Content      │
    └─────────────────┘
            ↓
    ┌─────────────────┐
    │  Integrated: Yes│ ← UX spec complete
    └─────────────────┘
            ↓
    ────────────────────────
    Slice 2 (SLC-002)
    ┌─────────────────┐
    │  backend-agent  │
    │  • API endpoint │
    │  • Validation   │
    │  • DTOs         │
    └─────────────────┘
            ↓
    ┌─────────────────┐
    │  Integrated: No │ ← API exists but not wired
    │                 │
    │  Missing:       │
    │  • Route not    │
    │    added to     │
    │    Next.js      │
    └─────────────────┘
            ↓
    ────────────────────────
    Slice 3 (SLC-003) ← MUST address missing wiring
    ┌─────────────────┐
    │  next-agent     │
    │  • Add route    │
    │  • Wire to API  │
    │  • SSR setup    │
    └─────────────────┘
            ↓
    ┌─────────────────┐
    │  Integrated: Yes│ ← Now backend is accessible
    └─────────────────┘
            ↓
    ────────────────────────
    Slice 4 (SLC-004)
    ┌─────────────────┐
    │  react-agent    │
    │  • UI component │
    │  • Form         │
    │  • Submit       │
    └─────────────────┘
            ↓
    ┌─────────────────┐
    │  Integrated: Yes│ ← Full feature works end-to-end
    └─────────────────┘
```

---

## 8. Agent Responsibility Matrix

```
┌───────────────┬────────┬────────┬────────┬────────┬────────┬────────┐
│               │  UX    │ React  │ Next   │Backend │ Data   │ Test   │
│  Capability   │ Agent  │ Agent  │ Agent  │ Agent  │ Agent  │ Agent  │
├───────────────┼────────┼────────┼────────┼────────┼────────┼────────┤
│ User Flows    │   ✅   │        │        │        │        │        │
│ Wireframes    │   ✅   │        │        │        │        │        │
│ Content/Copy  │   ✅   │        │        │        │        │        │
│ A11y Spec     │   ✅   │        │        │        │        │        │
├───────────────┼──────--┼────────┼────────┼────────┼────────┼────────┤
│ Components    │        │   ✅   │        │        │        │        │
│ Hooks         │        │   ✅   │        │        │        │        │
│ Client State  │        │   ✅   │        │        │        │        │
│ Forms         │        │   ✅   │        │        │        │        │
├───────────────┼────────┼────────┼────────┼────────┼────────┼────────┤
│ Routing       │        │        │   ✅   │        │        │        │
│ Layouts       │        │        │   ✅   │        │        │        │
│ SSR/CSR       │        │        │   ✅   │        │        │        │
│ Caching       │        │        │   ✅   │        │        │        │
│ Metadata      │        │        │   ✅   │        │        │        │
├───────────────┼────────┼────────┼────────┼────────┼────────┼────────┤
│ API Endpoints │        │        │        │   ✅   │        │        │
│ Business Logic│        │        │        │   ✅   │        │        │
│ Validation    │        │        │        │   ✅   │        │        │
│ Auth/Authz    │        │        │        │   ✅   │        │        │
│ DTOs          │        │        │        │   ✅   │        │        │
├───────────────┼────────┼────────┼────────┼────────┼────────┼────────┤
│ Schema        │        │        │        │        │   ✅   │        │
│ Migrations    │        │        │        │        │   ✅   │        │
│ Indexes       │        │        │        │        │   ✅   │        │
│ Queries       │        │        │        │        │   ✅   │        │
├───────────────┼────────┼────────┼────────┼────────┼────────┼────────┤
│ E2E Tests     │        │        │        │        │        │   ✅   │
│ Integration   │        │        │        │        │        │   ✅   │
│ Unit Tests    │   🔀   │   🔀   │   🔀   │   🔀   │   🔀   │   ✅   │
└───────────────┴────────┴────────┴────────┴────────┴────────┴────────┘

Legend:
  ✅ = Primary owner (responsible for implementation)
  🔀 = Can write unit tests for their own code
```

---

## 9. Slice Sizing Guidelines (Visual)

```
XS Slice (1-2 hours)
├─ Single component
├─ No dependencies
├─ Minimal risk
└─ Example: Add form field
    ┌─────────────────────────┐
    │ ▓▓                      │  Complexity: ■□□□□
    │ ONE component           │  Risk:       ■□□□□
    │ ONE file (maybe 2)      │  Time:       1-2h
    └─────────────────────────┘

─────────────────────────────────

S Slice (0.5-1 day)
├─ Full screen or flow
├─ Some integration
├─ Moderate complexity
└─ Example: Complete form with submission
    ┌─────────────────────────┐
    │ ▓▓▓▓▓▓                  │  Complexity: ■■■□□
    │ 2-3 agents involved     │  Risk:       ■■□□□
    │ Clear boundaries        │  Time:       4-8h
    └─────────────────────────┘

─────────────────────────────────

M Slice (2-3 days) - REQUIRES JUSTIFICATION
├─ Complex coordination
├─ Multiple dependencies
├─ High risk
└─ Example: Multi-step wizard with validation
    ┌─────────────────────────┐
    │ ▓▓▓▓▓▓▓▓▓▓              │  Complexity: ■■■■■
    │ 4+ agents               │  Risk:       ■■■■□
    │ Should be split!        │  Time:       16-24h
    └─────────────────────────┘
    
    ⚠️ If you see M, ask: Can this be split into multiple S slices?
```

---

## 10. Success Metrics Dashboard (Conceptual)

```
┌─────────────────────────────────────────────────────────────┐
│  Multi-Agent System Health Dashboard                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Slice Velocity                                             │
│  ┌───────────────────────────────────────────────────────┐  │
│  │ XS: ████████ 8 slices/week                            │  │
│  │ S:  ████     4 slices/week                            │  │
│  │ M:  █        1 slice/week (⚠️ target:0 )              │  │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Integration Rate                                           │
│  ┌───────────────────────────────────────────────────────┐ │
│  │ Integrated: Yes  ████████████ 90% (✅ Good)           │ │
│  │ Integrated: No   ██           10% (track closely)     │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Agent Utilization                                          │
│  ┌───────────────────────────────────────────────────────┐ │
│  │ brain-agent:   ████████████ (Every request)           │ │
│  │ react-agent:   ████████                               │ │
│  │ backend-agent: ██████                                 │ │
│  │ ux-agent:      ████                                   │ │
│  │ test-agent:    ██                                     │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  ADR Health                                                 │
│  ┌───────────────────────────────────────────────────────┐ │
│  │ Proposed:  █  1 (waiting approval)                    │ │
│  │ Accepted:  ████████ 8 (active)                        │ │
│  │ Superseded: ██ 2 (archived)                           │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Handoff Quality Score                                      │
│  ┌───────────────────────────────────────────────────────┐ │
│  │ Complete contracts:    ████████████ 95% (✅)          │ │
│  │ Missing test steps:    █            5%  (⚠️)          │ │
│  │ Unclear assumptions:   (none)       0%  (✅)          │ │
│  └───────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘

Target KPIs:
  • 80%+ of slices are XS or S
  • 90%+ integration rate
  • All handoffs have complete contracts
  • ADRs resolved within 1 week
```

---

## Usage Guide for These Diagrams

### For Documentation
- Copy diagrams into your project's README or docs
- Use in onboarding materials
- Reference in architecture presentations

### For Team Training
- Walk through request flow diagram with examples
- Use responsibility matrix to clarify ownership
- Review integration checkpoint flow for discipline

### For Debugging
- When integration fails: Check integration flow
- When routing unclear: Review decision tree
- When handoffs incomplete: Reference handoff flow

---

**All diagrams are ASCII-based and can be copied directly into markdown files!**
