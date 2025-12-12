# Registry Agent Development Meeting

## Opening: Setting the Stage

The call began with a practical negotiation of time—two hours in the car, enough space to breathe and explore. The agenda took shape organically, Dave's methodology now internalized by the team.

### Agenda Items

**Shawn:**
- Demo the Registry Assistant MCP
- Utilizing the KOI MCP and Regen Network Ledger MCP in conjunction for accurate data
- Gregory's data reports through KOI GPT (addressing hallucination issues)
- New forum post laying foundations for how KOI works and MCP utilization
- Part two forum post this week: usage instructions and installation approaches

**Darren:**
- YouTube Sensor for KOI
- Processing data in the KOI processor
- Full Stack Engineering Focused MCP Tooling ready for team testing
- Automatic Zoom transcript processing (messages sent to Greg and Dave)
- Getting out of Otter AI and determining next steps

**Gregory:**
- Setting up Claude Code with the MCPs
- Document the GPT connection process
- Registry Assistant Demo
- Knowledge Graph overview and KOI infrastructure

**Dave:**
- Plan for tomorrow's Regen AI Deep Dive promotion
- Second Community Call 2025 Arc for Regen AI
- Check in with Becca on Registry Agent Assistant progress

**Becca:**
- Update naming for KOI
- Support for artifacts and gardening workflows

**Zach:**
- No agenda items (orienting to work in progress and priorities)

## The Promise and Perils of AI Hallucination

The conversation turned to recent explorations with the KOI MCP and the Regen Network ledger MCP working in concert. Gregory had been crafting data reports through the KOI GPT, only to discover it had been hallucinating—conjuring a beautiful fiction of $150 million in eco-credits on-chain, a number more aspirational than actual. The team laughed at the sweetness of the hallucination, momentarily entertaining the fantasy: "Can we just go with that? Let's just make that reality."

This became a playful invocation of what Gaia AI calls "eco-hyperstition"—the collective hallucination of a regenerative future until it manifests into being. But the registry agent, unlike its more creative cousin, had been given clear instructions: rely only on the data at hand, no embellishments, no dreams. Testing would prove whether those instructions held firm.

## Knowledge Foundations and Community Engagement

Shawn had published a new forum post laying the foundations for how KOI works and how the team utilizes it through the MCP framework. A second post was scheduled for the week ahead—usage instructions informed by insights from the econ call and discussions with Gregory and Darren about different installation approaches and practical examples.

The forum posts had generated little engagement so far, no responses yet on either thread. The team acknowledged they could mobilize more strategic outreach if they wanted to amplify reach. For now, the invitation stood: review the posts, ask questions, comment publicly. Plant seeds in the fertile ground of community discourse.

## Infrastructure Development and Integration

Darren shared his updates: a YouTube sensor for KOI now operational, and a reprocessing effort underway for much of the data in the KOI pipeline. The engineering-focused MCP tooling had reached a stage where it could be tested, played with, refined through feedback. It was ready for the world, at least in prototype form.

The question of automatic Zoom transcript processing arose—a different beast entirely. Darren had sent messages to Greg and Dave, noting it remained on his to-do list. He'd explored Otter AI exports, banging his head against what he called "terrible, terrible, terrible software." Five Otter AI recording devices were in the call itself, a small act of defiance: "You hear that, Otter? Your days are numbered."

## Cloud Code Configuration and MCP Servers

Dave had been working through the setup of Cloud Code with the MCP servers, successfully connecting all of them except the registry review MCP, which reported a non-existent directory. Along the way, he'd cleaned up Notion commands, removing extraneous brackets and syntax issues. The process revealed a tension between one-liner installs—elegant, auto-updating—and manual installation routes that offered more reliable control.

Shawn acknowledged both paths would be documented in the upcoming forum post. The one-liner approach would be ideal if they could get it working consistently across different MCPs. Manual installation would remain as a fallback, a proven path through uncertain terrain.

Dave shared his ambition to document his process of connecting the custom GPT to the MCP servers, and potentially extend that work to Gemini Gems. The appeal was clear: Gemini's epic context window made it suited for different use cases, and an internally published Gem could give all team members at Regen access to the full-context, MCP-connected chatbot experience.

## Technical Architecture and Dual Orientations

The registry agent MCP stood apart from its siblings—more complex, more sophisticated, a multi-stage workflow that saved data on the server. It carried a soft requirement for an Anthropic API key to handle processing. This created a natural division in the MCP ecosystem: public-facing tools like the KOI MCP and ledger MCP on one side, and the registry assistant MCP on the other—hosted internally, serving team members like Becca and Giselle who needed specialized functionality.

Two different orientations, Shawn explained, two different sets of constraints and possibilities.

## The Registry Agent Demonstration

Zach joined the call mid-flow, oriented himself to the work in progress and priorities at hand. The agenda crystallized: first, a tour of the registry agent with Shawn; then, time permitting, a journey through the knowledge graph with Darren—a zoom around the structure he'd been gardening, the moving parts and their relationships.

Before diving in, quick check-ins from the team. Dave wanted to confirm the plan for tomorrow's Regen AI deep dive and ensure nothing was needed from their side for promotion. He also wanted to carve out space in the final community call for discussing the 2025 arc, a significant moment for Regen AI. Becca noted the registry assistant work had been slightly delayed due to family matters, and mentioned upcoming naming updates for KOI—a side conversation to schedule with Gregory.

### Accessing the Registry GPT

Shawn shared his screen, opening the Registry GPT connected to the Registry MCP. The agents weren't on the general GPT store but accessible through direct links—a middle path between fully public and fully private. The Regen KOI GPT leaned toward public access, its link shared in recent forum posts. The registry review system remained available only through direct link, which Shawn shared with the team.

The agent connected to a data directory on their server at regen.iai.xyz. Shawn demonstrated the typical entry point: "List sessions." The command surfaced a table of active sessions, test runs, and sessions built from the example PDF directory Becca had provided.

### Understanding Sessions and Workflow

Each session mapped to a project, carrying metadata through an eight-phase workflow that emerged from Zach's story-mapping exercise. Shawn thanked Zach for that work—it had enabled him to ship the first iteration and get it live for testing. The table displayed project names, session IDs, status markers tracking progress through the stages, zero documents uploaded, zero percent coverage for projects still in initialization.

The system revealed some duplication issues—multiple sessions with identical project names at different stages. This might need addressing, but for now, it demonstrated the system's capacity to track multiple project states simultaneously.

### Document Discovery and Upload

Shawn chose to continue with "Test A," a session in initialized state using Soil Carbon methodology v1.2.2. The agent confirmed: stage one complete, moving to stage two—document discovery. The next steps would involve uploading project files: project plans, monitoring reports, deeds, GIS data. The system would automatically discover and classify them.

A nuance emerged: direct document upload through GPT wasn't fully operational yet. Instead, the system posted a link to a custom API on their server. In the future, this could connect directly to Google Drive, leveraging the OAuth work Darren had implemented. For now, users followed the link, selected files, and uploaded them manually.

Shawn selected all the example files from the directory provided, uploaded them, and let the GPT know the upload was complete. The agent gained access to those PDFs and began its extraction process—converting PDFs to markdown on the server, then using the Anthropic API to observe the markdown and extract structured data according to the 23-item checklist that lived in the GPT's root knowledge.

### Methodology and Customization

The checklist was currently fixed, based on specific methodology requirements, but Shawn noted future iterations could make this dynamic. Different verification approaches, different standards, different requirements—all configurable as the system matured.

The agent detected that the files matched an existing session, Test A, which already had documents uploaded and had progressed to stage five: cross-validation. This triggered a deduplication question—should they consolidate the sessions?

### Natural Language Intelligence

Shawn encouraged the team to speak naturally with the agent, noting it had full GPT-4o thinking capabilities at its disposal. He tested this by asking whether the project was duplicated and if they should consolidate sessions. The agent analyzed the situation: one empty placeholder session, one active session with all seven files processed and evidence extracted. Its recommendation: keep only the complete session, delete the initialized duplicate.

"Yes, please," Shawn instructed. "Delete the empty session."

The agent requested permission—any time it would hit the server, it prompted for explicit authorization. Confirmation received, the empty session vanished. The agent recommended proceeding to the next stage: cross-validation.

### The Evidence Matrix

Shawn asked for a table view. The evidence matrix appeared, structured around the 27 requirements from the checklist. Each requirement tracked description, extracted value, source document, page number, section reference, evidence text, and status. Zero items missing. The extraction had been thorough.

Cross-validation would check dates for consistency—low-hanging fruit that Becca had identified as particularly valuable. Manual date-checking was tedious, error-prone, a perfect candidate for automation. The system would also run about five other validation checks, looking for contradictions and inconsistencies in the extracted data.

### Debugging in Real Time

The cross-validation process seemed slower than expected. Shawn wondered aloud whether something might be hanging on the server. These early-stage investigations generated valuable data about system performance and reliability. He considered checking server logs but decided to wait for the response.

The validation completed, but with a curious result: no automated validations were performed. The system found no contradictions or inconsistencies, but it couldn't run structured checks comparing dates or IDs. Human review remained required.

Shawn asked why the checks hadn't run. The agent explained: while text evidence was found for all 23 requirements, the AI extraction hadn't included structured metadata fields. It had pulled text snippets but not standardized key-value data. This pointed to a fault in the data extraction point where they interfaced with the Anthropic API.

Shawn recognized the issue—he'd encountered it during development. They needed to be more explicit that the agent must return a JSON structure. Sometimes it returned unstructured data, which tripped up downstream processes.

## Call Conclusion

Gregory needed to jump to another meeting, and Zoom wouldn't allow him to maintain both calls simultaneously. The demonstration would need to pause, to be continued the next day if time allowed. The team expressed enthusiasm for the progress, excitement for the direction. The work was taking shape, becoming real, moving from hallucination toward implementation.

The call ended with gratitude and anticipation—more to explore, more to build, more to discover in the evolving dance between human expertise and artificial intelligence in service of regenerative systems.
