# log4brains Migration Guide

## Current Structure Analysis

### What We Have
```
docs/decisions/
├── .markdownlint.yml
├── 0000-use-markdown-architectural-decision-records.md
├── 0002-do-not-use-numbers-in-headings.md
├── 0003-use-log4brains-for-adr-management.md
├── index.md
├── README.md
└── template.md
```

### What log4brains Expects

Based on analysis of the log4brains repository, here's what the tool expects:

1. **Directory Structure**: 
   - ADRs can be in any directory (configurable via `.log4brains.yml`)
   - Default is `docs/adr/` but we can keep `docs/decisions/`
   - Flat structure with all ADRs in one directory (no subdirectories)

2. **File Naming**:
   - Pattern: `YYYYMMDD-descriptive-name.md` (e.g., `20200927-avoid-default-exports.md`)
   - OR: `NNNN-descriptive-name.md` (e.g., `0001-use-markdown.md`)
   - Our current naming (`0000-use-markdown...`) is compatible

3. **File Format**:
   - Markdown files with specific frontmatter
   - Uses a simplified frontmatter compared to MADR

4. **Required Files**:
   - `README.md` - Overview of ADRs (we have this)
   - `index.md` - Entry point for log4brains (we have this)
   - `template.md` - Template for new ADRs (we have this, but need to update)

## Changes Needed for Our ADRs

### 1. Update Frontmatter Format

**Current MADR format** (in our ADRs):
```yaml
---
status: accepted
date: 2025-01-07
decision-makers: Development Team
consulted: Project stakeholders
informed: All contributors
---
```

**log4brains format** (simpler):
```markdown
- Status: accepted
- Date: 2025-01-07
- Deciders: Development Team
- Tags: meta, tooling
```

Note: log4brains uses bullet points, not YAML frontmatter!

### 2. Files to Update

1. **Keep As-Is**:
   - Directory location (`docs/decisions/`)
   - File names (already follow NNNN- pattern)
   - README.md (already compatible)

2. **Update Frontmatter**:
   - `0000-use-markdown-architectural-decision-records.md`
   - `0002-do-not-use-numbers-in-headings.md`
   - `0003-use-log4brains-for-adr-management.md`

3. **Replace Template**:
   - Current `template.md` uses MADR format
   - Need to use log4brains template format

4. **Optional Changes**:
   - Could rename files to YYYYMMDD format but not required
   - Could move to `docs/adr/` but not required

## Configuration File

Create `.log4brains.yml` in project root:
```yaml
project:
  name: Laniakea-Edge
  tz: America/New_York  # Adjust to your timezone
  adrFolder: ./docs/decisions
```

## Migration Steps

### Phase 1: Backup (Already discussed)
```bash
# Create backup before any changes
tar -czf decisions-backup-$(date +%Y%m%d-%H%M%S).tar.gz docs/decisions/
```

### Phase 2: Update Existing ADRs
1. Convert YAML frontmatter to log4brains format
2. Ensure content structure matches expected format

### Phase 3: Initialize log4brains
```bash
# Install globally
npm install -g log4brains

# Initialize (will create .log4brains.yml)
log4brains init

# When prompted:
# - ADR folder: ./docs/decisions
# - Project name: Laniakea-Edge
```

### Phase 4: Verify
```bash
# Start dev server to verify
log4brains serve

# Check that all ADRs appear correctly
```

## Important Notes

1. **No Destructive Changes**: log4brains init will:
   - Create `.log4brains.yml` config file
   - Add some npm scripts to package.json (if it exists)
   - NOT overwrite existing ADRs
   - NOT change directory structure

2. **Gradual Migration**: We can:
   - Keep existing ADRs and update them gradually
   - New ADRs will use log4brains format automatically

3. **Compatibility**: Our current structure is mostly compatible:
   - File naming convention works
   - Directory can stay as `docs/decisions/`
   - Only frontmatter needs updating

## Decision Point

Before proceeding, we need to decide:

1. **Keep `docs/decisions/` or move to `docs/adr/`?**
   - Recommendation: Keep `docs/decisions/` to maintain git history

2. **Update frontmatter format now or gradually?**
   - Recommendation: Update all 3 existing ADRs now for consistency

3. **Rename files to YYYYMMDD format?**
   - Recommendation: Keep current NNNN- format, it's already compatible

4. **When to initialize log4brains?**
   - Recommendation: After updating frontmatter in existing ADRs