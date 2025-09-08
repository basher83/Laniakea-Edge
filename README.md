# Laniakea-Edge

**The AI-powered quality engine for Infrastructure-as-Code, beginning with deep analysis for the Ansible ecosystem.**

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Planning-yellow.svg)](docs/planning/)
[![Phase](https://img.shields.io/badge/Phase-0_Architecture-orange.svg)](docs/planning/roadmap.md)

## Project Status

**Current Phase**: Planning & Architecture (Phase 0)
- ✅ Research completed
- 🔄 Architecture decisions in progress  
- 📋 POC planned for validation
- ⏳ No implementation code yet

See [Planning Documents](docs/planning/) for current progress and [Decision Matrix](docs/planning/decisions-matrix.md) for pending architectural decisions.

## Vision

Building a comprehensive quality assessment platform for the entire Infrastructure-as-Code (IaC) landscape, enabling developers and organizations to discover and evaluate high-quality code repositories with confidence.

## Solution Overview

Laniakea-Edge will be a specialized AI research assistant designed to solve the critical "signal vs. noise" problem in IaC ecosystems. Designed as an API-first microservice using the Model Context Protocol, it will serve as an intelligent tool that AI agents, CI/CD pipelines, and development teams can utilize for comprehensive repository analysis.

### Core Capabilities

- **Automated Repository Discovery**: Intelligent GitHub search and filtering across IaC ecosystems
- **Multi-Faceted Quality Scoring**: Comprehensive evaluation based on testing frameworks, maintenance activity, documentation standards, and community health
- **AI-Powered Analysis**: Advanced reasoning and synthesis for actionable insights
- **Extensible Architecture**: Pluggable analyzer system supporting multiple IaC technologies

## Current Focus: Ansible Ecosystem

The initial release delivers the most comprehensive quality analysis available for the Ansible ecosystem, evaluating repositories based on:

- **Testing Frameworks**: Molecule and ansible-lint integration
- **Maintenance Activity**: Commit frequency and active contributor engagement
- **Documentation Quality**: README completeness and usage examples
- **Community Health**: Issue resolution times and collaborative development patterns

## Architecture: AI Tool/Plugin Model

### Microservices Design

Laniakea-Edge follows a modern microservices architecture with specialized components:

#### Core Services

- **GitHub Discovery Service**: Expert repository search and filtering
- **Ansible Analyzer Service**: Domain-specific quality assessment
- **Orchestrator/API Gateway**: Request coordination and result synthesis

#### Model Context Protocol

The service implements a comprehensive API contract enabling seamless integration with:

- Custom GPTs and AI assistants
- LangChain-powered applications
- CI/CD pipelines and automation workflows
- Development tools and IDE integrations

## Technology Stack (Under Evaluation)

### Pending Decisions

The following technologies are being evaluated and will be finalized through Architecture Decision Records (ADRs):

| Technology | Options | Status | Decision Target |
|------------|---------|--------|-----------------|
| **Language** | Python 3.11, 3.12 | 📋 Pending ADR | Week 1 |
| **API Framework** | FastAPI, Flask, Django REST | 🔄 Evaluating | Week 2 |
| **AI Integration** | LangChain, LlamaIndex, Custom | 📋 Pending ADR | Week 2 |
| **GitHub Client** | PyGithub, GitHub GraphQL | 📋 Not Started | Week 3 |

### Confirmed Technologies

- **Version Control**: GitHub
- **Container**: Docker
- **Documentation**: Markdown with ADRs

See [Technology Stack Reference](docs/reference/tech-stack.md) for detailed evaluation criteria and [Decision Matrix](docs/planning/decisions-matrix.md) for decision status.

## Development Roadmap

### Phase 0: Planning & Architecture (Current - Weeks 1-4)

- ✅ Research and problem analysis
- 🔄 Architecture decision documentation
- 📋 Proof of concept planning
- 📋 Development environment setup

### Phase 1: Foundation Implementation (Weeks 5-8)

- Core orchestration service
- GitHub discovery service
- Basic API gateway
- Initial Ansible analyzer

### Phase 2: MVP Development (Weeks 9-12)

- Quality scoring algorithms
- Model Context Protocol integration
- Comprehensive testing suite
- Performance optimization

### Phase 3: Production Readiness (Weeks 13-16)

- Caching layer implementation
- Monitoring and observability
- Security hardening
- Beta release preparation

See [Full Roadmap](docs/planning/roadmap.md) for detailed timeline and milestones.

## Planned Usage

*Note: This project is currently in the planning phase. The following represents the intended design and API.*

### Future Installation

```bash
# Planned installation method (not yet available)
pip install laniakea-edge
```

### Planned API Design

#### Repository Analysis Endpoint
```http
POST /v1/analyze
Content-Type: application/json

{
  "repository_url": "https://github.com/example/ansible-role",
  "technology": "ansible"
}
```

#### Expected Response Format
```json
{
  "repository": "example/ansible-role",
  "overall_score": 8.5,
  "metrics": {
    "testing": 9.0,
    "documentation": 8.0,
    "maintenance": 9.5,
    "community": 7.0
  },
  "recommendations": [
    "Add Molecule tests for better validation",
    "Include more usage examples in README"
  ]
}
```

### Planned Model Context Protocol Integration

The service will implement MCP for AI agent integration:

```python
# Planned integration example
{
  "tool": "analyze_repository",
  "parameters": {
    "repository_url": "https://github.com/ansible/ansible",
    "technology": "ansible"
  }
}
```

See [API Design Documentation](docs/architecture/api-design.md) for complete specifications.

## Documentation

The project documentation is organized into five main sections:

### 📚 [Research Phase](docs/research/)
- Problem analysis and validation
- Market and competitive analysis  
- Technical architecture research

### 📋 [Planning & Tracking](docs/planning/)
- **[Decision Matrix](docs/planning/decisions-matrix.md)** - Architectural decisions tracking
- **[Risk Register](docs/planning/risk-register.md)** - Risk identification and mitigation
- **[POC Plan](docs/planning/poc-plan.md)** - Proof of concept strategy
- **[Requirements](docs/planning/requirements.md)** - Functional and non-functional requirements

### 🏗️ [Architecture Design](docs/architecture/)
- **[System Design](docs/architecture/system-design.md)** - High-level architecture
- **[API Specification](docs/architecture/api-design.md)** - API contracts and MCP integration
- **[Quality Framework](docs/architecture/quality-framework.md)** - Scoring methodology

### 📝 [Architecture Decisions](docs/decisions/)
- ADR template and lifecycle folders
- Pending and accepted decisions

### 📖 [Quick Reference](docs/reference/)
- **[Technology Stack](docs/reference/tech-stack.md)** - Technology evaluation status
- **[Pre-Implementation Checklist](docs/reference/checklist.md)** - Readiness assessment
- **[Glossary](docs/reference/glossary.md)** - Terms and definitions

## Getting Started

### For Contributors

1. **Understand the Project**: Start with [Research Documentation](docs/research/)
2. **Review Current Status**: Check [Planning Documents](docs/planning/)
3. **Architecture Decisions**: Monitor [Decision Matrix](docs/planning/decisions-matrix.md)
4. **POC Participation**: See [POC Plan](docs/planning/poc-plan.md)

### Next Steps

- **Week 1**: Python version decision, POC setup
- **Week 2**: Core technology ADRs (API, AI frameworks)
- **Week 3-4**: POC implementation and validation

## Contributing

We welcome contributions! As the project is in planning phase, you can help by:

- Reviewing and providing feedback on architectural decisions
- Participating in POC development
- Contributing to documentation improvements
- Suggesting evaluation criteria for technology choices

See [Contributing Guide](CONTRIBUTING.md) (coming soon) for details.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

- **Documentation**: [docs/](docs/)
- **Planning Status**: [docs/planning/](docs/planning/)
- **Issues**: [GitHub Issues](https://github.com/your-org/laniakea-edge/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-org/laniakea-edge/discussions)

---

**Laniakea-Edge**: Transforming Infrastructure-as-Code discovery through intelligent, automated quality assessment.
