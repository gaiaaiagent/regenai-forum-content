# Google Gemini Gems Research Report
## Future Regen AI Integration Considerations

**Report Date:** December 9, 2025
**Prepared for:** Regen AI Blog Post on Future Integrations
**Research Focus:** Gemini Gems capabilities, limitations, and MCP integration potential

---

## Executive Summary

Google Gemini Gems represent a consumer-friendly approach to AI customization that differs significantly from ChatGPT's Custom GPTs and Claude's ecosystem. While Gems offer compelling advantages (free access, Google Workspace integration, large context windows), they currently lack critical features for developer integration: no public API access, no sharing marketplace, and no direct MCP protocol support. This limits their immediate viability for Regen MCP integration compared to Claude Code and GPT platforms.

**Key Finding:** Gems are best suited for personal productivity and organizational workflows within Google's ecosystem, but are not yet ready for third-party developer integration or customer-facing deployments.

---

## 1. What are Gemini Gems?

Gemini Gems are specialized AI assistants built within Google Gemini that can be customized with specific instructions and knowledge files for particular tasks and workflows.

### Core Characteristics

**Definition:** Gems are customizable versions of Google Gemini that you can program with specific instructions and knowledge files for it to consult every time it responds. They function as AI experts tailored to specific use cases, reducing the need for repetitive prompting.

**Purpose:** At Google I/O, Google introduced Gems as a tool that lets you create custom experts for any task within Gemini. The idea behind Gems is to give you an AI chat agent that's designed to help you exactly how you want it to.

**Functionality:** With Gems, you can create specific and repeatable instructions for Gemini to follow. By creating a Gem with all of the info about your goals and preferences, or using a premade Gem designed for a certain action, the Gem acts as a shortcut every time you want to explore a topic with similar instructions.

### How Gems Work

**Creation Process:** Users can create Gems by writing instructions, giving them a name, and then chatting with them whenever needed. The process is straightforward:

1. Go to gemini.google.com and log in
2. In the side panel, click "Gem manager"
3. Click "New Gem"
4. Write instructions following four categories:
   - **Persona:** What role should the Gem take on?
   - **Task:** What should the Gem create or do for you?
   - **Context:** How should the Gem perform these tasks?
   - **Format:** How should the Gem present results?

**AI-Assisted Creation:** The magic wand icon at the bottom of the text box allows Gemini to help re-write and expand on instructions, making it easier to create effective Gems.

**Premade Options:** Google provides starter Gems including Brainstormer, Career guide, Coding partner, Learning coach, and Writing editor. Users can also make a copy of premade Gems to customize them for specific needs.

### Use Cases

**Personal Productivity:**
- Running coach with personalized training plans
- Meeting notes summarizer with specific style and format requirements
- Writing assistant adhering to personal style guides
- Research assistant for specific domains

**Business Applications:**
- Custom style guide enforcement for team communications
- Automated report generation with consistent formatting
- Domain-specific knowledge assistants (legal, technical, etc.)
- Customer support FAQ handlers

---

## 2. Gems vs GPTs vs Claude: Comparative Analysis

### Feature Comparison Matrix

| Feature | Gemini Gems | ChatGPT Custom GPTs | Claude (MCP) |
|---------|-------------|---------------------|--------------|
| **Free Creation** | Yes (anyone with Gmail) | No ($20/month required) | API-based pricing |
| **Free Usage** | Yes | GPTs: Yes / Projects: No | API-based pricing |
| **Knowledge Files** | 10 files max | 20 files max | Context window-based |
| **Public Marketplace** | No | Yes | No (community MCP servers) |
| **Sharing Capability** | Limited (org sharing only) | Full (private/link/public) | N/A (open protocol) |
| **Image Generation** | No | Yes (DALL-E) | Limited |
| **Voice Mode** | Limited (not with Gems) | Yes | Yes (in some interfaces) |
| **Creation Interface** | Manual only | Guided + Manual | Code/configuration |
| **API Access** | No | Yes (GPT Actions) | Yes (MCP protocol) |
| **Context Window** | Very large (Gemini advantage) | Standard | Very large |
| **External Integrations** | Google Workspace native | Actions + plugins | MCP servers (thousands) |

### Key Differentiators

**Gemini Gems Advantages:**
- **Free Access:** Anyone with a Gmail account can create Gems for free, unlike ChatGPT which requires a $20/month Plus subscription
- **Context Window:** Gemini's context window is significantly larger, making it better for analyzing massive projects (500-page documents, entire codebases)
- **Native Google Integration:** Automatic Gmail integration, direct Google Drive document access, and immediate calendar information retrieval with no API calls required
- **Team Collaboration:** Can be shared within organizations similar to Google Docs (as of September 2025)
- **Lower Hallucination:** For massive projects, Gemini Gems often hallucinate less and remember more than standard GPTs

**ChatGPT Custom GPTs Advantages:**
- **Public Marketplace:** Full GPT marketplace allows discovery and sharing of custom GPTs publicly
- **Advanced Sharing:** Three sharing options (private, link-based, public)
- **More Files:** 20-file knowledge base limit vs Gems' 10-file limit
- **Multimodal Features:** Web browsing, image generation, code execution all available
- **Guided Creation:** "Create" mode allows conversational GPT building
- **API Integration:** GPT Actions enable external API connections and automation

**Claude/MCP Advantages:**
- **Open Standard:** MCP is model-agnostic and prevents vendor lock-in
- **Ecosystem Scale:** Thousands of community-built MCP servers
- **Developer-First:** Designed for programmatic integration and automation
- **Multi-Service Integration:** Can connect to Jira, Confluence, Zapier, Intercom, Asana, Square, Sentry, PayPal, Linear, Plaid, and more
- **Parallel Tool Use:** Claude excels at multi-tool orchestration in agentic workflows
- **Research with Citations:** Can fold multiple external sources into research with proper citations

### Accessibility and Pricing

**Gemini Gems:**
- Free for all Gmail users
- Gems available for Gemini Advanced, Business and Enterprise users
- No cost barrier to creation or usage

**ChatGPT:**
- Requires $20/month Plus subscription to CREATE Custom GPTs
- Anyone can USE publicly shared GPTs without subscription
- Enterprise tier available for organizations

**Claude Code/MCP:**
- API-based pricing model
- Pay-per-token usage
- Claude Sonnet 4.5 roughly twice the cost of GPT-5
- MCP implementation is free and open-source

### Creation Experience

**Ease of Use Rankings:**
1. **ChatGPT:** Guided creation mode with conversational interface makes it easiest for non-technical users
2. **Gemini Gems:** Manual instruction writing but with AI assistance via magic wand feature
3. **Claude MCP:** Requires technical configuration and understanding of protocols

### Best Use Cases by Platform

**Use Gemini Gems for:**
- Quick productivity hacks within Google ecosystem
- Personal assistants that need large context windows
- Team workflows already centered on Google Workspace
- Free access requirements

**Use ChatGPT GPTs for:**
- Public sharing and community distribution
- Multimodal workflows (images, code, web)
- Monetization opportunities via GPT Store
- Extensive knowledge base requirements (20 files)

**Use Claude MCP for:**
- Developer integrations and automation
- Multi-service orchestration
- Customer-facing AI deployments
- Open-source and vendor-neutral requirements

---

## 3. Gems Capabilities and Limitations

### Current Capabilities

**Knowledge Integration:**
- Upload up to 10 files when creating a Gem for additional reference information
- Can anchor Gems to specific Google Drive files (Docs, Sheets)
- Access to Gemini's large context window for processing extensive documents
- Integration with Google's Knowledge Graph for structured information access

**Google Workspace Integration (2025):**
- AI-driven assistants integrated directly into side panels of Docs, Sheets, and Gmail
- Real-time assistance without switching between tools
- Automatic and secure Gmail integration
- Direct Google Drive document access
- Immediate calendar information retrieval with no API calls or webhooks required

**External Data Access:**
- Can connect to external data sources and APIs (in theory)
- Can incorporate conditional logic and looping for complex operations
- Ability to pull data from external sources like CRMs for analysis and reporting

**Workflow Automation:**
- Google Workspace Flows can use Gems for multi-step automation
- Can perform research, analysis, and content generation
- Designed for repeatable tasks with consistent requirements

**Education Integration:**
- Gems in Gemini Learning Tools Interoperability (LTI) rolled out September 2025
- Integration with Canvas by Instructure and PowerSchool Schoology Learning
- Educators can create FAQ Gems for students
- Real-time coaching capabilities

**Team Collaboration:**
- Sharing capability launched September 2025
- Powered by Google Drive sharing technology
- Recipients can edit, use, or copy shared Gems
- Admin controls for organizational Gem sharing
- Similar interface to sharing Google Docs

### Current Limitations

**Platform Restrictions:**
- Can only create and edit Gems in web app (not mobile)
- Cannot use Gems with Gemini Live (voice mode)
- Cannot use Gems to create AI-generated images
- Limited to 10 knowledge files vs GPTs' 20 files

**Sharing and Discovery:**
- No public marketplace for discovering Gems
- Sharing limited to direct organization-to-organization or individual sharing
- Cannot browse or search community-created Gems
- No monetization options for Gem creators

**API and Programmatic Access:**
- **Critical Limitation:** No direct API access to custom Gems
- Cannot invoke Gems programmatically through Gemini API
- System instructions in API don't produce same results as Gems
- No documented way to export or replicate Gem configurations via code

**Integration Limitations:**
- No documented MCP (Model Context Protocol) support for Gems specifically
- Cannot create custom actions or plugins like GPTs
- External data integration capabilities are theoretical but not well-documented
- Limited third-party integration compared to GPT Actions or MCP servers

**Development Status:**
- Manual creation only (no guided conversational mode like GPTs)
- Limited documentation for advanced use cases
- No version control or change tracking for Gems
- Cannot programmatically manage or deploy Gems at scale

### Technical Constraints

**File and Context:**
- 10-file knowledge base limit (oddly lower than GPTs despite larger context window)
- No code execution environment
- Cannot access real-time web browsing within Gems
- Limited multimodal capabilities compared to competitors

**Deployment:**
- Internal/organizational use only
- Not suitable for customer-facing deployments
- No white-labeling or embedding options
- Tied to Google account ecosystem

---

## 4. MCP Integration Analysis

### Current State of Gemini and MCP

**MCP Support in Gemini Ecosystem:**

Google Gemini has MCP (Model Context Protocol) support, but it's important to distinguish between different parts of the Gemini ecosystem:

1. **Gemini CLI:** Has full MCP server support for custom integrations
2. **Gemini API:** Can work with MCP through proper implementation
3. **Gemini Gems:** No documented MCP support or integration capability

**Gemini CLI MCP Implementation:**

The Gemini CLI provides comprehensive support for Model Context Protocol (MCP) servers:
- MCP servers act as a bridge between the Gemini model and local environment or external services
- Configure MCP servers in `~/.gemini/settings.json` to extend Gemini CLI with custom tools
- Seamless integration with FastMCP (Python's leading MCP library)
- Can install local STDIO transport MCP servers using `fastmcp install gemini-cli`

**MCP Server Capabilities:**
- Discover tools through standardized schema definitions
- Execute tools with defined arguments and receive structured responses
- Access resources from databases, APIs, custom scripts, or specialized workflows
- Extend Gemini CLI's capabilities beyond built-in features

**FastMCP Integration (December 2025):**

As of FastMCP v2.12.3, developers can install local STDIO transport MCP servers built with FastMCP using simple commands. This simplifies MCP server development significantly.

### Gemini as MCP Server

**Reverse Integration:**

Interestingly, there's a dedicated MCP server that wraps the @google/genai SDK, exposing Google's Gemini model capabilities as standard MCP tools. This allows:
- Other LLMs (like Claude) to leverage Gemini's features as a backend
- Consistent, tool-based interface managed via MCP standard
- Support for latest Gemini models including gemini-1.5-pro-latest, gemini-1.5-flash, and gemini-2.5-pro

This is the opposite of what we'd want for Regen integration - it lets Claude use Gemini, not Gemini use external MCP servers.

### MCP Limitations with Gemini

**Documented Constraints (March 2025):**
- Supported parameter types in Python are limited
- Automatic function calling is a Python SDK feature only
- No specific documentation about Gems having MCP support

**Critical Gap for Regen Integration:**

The research found **no evidence** that Gemini Gems can:
- Connect to external MCP servers
- Act as MCP clients
- Use MCP protocol for external integrations
- Access community-built MCP tools

This is fundamentally different from Claude Code's architecture, where MCP is a first-class integration method.

### Comparison: Claude MCP vs Gemini Integration

**Claude Code MCP:**
- Native MCP support enabling seamless third-party integrations
- Can connect to thousands of community-built MCP servers
- Remote MCP support launched June 2025
- Can act across services like Jira, Confluence, Zapier, Intercom, Asana, Square, Sentry, PayPal, Linear, and Plaid
- Open standard that prevents vendor lock-in
- Model-agnostic design (any LLM can implement MCP)
- Community-driven tool ecosystem

**Gemini Integration Approach:**
- Focus on Google Workspace native integrations
- API-based external connections
- Function calling for custom tools
- No consumer-facing MCP client capability in Gems
- Gemini CLI has MCP support for developer use cases
- Can be used AS an MCP server by other systems

**Key Insight:** Google's integration strategy focuses on tight Google Workspace integration and developer API access, rather than an open protocol like MCP for consumer-facing customization.

---

## 5. Potential for Regen MCP Integration

### Technical Feasibility Assessment

**Direct Gems Integration: NOT CURRENTLY FEASIBLE**

Based on research findings, integrating Regen MCP with Gemini Gems faces critical blockers:

1. **No API Access:** Gems cannot be accessed programmatically through any documented API
2. **No MCP Client Support:** Gems do not support connecting to external MCP servers
3. **No Custom Actions:** Unlike GPT Actions, Gems lack a mechanism for custom external integrations
4. **Consumer-Only Interface:** Gems are designed for personal/organizational use via web UI only

**Rating:** ❌ Not Feasible (Current State)

### Alternative Integration Paths

**Option 1: Gemini API with System Instructions**

Instead of Gems, use the Gemini API with custom system instructions:

**Pros:**
- Full programmatic access via REST API
- Function calling capabilities for external tools
- Can be integrated into custom applications
- Support for grounding with Google Search
- URL context capabilities
- Structured outputs support

**Cons:**
- Different behavior than Gems (users report system instructions don't match Gem results)
- Requires API billing after free tier
- No pre-configured "Gem" shortcuts for users
- Requires custom implementation work

**Feasibility:** ✅ Feasible but requires significant development

**Option 2: Gemini CLI with MCP Servers**

Use Gemini CLI's native MCP support for developer workflows:

**Pros:**
- Native MCP server support
- Can configure custom MCP servers in settings
- Works with FastMCP ecosystem
- Terminal-based workflows for developers

**Cons:**
- Not accessible to non-technical users
- Requires command-line knowledge
- Limited to local development environments
- Not suitable for consumer-facing features

**Feasibility:** ✅ Feasible for developer tools only

**Option 3: Wait for Gems API/MCP Support**

Monitor Google's roadmap for future Gems capabilities:

**Indicators to Watch:**
- Public API access for Gems
- MCP client support announcement
- Gems marketplace launch (would require programmatic access)
- Enterprise features for Gem deployment

**Current Timeline:** No public roadmap information found

**Feasibility:** ⏳ Unknown timeline

### Comparison to Existing Regen Integrations

**Claude Code + MCP (Current State):**
- ✅ Native MCP support
- ✅ Can connect to Regen MCP servers
- ✅ Developer-friendly integration
- ✅ Open protocol
- ✅ Community adoption

**ChatGPT + GPT Actions (Potential):**
- ✅ Custom Actions API
- ✅ External service integration
- ✅ Public marketplace distribution
- ✅ Consumer-accessible
- ⚠️ Proprietary integration method

**Gemini Gems (Current Assessment):**
- ❌ No MCP support
- ❌ No API access
- ❌ No custom actions
- ❌ No marketplace
- ✅ Free access
- ✅ Google Workspace integration

### User Experience Considerations

**Ideal Regen Integration Requirements:**
1. Users can easily add Regen data access to their AI assistant
2. Integration works within familiar chat interface
3. No complex technical setup required
4. Can access Regen network data, proposals, projects
5. Maintains security and privacy controls
6. Cross-platform availability

**How Each Platform Meets Requirements:**

**Claude Code (MCP):**
- Setup: Medium complexity (config file editing)
- Interface: Terminal-based (developer-focused)
- Distribution: Install MCP server once
- Access: Full Regen API capabilities via MCP
- Security: Token-based, user-controlled
- Rating: ⭐⭐⭐⭐ (Excellent for developers)

**ChatGPT (Hypothetical GPT Actions):**
- Setup: Low complexity (marketplace install or GPT creation)
- Interface: Familiar chat UI
- Distribution: GPT Store or private link
- Access: Custom API endpoints via Actions
- Security: OAuth or API key integration
- Rating: ⭐⭐⭐⭐⭐ (Excellent for consumers)

**Gemini Gems (Current):**
- Setup: N/A (not technically possible)
- Interface: Would be familiar chat UI if possible
- Distribution: N/A
- Access: N/A
- Security: N/A
- Rating: ⭐ (Not feasible currently)

### Recommended Approach

**Short-term (0-6 months):**
- ❌ **Do not** prioritize Gemini Gems integration
- ✅ Focus on Claude Code MCP integration (already viable)
- ✅ Consider ChatGPT GPT Actions as secondary platform
- ✅ Document limitations for Gemini users

**Medium-term (6-12 months):**
- 👁️ Monitor Google's Gems roadmap announcements
- 🔬 Experiment with Gemini API + system instructions approach
- 📋 Gather user feedback on demand for Gemini support
- 🤝 Engage with Google AI developer community

**Long-term (12+ months):**
- 🎯 Re-evaluate if Gems gains API or MCP support
- 🏗️ Build Gemini API integration if user demand warrants it
- 🌐 Maintain platform-agnostic MCP approach for flexibility

---

## 6. Roadmap and Strategic Considerations

### Google's Gemini Ecosystem Trajectory

**Recent Major Updates (2025):**

**March 2025 - Wider Availability:**
- Gems became free for all users (not just paid tiers)
- Expanded to more Google Workspace editions
- Added file anchoring to Google Drive documents
- Mobile app support announced for later date

**September 2025 - Sharing and Collaboration:**
- Launched Gems sharing capabilities
- Integration with Learning Management Systems (LTI)
- Admin controls for enterprise deployment
- Drive-like sharing interface

**Gemini 3 API Updates (Latest):**
- New `thinking_level` parameter for reasoning depth control
- `media_resolution` parameter for token/fidelity balance
- Grounding with Google Search + structured outputs
- Enhanced agentic capabilities
- Real-time streaming via Live API

**Key Observations:**

Google's development focus appears to be:
1. Making Gems free and accessible
2. Building collaboration features (sharing)
3. Deepening Google Workspace integration
4. Expanding to education sector
5. Advancing the Gemini API for developers

**What's NOT in the Roadmap (publicly):**
- Gems marketplace
- Gems API access
- MCP client support for Gems
- Custom actions/plugins for Gems
- Programmatic Gem deployment

### Strategic Patterns

**Google's Integration Philosophy:**

Google appears to be taking a **walled garden approach** with Gems:
- Deep integration within Google ecosystem
- Free access to drive adoption
- Sharing within trusted networks
- Focus on productivity and education
- Separate developer API for advanced use cases

This contrasts with:
- **OpenAI's marketplace approach** (GPT Store for public distribution)
- **Anthropic's open protocol approach** (MCP as universal standard)

**Implications for Third-Party Integration:**

Google seems to be positioning:
- **Gems** = Consumer productivity tool within Google ecosystem
- **Gemini API** = Developer integration point for custom applications
- **Gemini CLI** = Developer tool with MCP support

The lack of Gems API suggests Google wants to:
- Control the user experience tightly
- Keep users within Google Workspace
- Avoid fragmentation via third-party Gem stores
- Drive API revenue for developer integrations

### Competitive Landscape Evolution

**MCP Adoption Trends:**

Since MCP's launch in November 2024:
- Thousands of community-built MCP servers
- SDKs available for all major programming languages
- Industry adoption as de-facto standard for agent integrations
- Model-agnostic design promoting flexibility

**Market Positioning:**

The AI assistant integration market is evolving into distinct tiers:

1. **Open Protocol Layer (MCP):**
   - Led by Anthropic/Claude
   - Community-driven ecosystem
   - Developer-first approach
   - Cross-platform compatibility

2. **Proprietary Platform Layer:**
   - ChatGPT GPT Store (consumer-facing, monetization)
   - Gemini Workspace Integration (enterprise productivity)
   - Each with unique strengths and lock-in

3. **Hybrid Approaches:**
   - Some platforms bridging internal productivity and customer deployment
   - Custom implementations using MCP servers as backend

**Where Gemini Fits:**

Gemini is carving out the **enterprise productivity** niche:
- Free tier for individual adoption
- Deep Google Workspace integration
- Admin controls for IT departments
- Education sector focus
- Less emphasis on public sharing/marketplace

### Future Scenarios

**Scenario 1: Gems Remains Closed (Likely)**

**Probability:** High (70%)

**Indicators:**
- No public roadmap mentions of API access
- Focus on internal sharing not marketplace
- Separate Gemini API for developers
- Pattern matches Google's historical approach

**Impact on Regen:**
- Gems integration remains non-viable
- Would need to pursue Gemini API integration separately
- User experience would differ from Claude/GPT integrations
- Limited consumer accessibility compared to competitors

**Scenario 2: Gems Gains Limited API (Moderate)**

**Probability:** Medium (25%)

**Potential triggers:**
- Enterprise customer demand for programmatic Gem deployment
- Competitive pressure from GPT marketplace success
- Developer community feedback
- Workspace automation use cases

**What this might look like:**
- Admin API for bulk Gem creation/management
- Workspace-scoped API access
- Still no public marketplace
- Enterprise/education focus

**Impact on Regen:**
- Might enable organization-level integration
- Still not consumer-friendly
- Would require enterprise relationships
- Limited compared to MCP/GPT approaches

**Scenario 3: Gemini Adopts MCP (Unlikely)**

**Probability:** Low (5%)

**Why it's unlikely:**
- Google typically builds proprietary solutions
- Gemini CLI already has MCP (separate tool)
- Workspace integration is the priority
- MCP adoption would commoditize their differentiation

**If it happened:**
- Would be game-changing for integration ecosystem
- Regen could deploy same MCP servers across all platforms
- Google's ecosystem would open significantly
- Unlikely given strategic direction

### Recommendations for Regen AI

**Strategic Positioning:**

1. **Lead with MCP-first approach**
   - Claude Code integration as flagship
   - Benefits from open standard and ecosystem growth
   - Future-proof against platform changes
   - Appeals to developer community

2. **Consider GPT Actions as consumer bridge**
   - Broader consumer reach via GPT Store
   - Familiar chat interface
   - Complementary to MCP approach
   - Different user demographics

3. **Monitor but don't prioritize Gemini Gems**
   - Keep watching Google's announcements
   - Re-evaluate quarterly
   - Don't invest development resources yet
   - Document limitation clearly for users

**Communication Strategy:**

Be transparent about platform support:
- "Regen MCP integration works with Claude Code and other MCP-compatible platforms"
- "We're exploring ChatGPT integration for broader accessibility"
- "Gemini Gems integration is not currently possible due to platform limitations, but we're monitoring Google's roadmap"

**Resource Allocation:**

Suggested priority order for integration development:
1. ✅ **Claude Code MCP** (high priority, already viable)
2. 🔄 **ChatGPT GPT Actions** (medium priority, good user reach)
3. 🔬 **Gemini API** (low priority, if enterprise demand)
4. ⏸️ **Gemini Gems** (on hold until feasible)

**Long-term Platform Strategy:**

The market is fragmenting between:
- **Developer tools** (Claude Code, MCP ecosystem)
- **Consumer platforms** (ChatGPT, Claude consumer apps)
- **Enterprise productivity** (Gemini Workspace, Microsoft Copilot)

Regen should consider:
- Which user segments are most valuable
- Where regenerative finance community already exists
- Platform alignment with values (open source, transparency)
- Development resource constraints

**Developer Community Engagement:**

Given MCP's community-driven growth:
- Open source Regen MCP server
- Contribute to MCP ecosystem
- Share integration guides
- Build in public to attract contributors

This approach:
- Reduces vendor lock-in
- Attracts developer mindshare
- Aligns with regenerative values
- Works across any MCP-compatible platform

---

## Conclusion

**Key Findings Summary:**

1. **Gemini Gems** are powerful productivity tools within Google's ecosystem but lack the programmatic access necessary for third-party integration like Regen MCP.

2. **No current path** exists for integrating Regen MCP with Gemini Gems due to absence of API access, MCP support, or custom action capabilities.

3. **Alternative approaches** (Gemini API, Gemini CLI) are technically feasible but offer different user experiences and limitations.

4. **Google's strategy** appears focused on tight Workspace integration and free consumer access rather than open ecosystem development.

5. **MCP ecosystem** (led by Claude) offers the most promising path for open, cross-platform AI integration.

6. **ChatGPT's approach** (GPT Store, Actions) provides better consumer accessibility than current Gemini options.

**Strategic Recommendation:**

**Focus Regen integration efforts on Claude Code MCP** as the primary platform, with **ChatGPT GPT Actions as a secondary option** for broader consumer reach. **Defer Gemini integration** until Google provides programmatic access to Gems or MCP client support emerges.

**Monitor Google's roadmap** quarterly, but don't allocate development resources until clear integration paths emerge. Be transparent with users about platform limitations while highlighting the benefits of the open MCP standard.

The regenerative finance community will be best served by **open, interoperable integration approaches** that avoid vendor lock-in and promote ecosystem collaboration - values that align more closely with Claude's MCP standard than with current Gemini Gems architecture.

---

## Sources

### Gemini Gems Overview
- [Gemini Gems — build custom AI experts from Gemini](https://gemini.google/overview/gems/)
- [How to use Gems - Gemini Apps Help](https://support.google.com/gemini/answer/15236405?hl=en)
- [How to use Gems, Google's custom AI tools](https://blog.google/products/gemini/google-gems-tips/)
- [A beginner's guide to Google Gemini Gems](https://www.computerworld.com/article/4054876/a-beginners-guide-to-google-gemini-gems.html)
- [What are Gemini Gems? And how to use them | Zapier](https://zapier.com/blog/gemini-gems/)
- [Get started with Gems in Gemini Apps - Gemini Apps Help](https://support.google.com/gemini/answer/15236321?hl=en)

### Capabilities and Integration
- [Building agents with Google Gemini and open source frameworks - Google Developers Blog](https://developers.googleblog.com/building-agents-google-gemini-open-source-frameworks/)
- [Gemini - Integrating External Data](https://www.tutorialspoint.com/gemini/gemini-integrating-external-data.htm)
- [Gemini Gems Integration Elevates Data Productivity in Google Workspace](https://connectcx.ai/gemini-gems-elevating-data-productivity-in-google-workspace/)
- [Gemini: plug-ins, add-ons, and third-party extensions in 2025](https://www.datastudios.org/post/gemini-plug-ins-add-ons-and-third-party-extensions-in-2025)

### Comparison with GPTs
- [Gemini vs. ChatGPT: What's the difference? [2025] | Zapier](https://zapier.com/blog/gemini-vs-chatgpt/)
- [Google Gemini Gems vs ChatGPT Projects (Step-by-Step Comparison for Beginners)](https://www.godofprompt.ai/blog/gemini-gems-vs-chatgpt-projects)
- [Custom GPTs vs. Gemini Gems: Who Wins?](https://learnprompting.org/blog/custom-gpts-vs-gemini-gems)
- [Gemini vs ChatGPT: Which AI Bot Reigns in 2025](https://www.leanware.co/insights/gemini-vs-chatgpt-comparison)
- [Gemini Gems vs. ChatGPT CustomGPTs: A Marketer's Guide to AI Mini Agents](https://www.cmswire.com/digital-marketing/gemini-gems-vs-chatgpt-customgpts-a-marketers-guide-to-ai-mini-agents/)

### MCP Integration
- [Model Context Protocol(MCP) with Google Gemini 2.5 Pro - Deep Dive](https://medium.com/google-cloud/model-context-protocol-mcp-with-google-gemini-llm-a-deep-dive-full-code-ea16e3fac9a3)
- [GitHub - bsmi021/mcp-gemini-server](https://github.com/bsmi021/mcp-gemini-server)
- [MCP servers with the Gemini CLI | gemini-cli](https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html)
- [Build multilingual chatbots with Gemini, Gemma, and MCP | Google Cloud Blog](https://cloud.google.com/blog/products/ai-machine-learning/build-multilingual-chatbots-with-gemini-gemma-and-mcp)
- [Gemini CLI 🤝 FastMCP: Simplifying MCP server development](https://developers.googleblog.com/en/gemini-cli-fastmcp-simplifying-mcp-server-development/)
- [Build MCP servers using vibe coding with Gemini 2.5 Pro](https://cloud.google.com/blog/products/ai-machine-learning/build-mcp-servers-using-vibe-coding-with-gemini-2-5-pro/)

### API and Programmatic Access
- [Accessing gemini gems through api - Google AI Developers Forum](https://discuss.ai.google.dev/t/accessing-gemini-gems-through-api/40534)
- [Are Gems available via API? - Gemini Apps Community](https://support.google.com/gemini/thread/313792663/are-gems-available-via-api?hl=en)
- [Gemini API | Google AI for Developers](https://ai.google.dev/gemini-api/docs)
- [New Gemini API updates for Gemini 3 - Google Developers Blog](https://developers.googleblog.com/new-gemini-api-updates-for-gemini-3/)

### Claude Code and MCP Comparison
- [Claude MCP: A New Standard for AI Integration](https://www.walturn.com/insights/claude-mcp-a-new-standard-for-ai-integration)
- [Claude Code Supercharged: Access Any AI Model via MCP Integration](https://lgallardo.com/2025/09/06/claude-code-supercharged-mcp-integration/)
- [Code execution with MCP: Building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp)
- [Codex vs Claude Code: Ultimate 2025 Comparison Guide](https://blog.laozhang.ai/ai-tools/codex-vs-claude-code-2025/)

### Roadmap and Updates
- [Gemini Apps' release updates & improvements](https://gemini.google/release-notes/)
- [Google Workspace Updates: Introducing Gems sharing in the Gemini app](https://workspaceupdates.googleblog.com/2025/09/gem-sharing-gemini-app-workspace.html)
- [Gemini App: 7 updates from Google I/O 2025](https://blog.google/products/gemini/gemini-app-updates-io-2025/)
- [Gemini Drops: New updates to the Gemini app, September 2025](https://blog.google/products/gemini/gemini-drop-september-2025/)
- [Gemini app updates: Deep Research, connected apps, personalization](https://blog.google/products/gemini/new-gemini-app-features-march-2025/)
- [Deep Research and Gems in the Gemini app are now available for more Google Workspace customers](https://workspaceupdates.googleblog.com/2025/03/gemini-gems-deep-research-available-for-more-google-workspace-customers.html)

---

**Report prepared by:** Claude Sonnet 4.5 (Research Agent)
**Date:** December 9, 2025
**Next Review:** March 2026 (quarterly reassessment recommended)
