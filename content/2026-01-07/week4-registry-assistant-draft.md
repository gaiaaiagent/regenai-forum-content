# The Registry Assistant: From Hours to Minutes

![Registry Assistant Workflow|690x400](upload://registry-assistant-workflow.png)

# [Week 4/12] Regen AI Update: The Registry Assistant - January 7, 2026

* **Posted by:** Shawn Anderson (Gaia AI)
* **Key Focus:** How AI transforms 6-8 hour registry reviews into 60-90 minute guided workflows

---

## Quickstart

**Try the Registry Assistant:**

| Platform | Access | Time |
|----------|--------|------|
| **ChatGPT** | [Registry Review Assistant GPT →](https://chatgpt.com/g/g-6928c53496ac8191bd6b3b93a1f266c6-registry-review-assistant) | Instant |
| **Claude Code** | Connect to Registry MCP (internal) | Setup required |
| **Eliza** | [Run locally](https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar) | 5 minutes |

**Demo:** [Loom walkthrough →](https://www.loom.com/share/53284fd4cf984447b8758e8d615418eb)

---

## From Verification to Process

Last week, we confronted the dark side of AI assistance: **ecohyperstition**—the generation of plausible-sounding ecological data that dissolves under verification. We showed how multi-MCP architecture prevents hallucination by routing queries to authoritative data sources.

But verification is only half the story.

The regenerative economy doesn't just need AI that *tells the truth*. It needs AI that *does the work*—the painstaking, methodical work of reviewing project documentation, cross-referencing evidence, and ensuring that every credit issued represents real ecological impact.

This is the domain of the **Registry Review Agent**.

---

## The Problem: Registry Review at Scale

Registry review is essential. Every carbon credit, every biodiversity unit, every ecosystem service token on Regen Ledger passes through a compliance review process:

- **Completeness checks**: Are all required documents present?
- **Evidence cross-validation**: Does the ownership claim match the deed?
- **Technical verification**: Do sampling methods meet methodology requirements?
- **Temporal alignment**: Are monitoring dates consistent with imagery dates?

A single project review can take 6-8 hours of focused work. That's 6-8 hours per project, per review cycle. With dozens of projects in the pipeline and limited staff, the bottleneck isn't expertise—it's time.

The traditional response to scaling challenges is hiring. But throwing bodies at the problem has limits:

1. **Training overhead**: New reviewers need months to internalize methodology requirements
2. **Consistency variance**: Different reviewers apply standards differently
3. **Knowledge siloing**: Expertise concentrates in individuals rather than systems
4. **Cost scaling**: Linear headcount growth for linear throughput growth

What if we could **amplify** human expertise rather than just parallelize it?

---

## The Registry Assistant: Anatomy of an Intelligent Workflow

The Registry Review Assistant isn't a black box that produces verdicts. It's a **guided workflow system** that handles the mechanical while preserving human judgment for what matters.

### The Seven Stages

```
┌─────────────────────────────────────────────────────────────────────┐
│                    REGISTRY REVIEW WORKFLOW                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  1. INITIALIZATION                                                  │
│     └─ Create session, select methodology/credit class             │
│                        ↓                                            │
│  2. DOCUMENT DISCOVERY                                              │
│     └─ Scan folder, normalize files, group by type                 │
│                        ↓                                            │
│  3. REQUIREMENTS MAPPING                                            │
│     └─ Load checklist, match documents to requirements             │
│                        ↓                                            │
│  4. COMPLETENESS CHECK                                              │
│     └─ Flag missing items, verify presence of evidence             │
│                        ↓                                            │
│  5. EVIDENCE EXTRACTION                                             │
│     └─ Locate cited sections, extract relevant passages            │
│                        ↓                                            │
│  6. CROSS-VALIDATION                                                │
│     └─ Compare claims across documents, flag inconsistencies       │
│                        ↓                                            │
│  7. REPORT GENERATION                                               │
│     └─ Produce structured report with citations and flags          │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

Let's walk through each stage with examples from actual review sessions.

---

## Stage 1: Initialization

Every review begins with context. The assistant needs to know:

- **Which methodology** is this project registered under?
- **Which credit class** will credits be issued to?
- **What checklist** should guide the review?

```
> list sessions

| Session ID | Project Name | Status | Stage | Documents | Coverage |
|------------|--------------|--------|-------|-----------|----------|
| botany-farm-001 | Botany Farm Soil Carbon | complete | report | 12 | 94% |
| terrasos-pilot-002 | Terrasos Biodiversity | in_progress | extraction | 8 | 72% |
| test-a | Test Session | initialized | discovery | 0 | 0% |

> start new session "kulshan-carbon-2026"
New review session created: kulshan-carbon-2026
Please upload your documents or provide a folder link.
```

The initialization stage sets the regulatory context. Different methodologies have different requirements—soil carbon projects need sampling plans and lab analyses; biodiversity projects need species surveys and habitat assessments. The assistant loads the appropriate checklist template.

---

## Stage 2: Document Discovery

Once documents are uploaded, the assistant scans and organizes them:

```
> generate upload link

Upload link: https://registry.regen.gaiaai.xyz/upload/kulshan-carbon-2026
Files uploaded will be processed and indexed automatically.

[After upload]

Discovered 8 documents:
├── Project_Plan_v2.1.pdf (89 pages)
├── Monitoring_Report_2025.pdf (45 pages)
├── Sampling_Plan_Final.docx (12 pages)
├── Lab_Results_SOC.xlsx (3 sheets)
├── Title_Deed_County.pdf (4 pages)
├── GIS_Boundary_Files.zip (shapefile)
├── Additionality_Assessment.pdf (8 pages)
└── Photos_Field_Visit.zip (47 images)

Processing: Converting to searchable format...
```

The assistant converts PDFs to searchable text, extracts tables from spreadsheets, and indexes everything for semantic search. This mechanical work—previously requiring manual file organization—happens in seconds.

---

## Stage 3: Requirements Mapping

Here's where the checklist meets the evidence. The assistant attempts to match each requirement to a supporting document:

```
Requirements Mapping for: CarbonPlus Grasslands v1.1

| # | Requirement | Status | Mapped Document | Confidence |
|---|-------------|--------|-----------------|------------|
| 1 | Project boundary definition | ✅ Mapped | GIS_Boundary_Files.zip | 0.95 |
| 2 | Land tenure documentation | ✅ Mapped | Title_Deed_County.pdf | 0.92 |
| 3 | Baseline SOC measurement | ✅ Mapped | Lab_Results_SOC.xlsx | 0.88 |
| 4 | Sampling methodology | ✅ Mapped | Sampling_Plan_Final.docx | 0.91 |
| 5 | Additionality demonstration | ✅ Mapped | Additionality_Assessment.pdf | 0.85 |
| 6 | Leakage assessment | ⚠️ Low confidence | Project_Plan_v2.1.pdf (p.67) | 0.43 |
| 7 | Buffer pool contribution | ❌ Not found | - | - |
| 8 | Permanence commitment | ⚠️ Low confidence | Project_Plan_v2.1.pdf (p.12) | 0.51 |

Items requiring attention: 3
Would you like to review the flagged items?
```

**This is a decision point.** The assistant surfaces uncertainty; the human reviewer decides how to proceed. The 0.43 confidence on "leakage assessment" might mean:
- The document exists but uses different terminology
- The section is buried in an unexpected location
- The requirement is genuinely unmet

Only a human can determine which.

---

## Stage 4: Completeness Check

The completeness check produces a structured assessment:

```
Completeness Assessment: kulshan-carbon-2026

REGISTRY REQUIREMENTS (from Program Guide v1.1):

✅ COMPLETE (5/8):
  - Land tenure documented (Title_Deed_County.pdf)
  - Project boundary defined (GIS_Boundary_Files.zip)
  - Baseline established (Lab_Results_SOC.xlsx)
  - Sampling methodology documented (Sampling_Plan_Final.docx)
  - Additionality demonstrated (Additionality_Assessment.pdf)

⚠️ NEEDS REVIEW (2/8):
  - Leakage assessment: Found in Project_Plan but section unclear
  - Permanence commitment: Duration mentioned but terms ambiguous

❌ MISSING (1/8):
  - Buffer pool contribution: No documentation found

Recommendation: Request clarification on items 6, 7, 8 before proceeding.
```

---

## Stage 5: Evidence Extraction

For requirements that map to documents, the assistant extracts the relevant evidence:

```
Evidence Extraction: Land Tenure (Requirement #2)

Source: Title_Deed_County.pdf
Pages: 1-2

Extracted Claims:
┌────────────────────────────────────────────────────────────────────┐
│ Property: 240.5 acres, Parcel #KSH-2024-0847                       │
│ Owner: Kulshan Carbon Trust LLC                                     │
│ Recorded: March 15, 2024                                           │
│ County: Whatcom, Washington                                        │
│ Legal Description: Section 14, Township 39N, Range 4E...           │
└────────────────────────────────────────────────────────────────────┘

Cross-reference check:
  Project_Plan_v2.1.pdf (p.4): "Kulshan Carbon Trust owns 240 acres..."
  ✅ Acreage matches (within 0.5 acre tolerance)
  ✅ Entity name matches
  ✅ Location consistent
```

Evidence extraction is where the assistant shines. Finding the exact page and section where evidence lives—across 150+ pages of documentation—used to require meticulous manual searching. Now it's automatic.

---

## Stage 6: Cross-Validation

Cross-validation catches inconsistencies that single-document review might miss:

```
Cross-Validation Report: kulshan-carbon-2026

CONSISTENCY CHECKS:

1. Ownership Claims
   Project Plan: "Kulshan Carbon Trust LLC"
   Title Deed: "Kulshan Carbon Trust LLC"
   ✅ CONSISTENT

2. Project Area
   Project Plan: 240 acres
   GIS Boundary: 240.47 acres
   Title Deed: 240.5 acres
   ✅ CONSISTENT (within tolerance)

3. Baseline Period
   Project Plan: "January 2024 - December 2024"
   Sampling Plan: "Q1 2024"
   Lab Results: Sample dates: 2024-02-15 to 2024-03-22
   ⚠️ CLARIFICATION NEEDED: Plan says "January" but sampling started February

4. SOC Measurements
   Lab Results: Average 3.2% SOC
   Monitoring Report: References "3.2% baseline SOC"
   ✅ CONSISTENT

INCONSISTENCIES FOUND: 1
CLARIFICATIONS NEEDED: 1
```

---

## Stage 7: Report Generation

The final output is a structured review report:

```
═══════════════════════════════════════════════════════════════════════
              REGISTRY REVIEW REPORT: kulshan-carbon-2026
═══════════════════════════════════════════════════════════════════════

Project: Kulshan Carbon Trust Biochar
Methodology: CarbonPlus Grasslands v1.1
Credit Class: C05 (Biochar Carbon Removal)
Review Date: 2026-01-07
Status: CONDITIONAL APPROVAL

───────────────────────────────────────────────────────────────────────
SUMMARY
───────────────────────────────────────────────────────────────────────

Completeness: 87.5% (7/8 requirements documented)
Cross-validation: 1 inconsistency, 1 clarification needed
Recommendation: Approve pending resolution of flagged items

───────────────────────────────────────────────────────────────────────
REQUIREMENTS CHECKLIST
───────────────────────────────────────────────────────────────────────

[Detailed checklist with citations...]

───────────────────────────────────────────────────────────────────────
ACTION ITEMS
───────────────────────────────────────────────────────────────────────

1. Request buffer pool contribution documentation
2. Clarify baseline period discrepancy (January vs February start)
3. Verify permanence commitment terms

───────────────────────────────────────────────────────────────────────
CITATIONS
───────────────────────────────────────────────────────────────────────

All claims in this report are traced to source documents:
  [1] Project_Plan_v2.1.pdf, page 4, section 2.1
  [2] Title_Deed_County.pdf, page 1
  [3] Lab_Results_SOC.xlsx, Sheet "Summary"
  ...
```

---

## The Transformation: 6-8 Hours → 60-90 Minutes

| Task | Manual Time | With Assistant | Savings |
|------|-------------|----------------|---------|
| Document organization | 45-60 min | 2 min | 96% |
| Requirements mapping | 90-120 min | 10 min | 91% |
| Evidence location | 120-180 min | 15 min | 91% |
| Cross-validation | 60-90 min | 10 min | 85% |
| Report drafting | 60-90 min | 5 min | 94% |
| **Human review & judgment** | 60-90 min | **60-90 min** | 0% |
| **Total** | **6-8 hours** | **~90 min** | ~80% |

The key insight: **automation handles the mechanical; humans handle judgment**.

The assistant doesn't decide whether a project should be approved. It surfaces the evidence, flags the inconsistencies, and presents the information in a structured format. The registry agent—the human expert—makes the call.

---

## Agent Archetypes: Specialized Intelligence

The Registry Assistant isn't a generic AI. It embodies domain expertise through **agent archetypes**—specialized personalities trained on specific knowledge domains:

### Becca (Registry)

*The compliance specialist.* Becca knows the Program Guide inside and out. She understands what constitutes sufficient evidence, which documents satisfy which requirements, and where project proponents commonly fall short.

**Use Becca for:**
- First-pass completeness checks
- Requirements mapping
- Identifying missing documentation

### Gregory (Methodology)

*The technical expert.* Gregory specializes in methodology specifications—sampling protocols, uncertainty quantification, baseline calculations. He understands the science behind the standards.

**Use Gregory for:**
- Technical verification
- Sampling plan review
- GHG accounting validation

### Marie (Full-Stack)

*The integration specialist.* Marie bridges knowledge and blockchain. She can verify on-chain state against documented claims, ensuring that credits reflect actual registered projects.

**Use Marie for:**
- Cross-referencing registry and ledger
- Verifying issuance claims
- Tracing credit provenance

These archetypes represent different **contexts**—not different models. The same underlying AI operates with different system prompts, tool access, and knowledge bases depending on the task.

---

## Technical Architecture

The Registry Assistant runs on the same MCP architecture as the KOI and Ledger tools:

```
┌─────────────────────────────────────────────────────────────────────┐
│                   REGISTRY REVIEW MCP STACK                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌─────────────────────┐    ┌─────────────────────┐                │
│  │  ChatGPT / Claude   │    │    Eliza Agent      │                │
│  │  (User Interface)   │    │  (Autonomous)       │                │
│  └──────────┬──────────┘    └──────────┬──────────┘                │
│             │                          │                            │
│             └──────────┬───────────────┘                            │
│                        │                                            │
│                        ▼                                            │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │              Registry Review MCP Server                      │   │
│  │  github.com/gaiaaiagent/regen-registry-review-mcp           │   │
│  ├─────────────────────────────────────────────────────────────┤   │
│  │  Tools:                                                      │   │
│  │    - list_sessions      - start_session                     │   │
│  │    - upload_documents   - map_requirements                  │   │
│  │    - extract_evidence   - cross_validate                    │   │
│  │    - generate_report    - get_status                        │   │
│  └─────────────────────────────────────────────────────────────┘   │
│                        │                                            │
│                        ▼                                            │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                    Data Layer                                │   │
│  │  - Document storage (local/S3/Google Drive)                 │   │
│  │  - Session state (JSON/YAML)                                │   │
│  │  - Checklist templates (YAML)                               │   │
│  │  - Report outputs (JSON/PDF)                                │   │
│  └─────────────────────────────────────────────────────────────┘   │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

The current implementation stores data locally on the server. Future iterations will integrate directly with Google Drive and SharePoint, allowing reviewers to work with documents where they already live.

---

## Human-in-the-Loop: Where AI Stops

The Registry Assistant is designed with explicit boundaries:

**AI Handles:**
- Document parsing and indexing
- Text extraction and search
- Pattern matching against checklists
- Cross-document comparison
- Report formatting

**Humans Handle:**
- Approval/rejection decisions
- Interpretation of ambiguous evidence
- Edge case judgment
- Stakeholder communication
- Final accountability

This isn't a limitation—it's the design. Ecological credit markets require **auditable human accountability**. Every credit issued should trace to a human decision, informed by structured evidence, documented in verifiable reports.

The AI amplifies human capability without replacing human responsibility.

---

## What Becca's Feedback Told Us

[TODO: Add specific feedback from Becca about the Registry Assistant - what's working, what needs improvement, specific examples from real reviews]

---

## Discussion Questions

1. **What review tasks consume most of your time?** Where would automation help most?

2. **How do you currently track evidence across documents?** What tools do you use?

3. **What makes a review "complete" in your workflow?** What standards do you apply?

4. **Would you trust AI-extracted evidence?** What verification would you want?

---

## Looking Ahead: Week 5 Preview

Next week, we explore the **Prospective Developer Support Agent**—the front-line resource for incoming inquiries from project and methodology developers:

- Handling newcomer vs. experienced developer inquiries
- Adaptive guidance based on user context
- Capturing market intelligence from conversation patterns
- Escalation pathways for strategic opportunities

We'll also begin the conversation about **agent memory**: how do we ensure that knowledge gained in one review session benefits future reviews?

---

## Resources

**Registry Assistant:**
- [Registry Review Assistant GPT](https://chatgpt.com/g/g-6928c53496ac8191bd6b3b93a1f266c6-registry-review-assistant) — Try it now
- [Registry Review MCP](https://github.com/gaiaaiagent/regen-registry-review-mcp) — Source code
- [Eliza Agent](https://github.com/gaiaaiagent/GAIA/tree/regen-assistant-avatar) — Autonomous version
- [Demo Video](https://www.loom.com/share/53284fd4cf984447b8758e8d615418eb) — Walkthrough

**Related MCPs:**
- [Regen KOI MCP](https://github.com/gaiaaiagent/regen-koi-mcp) — Knowledge search
- [Regen Python MCP](https://github.com/gaiaaiagent/regen-python-mcp) — Blockchain queries

**Documentation:**
- [Program Guide](https://registry.regen.network/program-guide) — Registry requirements
- [Credit Classes](https://registry.regen.network/credit-classes) — Methodology specifications
- [Previous Posts](https://forum.regen.network/t/regen-ai-update-connecting-to-regen-mcps/562) — Week 3

---

*This is the fourth of 12 weekly updates on Regen AI development. The Registry Assistant transforms how we verify ecological claims—not by replacing human expertise, but by amplifying it.*

*The difference between ecohyperstition and regenerative intelligence is verification. The difference between verification and action is workflow.*
