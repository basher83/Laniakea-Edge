# Laniakea-Edge Project Assistant Guide

## Project Context

Laniakea-Edge is an AI-powered quality engine for Infrastructure-as-Code, currently in the **research and planning phase**. The project aims to solve the "signal vs. noise" problem in IaC ecosystems through comprehensive repository analysis and quality scoring.

## Current Phase: Planning & Architecture

We are in the **pre-implementation phase** focusing on:

1. Documenting architectural decisions (ADRs)
2. Evaluating technology choices
3. Defining quality metrics and scoring algorithms
4. Planning the microservices architecture

## Project Structure

```text
Laniakea-Edge/
├── docs/
│   ├── ADR/                 # Architecture Decision Records
│   │   └── ADR-TEMPLATE.md  # Template for new ADRs
│   ├── research/            # Research documentation
│   │   ├── decisions.md     # Decision matrix (KEY DOCUMENT)
│   │   ├── signal-noise.md  # Problem analysis
│   │   ├── architecture.md  # Technical architecture
│   │   ├── framework.md     # Pluggable analyzer design
│   │   ├── solutions.md     # Technology evaluation
│   │   ├── success-blueprint.md # Development strategy
│   │   └── summary.md       # Strategic positioning
│   └── README.md           # Documentation overview
└── README.md               # Project overview
```

## Key Documents for Planning Phase

1. **docs/research/decisions.md** - The decision matrix tracking all architectural decisions needed
2. **docs/ADR/ADR-TEMPLATE.md** - Template for documenting decisions
3. **docs/research/architecture.md** - AI tool/plugin model design
4. **docs/research/signal-noise.md** - Core problem and quality metrics

## Decision-Making Process

When evaluating architectural decisions:

1. **Review the decision matrix** in `docs/research/decisions.md`
2. **Check evaluation criteria** for the specific decision category
3. **Research options** using the documented constraints and success metrics
4. **Create an ADR** using the template when ready to document a decision
5. **Update the status table** in decisions.md

## Priority Decisions (Phase 1 - Blocking)

These decisions must be made before any implementation:

1. **API Framework Selection** (FastAPI vs Flask vs Django REST)
   - Target: <100ms p95 latency, OpenAPI generation required
2. **AI Agent Framework** (LangChain vs LlamaIndex vs Custom)

   - Target: <5s response time, GitHub API integration

3. **Python Version** (3.9 vs 3.10 vs 3.11 vs 3.12)

   - Consider library compatibility and LTS support

4. **Service Architecture** (Microservices vs Modular Monolith)
   - Target: <10ms inter-service latency

## Research Focus Areas

### Quality Metrics Framework

- Review `docs/research/signal-noise.md` for metric definitions
- Consider: Testing coverage, maintenance activity, documentation quality, community health

### Architecture Patterns

- Model Context Protocol implementation (see `docs/research/architecture.md`)
- Microservices boundaries and communication
- Pluggable analyzer system for multi-IaC support

### Technology Stack

- GitHub API integration patterns
- Repository analysis strategies
- Caching and rate limiting approaches

## ADR Creation Guidelines

When creating a new ADR:

```markdown
# ADR-YYYY-MM-DD: [Decision Title]

## Status

Proposed

## Context

[Problem requiring decision]

## Decision

[What we're doing and why]

## Consequences

### Positive

- [Benefits]

### Negative

- [Drawbacks]

### Risks

- [Uncertainties]

## Alternatives Considered

[Options evaluated and why rejected]

## Implementation

[Key steps to implement]
```

## Planning Phase Deliverables

Before moving to implementation, we need:

1. ✅ Research documentation (COMPLETE)
2. 🔄 Phase 1 ADRs (IN PROGRESS)
   - [ ] API Framework Selection ADR
   - [ ] AI Framework Selection ADR
   - [ ] Python Version ADR
   - [ ] Service Architecture ADR
3. ⏳ Development environment setup
4. ⏳ Initial project structure
5. ⏳ CI/CD pipeline configuration

## Communication Style

When discussing the project:

- Focus on **architectural decisions** rather than implementation details
- Reference **research documents** to support recommendations
- Use **evaluation criteria** from decisions.md when comparing options
- Highlight **dependencies** between decisions
- Track progress using the **decision status table**

## Next Steps

1. Review and prioritize Phase 1 decisions in `docs/research/decisions.md`
2. Begin evaluation of API frameworks against defined criteria
3. Document findings in ADRs as decisions are made
4. Update decision tracking table with progress

## Important Notes

- **No implementation code exists yet** - we're in planning phase
- All code examples should be **conceptual** or **pseudo-code**
- Focus on **architecture and design** decisions
- Reference research docs for context and rationale
- The goal is to establish a solid foundation before coding begins

## Questions to Consider

When reviewing any decision:

1. Does it align with the project vision in README.md?
2. Are the evaluation criteria comprehensive?
3. What are the long-term implications?
4. How does it affect other pending decisions?
5. Can we validate this choice with a proof of concept?

---

_This guide will evolve as the project moves from planning to implementation phase._
