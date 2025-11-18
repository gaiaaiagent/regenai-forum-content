# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is the **Regen AI Forum Content** repository - a knowledge archive and content production system for the Regen AI initiative (collaboration between Gaia AI and Regen Network). It serves as:

1. **Documentation Archive** - Comprehensive collection of technical specs, roadmaps, blog posts, and transcripts
2. **Content Production** - Strategic planning and draft creation for forum.regen.network weekly updates
3. **Knowledge Base** - Source material for AI agents via the KOI (Knowledge Organization Infrastructure) MCP server

## Repository Architecture

### Directory Structure

```
/docs/          - Read-only documentation archive (source material)
  /github/      - GitHub documentation (KOI data, MCP specs)
  /koi/         - KOI documentation (roadmaps, agent specs, infrastructure)
  /other/       - Interviews and miscellaneous content
  /paragraph/   - Published blog posts from paragraph.com/@gaiaai
  /transcripts/ - Community call transcripts

/content/       - Active content production (forum posts, strategies)
  *-strategy.md - Strategic planning documents
  *-foundation.md - Draft forum posts and articles

/.claude/       - Claude Code configuration
  /commands/    - Custom slash commands
    /prime/     - Prime commands for loading documentation context
```

### Key Architectural Patterns

**Documentation Organization:**
- All docs are dated with `YYYY-MM-DD` prefix for chronological tracking
- Source categorization (github, koi, paragraph, transcripts, other) reflects origin and purpose
- Documents are immutable once committed - they're historical reference material

**Content Production Workflow:**
1. Strategy documents define multi-week content calendars
2. Individual posts drafted as separate markdown files
3. Posts reference documentation in `/docs/` for factual accuracy
4. Forum posts use Discourse markdown formatting (different from GitHub markdown)

**Prime Command Pattern:**
- The `/prime:2025-11-17` command loads comprehensive context by reading all key documentation
- This establishes shared knowledge base for AI-assisted content creation
- Pattern: `RUN: !git ls-files` followed by `READ @path/to/doc.md` for each relevant file

## Working with This Repository

### Loading Context

Before creating content, load the documentation context:
```bash
/prime:2025-11-17
```

This reads all 14 core documentation files to establish comprehensive understanding of:
- Regen AI technical architecture (3 MCP servers: KOI, Ledger, Registry Review)
- Strategic roadmap and development phases
- Community programs (Regen IRL grants, partnerships)
- Historical context and evolution

### Creating Forum Content

**For weekly forum updates:**
1. Reference the strategy document (`content/2025-11-17-strategy.md`) for:
   - 12-week content calendar
   - Standard post structure template
   - Engagement tactics and cross-platform syndication

2. Follow the established format from `content/2025-11-17-foundation.md`:
   - Title: `[Week X/12] Regen AI Update: [Theme] - [Date]`
   - Metadata header with author and key focus
   - Main content (500-800 words)
   - Discussion questions for community engagement
   - Preview of next week's topic
   - Resources & links section

3. **Discourse-specific markdown:**
   - Images: `![alt text|WIDTHxHEIGHT](upload://HASH.ext)`
   - Lists use `*` not `-` for compatibility
   - Headings use `##` (no single `#` except for title)

### Git Workflow

This is a documentation and content repository - there's no build process, tests, or compilation.

**Standard workflow:**
```bash
# Check status
git status

# Add new content
git add content/2025-11-XX-topic.md

# Commit with descriptive message
git commit -m "Add Week X forum post: [Theme]"

# Push to remote
git push origin main
```

**Commit message conventions:**
- Strategy docs: `"Add 12-week forum update strategy"`
- Forum posts: `"Add Week X forum post: [Theme]"`
- Documentation updates: `"Add [source] documentation: [title]"`

## Key Content Relationships

### The Regen AI Ecosystem

Understanding how pieces connect is critical for accurate content creation:

**Technical Infrastructure:**
- **KOI MCP** - Knowledge Organization Infrastructure (15k+ docs, semantic search, RDF graph)
- **Regen Ledger MCP** - On-chain data queries (eco-credits, methodologies, governance)
- **Registry Review MCP** - 7-stage workflow for automating project onboarding

**Agent Archetypes (Generation 2):**
- Registry Agent (Becca) - Automates registry reviews
- Methodology Evaluation Agent (Gregory) - Technical analysis
- Full-Stack/CTO Agent (Marie) - Comprehensive system knowledge
- Voice of Nature - Data-informed governance proposals

**Development Phases:**
- Phase 1 (Complete): Initial agents, KOI sensors, basic MCPs
- Phase 2 (Nov 2025 - Jan 2026): Registry MCP intensive, agent refinement, digest generation
- Phase 3 (Future): External agents, community portal, full automation

**Strategic Partnerships:**
- Gaia AI × Regen Network alliance (August 2025)
- Token alignment around $REGEN
- Integration with DaoDao for role-based permissions
- Eliza OS framework for agent orchestration

### Critical Reference Documents

When writing about:

**Technical Architecture:**
- `docs/github/2025-11-12-regen-registry-review-mcp-server-spec.md` - Complete Registry Review spec
- `docs/github/2025-11-13-regen-koi-mcp-server.md` - KOI MCP implementation
- `docs/koi/2025-10-30-regen-knowledge-commons-registry-review-agent-infrastructure.md` - System architecture

**Strategic Vision:**
- `docs/koi/2025-08-19-regen-ai-roadmap.md` - 12-month roadmap
- `docs/paragraph/2025-08-01-regen-ai.md` - Partnership announcement
- `docs/paragraph/2025-11-04-planetary-data-layer.md` - UN presentation and data legibility

**Community Programs:**
- `docs/paragraph/2025-09-10-announcing-regen-irl.md` - Grant program details
- `docs/paragraph/2025-10-12-regen-irl.md` - Grant winners and PROI framework

**Current State:**
- `docs/transcripts/2025-11-07-regen-network-community-call.md` - November 2025 community call (most recent status)

## Content Quality Standards

### Accuracy Requirements

All technical claims must be traceable to source documentation:
- MCP capabilities → Reference MCP spec documents
- Development timelines → Reference roadmap or community call transcript
- Partnership details → Reference announcement posts
- Agent capabilities → Reference agent specs or infrastructure docs

### Tone and Style

**For forum posts:**
- Professional but accessible - balance technical depth with clarity
- Inclusive and inviting - encourage community participation
- Honest and transparent - share challenges, not just successes
- Specific and concrete - code examples, real data, clear metrics
- Forward-looking - always preview next steps

**Avoid:**
- Marketing hyperbole or unsubstantiated claims
- Overly technical jargon without explanation
- Promising features not yet in development
- Generic AI/blockchain buzzwords without context

### Engagement Optimization

Every forum post must include:
1. **Clear value proposition** - Why should readers care?
2. **Concrete deliverables** - What can they see/use/test?
3. **Participation hooks** - How can they get involved?
4. **Discussion questions** - Specific prompts for comments
5. **Next steps preview** - Build anticipation for next update

## Special Considerations

### Forum vs. Other Platforms

The forum is the **primary, authoritative source**. Other platforms (Telegram, Discord, Twitter) syndicate forum content with short summaries and links back. Never create primary content for other platforms first.

### Knowledge Layering

Gregory's emphasis: "The forum is our central knowledge layer - this is where we'll build context."

Every post contributes to a permanent, searchable archive that:
- Future developers and community members will reference
- AI agents will index via KOI MCP
- Serves as institutional memory for the project
- Demonstrates transparency and accountability

Therefore, posts should be:
- Comprehensively documented with links to resources
- Tagged appropriately for search and categorization
- Written for both immediate audience and future readers
- Maintained in the weekly updates index (pinned thread)

### Cross-Platform Consistency

When the same information appears in multiple docs (roadmap, forum post, community call), maintain consistency:
- Use exact same terminology (e.g., "Registry Review MCP" not "Registry Agent MCP")
- Keep metrics consistent (e.g., "15,000+ documents" in KOI)
- Align timelines (Phase 2 is always "Nov 2025 - Jan 2026")
- Reference the same source documents

## Working with Documentation Updates

### Adding New Documentation

When adding new source material to `/docs/`:

1. **Maintain naming convention:** `YYYY-MM-DD-descriptive-title.md`
2. **Place in appropriate subdirectory:**
   - `/github/` - Technical specs, implementation docs
   - `/koi/` - Roadmaps, strategy, architecture
   - `/paragraph/` - Published blog posts
   - `/transcripts/` - Meeting notes, community calls
   - `/other/` - Interviews, miscellaneous

3. **Update prime command** if the doc should be part of standard context loading

4. **Update strategy document** if it affects content calendar or messaging

### Documentation Integrity

Never modify historical documentation in `/docs/`. If information is outdated:
- Add new dated document with updated information
- Reference the evolution in forum posts ("As we shared in August... now in November...")
- Maintain the historical record for context

This repository is a knowledge commons - treat it with care and respect for future users.
