# Regen AI Forum Content Repository

Knowledge archive and content production system for the [Regen AI initiative](https://forum.regen.network) - a collaboration between Gaia AI and Regen Network to build planetary intelligence infrastructure.

## Repository Structure

```
/docs/          - Documentation archive (read-only, historical)
  /github/      - Technical specs from GitHub
  /koi/         - Roadmaps and architecture docs
  /paragraph/   - Published blog posts
  /transcripts/ - Community call transcripts
  /other/       - Interviews and miscellaneous

/content/       - Active content production
  *-strategy.md - Content strategies and calendars
  *-*.md        - Draft forum posts and articles

/.claude/       - Claude Code configuration
  /commands/    - Custom slash commands
```

## Quick Start

### 1. Load Documentation Context

Before creating new content, load the full knowledge base:

```bash
/prime:2025-11-17
```

This reads all core documentation and establishes comprehensive context about:
- Regen AI technical architecture (KOI, Ledger, and Registry Review MCPs)
- Strategic roadmap and development phases
- Community programs and partnerships
- Historical context and evolution

### 2. Review Existing Strategy

Check the content strategy for guidance:

```bash
cat content/2025-11-17-strategy.md
```

This contains:
- 12-week content calendar with themes and deadlines
- Standard post structure template
- Engagement tactics and best practices
- Author rotation and sustainability guidelines

### 3. Review Previous Posts

Look at existing posts for format and style:

```bash
cat content/2025-11-17-foundation.md
```

This Week 1 post demonstrates:
- Title format: `[Week X/12] Regen AI Update: [Theme] - [Date]`
- Metadata header structure
- Content organization and flow
- Discussion question patterns
- Discourse markdown formatting

## Creating Forum Posts

### Weekly Update Process

1. **Check the calendar** in `content/2025-11-17-strategy.md`
   - Find your week number and theme
   - Review the assigned focus areas
   - Note the engagement question

2. **Load context** with `/prime:2025-11-17`

3. **Create the post** following the template:

```markdown
# [Week X/12] Regen AI Update: [Theme] - [Date]

**Posted by:** [Your Name]
**Key Focus:** [1-2 sentence summary]

---

## [Main Content Sections]

[500-800 words of content]

---

## Discussion Question

**[Specific question for community]**

More specifically:
* [Sub-question 1]
* [Sub-question 2]

---

## Looking Ahead: Week X+1 Preview

[Preview next week's topic]

---

*This is the [ordinal] of 12 weekly updates...*
```

4. **Save to content directory**:
   ```bash
   # Format: content/YYYY-MM-DD-topic.md
   # Example:
   vim content/2025-12-02-koi-deep-dive.md
   ```

5. **Commit and push**:
   ```bash
   git add content/2025-12-02-koi-deep-dive.md
   git commit -m "Add Week 2 forum post: KOI MCP Deep Dive"
   git push origin main
   ```

### Discourse Markdown Notes

Forum posts use Discourse markdown (different from GitHub):

- **Images**: `![alt text|WIDTHxHEIGHT](upload://HASH.ext)`
- **Lists**: Use `*` not `-`
- **Headings**: Use `##` for sections (no single `#` except title)
- **Bold**: `**text**` works the same
- **Links**: `[text](url)` works the same

## Adding Documentation

### New Documentation Workflow

1. **Determine the source category**:
   - `/github/` - Technical specs, implementation docs
   - `/koi/` - Roadmaps, strategy, architecture
   - `/paragraph/` - Published blog posts
   - `/transcripts/` - Meeting notes, community calls
   - `/other/` - Everything else

2. **Name the file with date prefix**:
   ```
   YYYY-MM-DD-descriptive-title.md
   ```

3. **Add to the appropriate directory**:
   ```bash
   # Example: Adding a new community call transcript
   vim docs/transcripts/2025-12-05-regen-network-community-call.md
   ```

4. **Update prime command** (if should be part of standard context):
   ```bash
   vim .claude/commands/prime/2025-11-17.md
   ```

   Add to the READ section:
   ```markdown
   @docs/transcripts/2025-12-05-regen-network-community-call.md
   ```

5. **Commit the documentation**:
   ```bash
   git add docs/transcripts/2025-12-05-regen-network-community-call.md
   git commit -m "Add December community call transcript"
   git push origin main
   ```

### Documentation Best Practices

**DO:**
- ✅ Use dated filenames (YYYY-MM-DD prefix)
- ✅ Place in the correct subdirectory
- ✅ Preserve original formatting and content
- ✅ Include source URLs at the top if applicable
- ✅ Keep docs immutable once committed (historical record)

**DON'T:**
- ❌ Modify existing documentation in `/docs/`
- ❌ Mix different source types in same directory
- ❌ Use arbitrary naming conventions
- ❌ Remove or relocate historical documents

## Using Prime Commands

### What are Prime Commands?

Prime commands are custom Claude Code commands that load comprehensive context by reading multiple documentation files at once. They establish a shared knowledge base for AI-assisted work.

### Available Prime Commands

**`/prime:2025-11-17`** - Loads core Regen AI documentation
- Reads all 14 key documents
- Establishes context about architecture, roadmap, partnerships
- Required before creating new content

### Creating a New Prime Command

1. **Create the command file**:
   ```bash
   vim .claude/commands/prime/2025-12-XX.md
   ```

2. **Define what to load**:
   ```markdown
   RUN:
   !git ls-files

   READ
   @.claude/commands/prime/2025-12-XX.md
   @docs/github/2025-09-05-koi-data.md
   @docs/koi/2025-08-19-regen-ai-roadmap.md
   [... add other relevant docs ...]
   ```

3. **Use the command**:
   ```bash
   /prime:2025-12-XX
   ```

### When to Update Prime Commands

Update when:
- New critical documentation is added
- Strategic priorities shift
- Documentation becomes outdated or superseded
- Onboarding new team members who need different context

## Referencing Documentation

### Finding the Right Source

When writing content, reference documentation to ensure accuracy:

**For technical architecture:**
```bash
docs/github/2025-11-12-regen-registry-review-mcp-server-spec.md
docs/github/2025-11-13-regen-koi-mcp-server.md
docs/koi/2025-10-30-regen-knowledge-commons-registry-review-agent-infrastructure.md
```

**For strategic vision:**
```bash
docs/koi/2025-08-19-regen-ai-roadmap.md
docs/paragraph/2025-08-01-regen-ai.md
docs/paragraph/2025-11-04-planetary-data-layer.md
```

**For current status:**
```bash
docs/transcripts/2025-11-07-regen-network-community-call.md  # Most recent
```

**For community programs:**
```bash
docs/paragraph/2025-09-10-announcing-regen-irl.md
docs/paragraph/2025-10-12-regen-irl.md
```

### Maintaining Consistency

Always use the same terminology across posts:
- "Registry Review MCP" (not "Registry Agent MCP")
- "15,000+ documents" (consistent metric for KOI)
- "Phase 2 (Nov 2025 - Jan 2026)" (consistent timeline)
- "Planetary Return on Investment (PROI)" (full term first, then acronym)

## Git Workflow

### Standard Operations

```bash
# Check what's changed
git status

# View differences
git diff content/2025-11-17-foundation.md

# Add new or modified files
git add content/2025-12-02-koi-deep-dive.md

# Commit with descriptive message
git commit -m "Add Week 2 forum post: KOI MCP Deep Dive"

# Push to remote
git push origin main

# Pull latest changes
git pull origin main
```

### Commit Message Conventions

```bash
# Strategy documents
git commit -m "Add 12-week forum update strategy"

# Forum posts
git commit -m "Add Week 2 forum post: KOI MCP Deep Dive"

# Documentation
git commit -m "Add December community call transcript"

# Updates to existing content
git commit -m "Update Week 1 post with community feedback"
```

## Quick Reference

### Weekly Post Checklist

Before publishing each forum post:

- [ ] Loaded context with `/prime:2025-11-17`
- [ ] Reviewed content strategy for the week's theme
- [ ] Followed standard post structure template
- [ ] Referenced source documentation for accuracy
- [ ] Used Discourse markdown formatting
- [ ] Included discussion questions
- [ ] Previewed next week's topic
- [ ] Committed with descriptive message

### Key Metrics & Terms

Use these consistently across all posts:

- **KOI MCP**: 15,000+ documents, semantic search + RDF graph
- **Registry Review MCP**: 7-stage workflow, 70% time reduction target
- **PROI**: Planetary Return on Investment
- **Development Phases**: Phase 2 (Nov 2025 - Jan 2026)
- **Agent Archetypes**: Becca (Registry), Gregory (Methodology), Marie (Full-Stack)
- **Partnership**: Gaia AI × Regen Network (launched August 2025)

## Getting Help

### For Claude Code Users

1. Read `CLAUDE.md` for comprehensive guidance
2. Use `/prime:2025-11-17` to load context
3. Ask specific questions about architecture or content strategy

### For Content Questions

- Review the strategy document: `content/2025-11-17-strategy.md`
- Check previous posts for examples: `content/2025-11-17-foundation.md`
- Reference source documentation in `/docs/` for factual accuracy

### For Technical Questions

- Load context first: `/prime:2025-11-17`
- Check the technical specs in `/docs/github/`
- Review the most recent community call transcript

## Contributing

This repository serves as institutional memory for the Regen AI initiative. When contributing:

1. **Accuracy matters** - All claims must be traceable to source documentation
2. **History matters** - Never modify historical docs, add new dated versions
3. **Consistency matters** - Use standard terminology and metrics
4. **Community matters** - Write for both current and future readers

Every post becomes part of a permanent, searchable archive that AI agents will index and community members will reference for years to come.

---

**Repository maintained by:** Gaia AI Team
**Primary use:** forum.regen.network weekly updates
**Related projects:** [Regen Network](https://regen.network), [Gaia AI](https://gaiaai.xyz)
