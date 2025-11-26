# Regen AI Forum Content

Knowledge archive and content production for [Regen AI](https://forum.regen.network)—planetary intelligence infrastructure built by Gaia AI and Regen Network.


### For Human Contributors

1. **Browse documentation** in `/docs/` to understand the project
2. **Check the strategy** in `content/2025-11-17-strategy.md` for the 12-week content calendar
3. **Review examples** in `content/2025-11-17-foundation.md` for format and style

## Repository Structure

```
/docs/              Historical documentation (read-only)
  /github/          Technical specs and implementation docs
  /koi/             Roadmaps, architecture, agent specifications
  /paragraph/       Published blog posts from paragraph.com/@gaiaai
  /transcripts/     Community call transcripts
  /other/           Interviews and miscellaneous

/content/           Active content production
  *-strategy.md     Content calendars and planning
  *-*.md            Draft forum posts and articles

/resources/         KOI infrastructure source code (submodules/references)
  /koi-net/         KOI protocol implementation
  /koi-processor/   Event processing and embeddings
  /koi-sensors/     Real-time data collection
  /regen-koi-mcp/   MCP server for AI agents

/.claude/           Claude Code configuration
  /commands/prime/  Context-loading commands
```

## Content Workflow

### Creating Forum Posts

1. Load context: `/prime:2025-11-25`
2. Check the week's theme in the strategy document
3. Draft in `content/YYYY-MM-DD-topic.md`
4. Follow the structure from previous posts
5. Use Discourse markdown formatting

### Discourse Markdown Notes

```markdown
![alt text|690x388](upload://HASH.ext)    # Images with dimensions
* List item                                # Use * not -
## Section heading                         # Use ## not #
```

### Committing Changes

```bash
git add content/YYYY-MM-DD-topic.md
git commit -m "Add Week X forum post: [Theme]"
git push origin main
```

## Key Resources

| Resource | Location |
|----------|----------|
| Content strategy | `content/2025-11-17-strategy.md` |
| Style example | `content/2025-11-17-foundation.md` |
| Technical roadmap | `docs/koi/2025-08-19-regen-ai-roadmap.md` |
| Partnership vision | `docs/paragraph/2025-08-01-regen-ai.md` |
| Latest status | `docs/transcripts/2025-11-07-regen-network-community-call.md` |

## Adding Documentation

New documentation goes in `/docs/` with date prefix:

```bash
# Format: docs/[category]/YYYY-MM-DD-descriptive-title.md
docs/transcripts/2025-12-05-community-call.md
docs/paragraph/2025-12-01-new-announcement.md
```

Categories:
- `github/` — Technical specs
- `koi/` — Strategy and architecture
- `paragraph/` — Published posts
- `transcripts/` — Meeting notes
- `other/` — Everything else

After adding key documentation, update the prime command in `.claude/commands/prime/`.

## Links

- [Regen Network Forum](https://forum.regen.network)
- [Gaia AI](https://gaiaai.xyz)
- [Regen Network](https://regen.network)
- [KOI MCP Server](https://github.com/gaiaaiagent/regen-koi-mcp)

---

**Maintained by:** Gaia AI Team
**Purpose:** Weekly updates for forum.regen.network
