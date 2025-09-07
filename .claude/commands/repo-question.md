---
allowed-tools: Bash(git ls-files:*), Read
description: Answer questions about the Laniakea-Edge project structure and documentation
argument-hint: [Repo question]
---

# Laniakea-Edge Repository Question Handler

Answer questions about the **Laniakea-Edge** project by analyzing its structure and documentation. This AI-powered research assistant solves the "signal vs. noise" problem in Infrastructure-as-Code ecosystems.

## Project Context

**Laniakea-Edge** is currently in the **planning and research phase**. The project focuses on:

- AI-powered quality analysis of IaC repositories
- Model Context Protocol for AI agent integration
- Multi-technology support (Ansible, Terraform, Kubernetes)
- Microservices architecture with API-first design

## Instructions

- **IMPORTANT: This is a question-answering task only - DO NOT write, edit, or create any files**
- **IMPORTANT: Focus on understanding and explaining existing research and documentation**
- **IMPORTANT: Provide clear, informative answers based on project analysis**
- **IMPORTANT: If the question requires code changes, explain what would need to be done conceptually without implementing**
- **IMPORTANT: Note that this is a planning-phase project with no implementation code yet**

## Execute

- `git ls-files` to understand the current project structure
- Focus on documentation and research files in planning phase

## Tool Integration Strategy

- **Initial Analysis**: Start with `git ls-files docs/` and `git ls-files docs/research/` to establish documentation baseline
- **Targeted Reading**: Use question classification to determine which research docs to read first
- **Verification**: Cross-reference findings against docs/README.md and research documentation
- **Planning Phase Context**: Emphasize that this is research/planning phase with ADRs pending

## Read

- @README.md for project overview and vision
- @docs/README.md for documentation structure
- @docs/research/decisions.md for pending architectural decisions
- @docs/ADR/ADR-TEMPLATE.md for ADR format reference

## Analysis Approach

1. **Documentation Mapping**: Cross-reference question against actual docs/ and docs/research/ structure
2. **Context-Aware Reading**: Selectively read relevant documentation based on question type:
   - Research questions → docs/research/ directory
   - Architecture questions → docs/research/architecture.md, framework.md
   - Decision questions → docs/research/decisions.md
   - Quality metrics → docs/research/signal-noise.md
   - Technology choices → docs/research/solutions.md
3. **ADR Awareness**: Note that architectural decisions are pending ADR documentation
4. **Planning Phase**: Emphasize research findings and pending implementation decisions
5. **Vision Alignment**: Reference strategic positioning from docs/research/summary.md

## Question Classification & Documentation Routing

**Research & Problem Analysis:**

- Primary: docs/research/signal-noise.md
- Secondary: docs/research/solutions.md
- Context: README.md project vision

**Architecture & Design:**

- Primary: docs/research/architecture.md, framework.md
- Secondary: docs/research/decisions.md (pending decisions)
- Future: ADR/ directory (when decisions are documented)

**Technology & Implementation:**

- Primary: docs/research/solutions.md, architecture.md
- Secondary: docs/research/decisions.md (framework choices pending)
- Context: Planning phase - no implementation code yet

**Quality & Metrics:**

- Primary: docs/research/signal-noise.md
- Secondary: docs/research/framework.md (analyzer plugins)
- Context: Multi-faceted scoring approach defined in research

**Strategic & Planning:**

- Primary: docs/research/summary.md (vision + proof point)
- Secondary: docs/research/success-blueprint.md (development strategy)
- Context: docs/research/decisions.md (decision matrix)

## Documentation Quality Assurance

- **Verify Completeness**: Cross-check findings against docs/README.md and docs/research/ structure
- **ADR Awareness**: Note that many architectural decisions are still pending ADR documentation
- **Research Alignment**: Ensure answers align with research findings and strategic positioning
- **Planning Phase Context**: Emphasize that this is research/planning phase with no implementation yet

## When Documentation is Incomplete

- Flag gaps in research or decision documentation
- Suggest creating ADRs for pending architectural decisions
- Reference most closely related existing research documentation
- Note current planning phase status and pending implementation decisions

## Planning Phase Considerations

- **Research Focus**: Emphasize that answers are based on research and planning documents
- **Decision Status**: Highlight which decisions are made vs. pending ADR documentation
- **Implementation Timeline**: Note that implementation code doesn't exist yet
- **Future State**: Reference roadmap and development phases from success-blueprint.md

## Response Structure

1. **Direct Answer** (2-3 sentences with planning phase context)
2. **Supporting Evidence** (cite specific research docs and current status)
3. **Documentation References** (with relative paths to research/docs)
4. **Decision Status** (note if ADR documentation is pending)
5. **Next Steps** (reference decision matrix or ADR creation if needed)

## Project Phase Awareness

**Current Status**: Research and planning phase

- ✅ Research completed and documented
- 🔄 Architectural decisions pending ADR documentation
- ⏳ Implementation phase awaiting decisions
- 📋 Decision matrix established in docs/research/decisions.md

## Question

$ARGUMENTS
