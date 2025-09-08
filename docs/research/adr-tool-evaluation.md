# ADR Tool Evaluation: log4brains vs ADG (ad-guidance-tool)

## Executive Summary

After evaluating both **log4brains** and **ADG (Architectural Decision Guidance)**, I recommend **log4brains** for the Laniakea-Edge project. While ADG offers innovative model-based decision management, log4brains provides better alignment with our immediate needs for ADR documentation, web-based visualization, and GitHub Pages integration.

## Detailed Comparison

### 1. log4brains (thomvaill/log4brains)

**Repository**: https://github.com/thomvaill/log4brains

#### Strengths
- **Active Maintenance**: Last commit December 2024, actively maintained
- **Modern Tech Stack**: Built with TypeScript/Node.js, aligns with modern web development
- **Comprehensive Features**:
  - Beautiful web UI with search capabilities
  - Static site generation (perfect for GitHub Pages)
  - Markdown-based with YAML frontmatter
  - Multi-package/monorepo support
  - Integration with Next.js/React
  - Live preview during editing
  - Graph visualization of decision relationships
  - Full-text search across all ADRs
- **Developer Experience**:
  - CLI commands similar to adr-tools
  - Hot reload in development mode
  - Automatic table of contents generation
  - Badge generation for README files
- **Community**: 1,292 stars, growing adoption
- **Documentation**: Excellent documentation with examples and templates

#### Weaknesses
- Requires Node.js runtime (not an issue for our stack)
- Slightly more complex setup than shell scripts
- Newer project (less battle-tested)

#### Installation & Usage
```bash
npm install -g log4brains
log4brains init
log4brains adr new "Use log4brains for ADR management"
log4brains serve  # Local preview
log4brains build  # Static site generation
```

### 2. ADG - Architectural Decision Guidance (adr/ad-guidance-tool)

**Repository**: https://github.com/adr/ad-guidance-tool

#### Strengths
- **Innovative Approach**: Model-based decision management with reusable patterns
- **Go-Based**: Fast, single binary, no runtime dependencies
- **Advanced Features**:
  - Decision models and templates
  - Decision linking and relationships
  - Copy/merge/import models for reuse
  - Tag-based categorization
  - Decision status tracking (open/decided)
  - Comment system for decisions
  - Clean Architecture patterns included
- **Academic Foundation**: Developed as part of university research projects
- **Cross-Platform**: Precompiled binaries for all major OS

#### Weaknesses
- **Brand New**: First commit June 2024, very recent project
- **Limited Adoption**: Only 7 stars, minimal community
- **No Web UI**: CLI-only, no visualization or search interface
- **Complex for Simple Use**: Model-based approach may be overkill for basic ADRs
- **No Static Site Generation**: Cannot generate documentation websites
- **Learning Curve**: Unique concepts (models, linking) require team training

#### Installation & Usage
```bash
# Download binary or build from source
go build
./adg init my-model
./adg add --model my-model --title "Decision title"
./adg decide --model my-model --id 0001 --option 1
```

## Evaluation Criteria Analysis

| Criteria | log4brains | ADG | Winner |
|----------|------------|-----|---------|
| **Maintenance Status** | Actively maintained (Dec 2024) | New project (June 2024) | ✅ log4brains |
| **Feature Set** | Web UI, search, visualization | Model-based, linking, tagging | ✅ log4brains |
| **Developer Experience** | Excellent (hot reload, preview) | Good (CLI autocomplete) | ✅ log4brains |
| **Documentation Quality** | Extensive with examples | Good academic foundation | ✅ log4brains |
| **Community Support** | Growing (1.3k stars) | Minimal (7 stars) | ✅ log4brains |
| **Integration** | GitHub Pages, CI/CD ready | CLI-only, no web output | ✅ log4brains |
| **Learning Curve** | Moderate | Steep (new concepts) | ✅ log4brains |
| **Dependencies** | Node.js required | Go binary (standalone) | ✅ ADG |
| **Innovation** | Standard ADR approach | Novel model-based approach | ✅ ADG |

## Recommendation for Laniakea-Edge

### 🏆 Recommended: log4brains

**Rationale:**

1. **Alignment with Project Goals**:
   - Laniakea-Edge is an AI-powered quality engine that values comprehensive documentation
   - The web UI and search capabilities align with our focus on accessibility and discoverability
   - Static site generation enables easy integration with GitHub Pages for public documentation

2. **Technical Fit**:
   - TypeScript/Node.js aligns with modern web development practices
   - API-first approach of Laniakea-Edge benefits from log4brains' structured data format
   - The visualization features help communicate complex architectural relationships
   - Web-based documentation fits our focus on transparency and community engagement

3. **Practical Considerations**:
   - Active maintenance ensures compatibility with future tooling
   - Established community provides support and examples
   - Standard ADR format is widely understood and accepted
   - GitHub Pages integration allows automatic documentation deployment

4. **Team Benefits**:
   - Web UI lowers barrier for non-technical stakeholders
   - Search functionality crucial as ADR count grows
   - Relationship visualization helps understand decision impacts
   - Live preview speeds up the writing process

### Why Not ADG?

While ADG offers innovative features like decision models and reusable patterns, it's not the right fit for Laniakea-Edge because:

- **Too New**: With only 7 stars and first commit in June 2024, it lacks community validation
- **No Web Output**: CLI-only approach doesn't meet our need for accessible, searchable documentation
- **Overengineered for Our Needs**: Model-based approach is powerful but adds unnecessary complexity for standard ADR management
- **Missing Critical Features**: No static site generation, no web UI, no search functionality

## Migration Path

If we choose log4brains, here's the implementation plan:

1. **Install and Initialize**:
   ```bash
   npm install -g log4brains
   cd /path/to/laniakea-edge
   log4brains init
   ```

2. **Migrate Existing ADRs**:
   - Move existing ADRs to log4brains format
   - Add YAML frontmatter to existing files
   - Update numbering scheme if needed

3. **Configure CI/CD**:
   - Add GitHub Action to build and deploy to GitHub Pages
   - Configure automatic badge generation

4. **Team Training**:
   - Quick tutorial on log4brains commands
   - Document workflow in CONTRIBUTING.md

## Conclusion

Between log4brains and ADG, **log4brains is the clear choice** for Laniakea-Edge. While ADG represents interesting innovation in the ADR space with its model-based approach, it's too new and lacks the essential features we need: web UI, search functionality, and static site generation.

log4brains provides:
- Proven, actively maintained solution
- Perfect alignment with our GitHub Pages documentation strategy
- Superior developer experience with live preview and hot reload
- Community support and extensive documentation

The additional complexity of log4brains over simpler tools is minimal and far outweighed by its benefits, especially the web UI, search capabilities, and visualization features that will be crucial as our ADR collection grows.

## Next Steps

1. Install log4brains globally
2. Initialize in the Laniakea-Edge repository
3. Migrate existing ADRs (currently 2 ADRs)
4. Set up GitHub Pages deployment
5. Update documentation workflow

---

*Evaluation Date: January 2025*  
*Evaluator: Development Team*  
*Decision Status: Pending Approval*