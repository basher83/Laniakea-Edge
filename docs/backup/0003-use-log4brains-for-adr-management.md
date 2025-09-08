# Use log4brains for ADR Management

- Status: accepted
- Date: 2025-01-07
- Deciders: Development Team
- Tags: tooling, documentation, meta

## Context and Problem Statement

The Laniakea-Edge project needs a robust tool for managing Architecture Decision Records (ADRs) that supports our goals of transparency, accessibility, and comprehensive documentation. How can we best manage ADRs to ensure they are discoverable, maintainable, and accessible to all stakeholders while integrating with our GitHub-based workflow?

We initially attempted to use `adr-log` but encountered Node.js v24 compatibility issues (TypeError: date.getFullYear is not a function), revealing the tool is unmaintained and incompatible with modern development environments.

## Decision Drivers

- Need for web-based documentation accessible to non-technical stakeholders
- Requirement for search functionality across all ADRs
- Integration with GitHub Pages for public documentation
- Active maintenance to ensure compatibility with modern tooling
- Developer experience with live preview and efficient workflows
- Ability to visualize relationships between decisions
- Standard format compatibility (MADR)

## Considered Options

- log4brains (thomvaill/log4brains)
- adr-log (unmaintained)
- adr-tools (npryce/adr-tools - deprecated)
- ADG - Architectural Decision Guidance (adr/ad-guidance-tool)
- Manual ADR management

## Decision Outcome

Chosen option: **log4brains**, because it provides the best combination of features, active maintenance, and alignment with our project goals. It offers a web UI with search and visualization capabilities that are essential for our documentation strategy, while maintaining compatibility with standard MADR format.

### Consequences

- Good, because we get a beautiful web UI with full-text search capabilities
- Good, because static site generation integrates perfectly with GitHub Pages
- Good, because active maintenance (last update Dec 2024) ensures long-term viability
- Good, because visualization features help understand decision relationships
- Good, because live preview with hot reload improves developer productivity
- Bad, because it requires Node.js runtime (though this aligns with modern web development)
- Bad, because it's slightly more complex than simple shell scripts
- Bad, because we need to add YAML frontmatter to existing ADRs (minimal effort for 2 files)

### Confirmation

Implementation success will be confirmed by:
- Successfully migrating existing ADRs to log4brains format
- Publishing ADR documentation to GitHub Pages
- Team successfully creating new ADRs using log4brains CLI
- Search functionality working across all ADRs

## Pros and Cons of the Options

### log4brains

TypeScript/Node.js tool with web UI, search, and static site generation. 1,292 stars on GitHub.

- Good, because it has an active community and maintenance
- Good, because web UI makes ADRs accessible to all stakeholders
- Good, because it integrates with GitHub Pages for automatic deployment
- Good, because search and visualization features aid navigation
- Neutral, because it requires Node.js (common in modern development)
- Bad, because it adds build complexity compared to plain markdown

### adr-log

Node.js-based ADR tool that we initially tried to use.

- Good, because it seemed to offer web interface capabilities
- Bad, because it's incompatible with Node.js v24 (fails with TypeError)
- Bad, because it appears to be unmaintained
- Bad, because it has unresolved dependency issues

### adr-tools (deprecated)

Original bash-based ADR tools with 5,049 stars.

- Good, because it's simple and well-established
- Good, because it requires only bash
- Bad, because it's explicitly deprecated by maintainers
- Bad, because maintainers recommend log4brains instead
- Bad, because it lacks web UI, search, and visualization
- Bad, because last meaningful update was in 2018

### ADG (ad-guidance-tool)

Go-based tool with innovative model-based decision management.

- Good, because it offers innovative model-based approach
- Good, because it's a standalone Go binary
- Bad, because it's too new (June 2024) with only 7 stars
- Bad, because it lacks web UI and static site generation
- Bad, because model-based approach adds unnecessary complexity
- Bad, because it doesn't meet our documentation publishing needs

### Manual Management

Continue without tooling support.

- Good, because it has zero dependencies
- Bad, because it lacks search capabilities
- Bad, because it provides no visualization of relationships
- Bad, because it offers no web publishing
- Bad, because it requires manual template management

## More Information

See the detailed [ADR Tool Evaluation](../research/adr-tool-evaluation.md) for comprehensive analysis of each option.

Implementation will follow these steps:
1. Install log4brains globally via npm
2. Initialize log4brains in the repository
3. Migrate existing ADRs by adding YAML frontmatter
4. Configure GitHub Actions for automatic deployment
5. Update documentation with new ADR workflow
6. Provide team training on log4brains usage

This decision directly supports our project's emphasis on transparency and comprehensive documentation, making architectural decisions easily accessible to all stakeholders through a searchable web interface.