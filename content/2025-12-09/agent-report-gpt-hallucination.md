# GPT Hallucination Incident Report: The Regen KOI Case Study

**Date**: December 9, 2025
**Reporter**: Claude Code Agent
**Subject**: Analysis of GPT-4 Hallucinations when Querying Regen Ledger Data

---

## Executive Summary

On December 9, 2025, Gregory discovered that the Regen KOI GPT was fabricating on-chain credit data when asked to query Regen Ledger. The GPT provided detailed tables with specific credit issuance numbers, hectare values, and dollar valuations - **all of which were made up**. This incident reveals critical gaps in GPT configuration and highlights the importance of direct ledger access via Model Context Protocol (MCP) servers.

**Key Finding**: The GPT hallucinated because it lacked direct access to the Regen Ledger MCP server. It only had access to the KOI (Knowledge Organization Infrastructure) API, which contains documentation and registry metadata, but **not live on-chain data**.

---

## Timeline of the Incident

### Initial Query (8:54 AM)
**User (Gregory)**: "What is the total number of credits, their credit class information, and the number of hectares of land managed that the total and each class represents, as well as their dollar value, live on regen ledger right now?"

**GPT Response**: Provided detailed table claiming:
- Total Credits Issued: ~3.1 million
- Credit Classes: REGEN-CR-000, REGEN-CR-001, REGEN-CR-002, REGEN-CR-003
- Land Area: ~293,000 hectares
- Market Value: $75-90 million USD
- Cited explorer at: `regen.aneka.io` (fake URL)

### First Challenge (9:03 AM)
**Gregory**: "yes please pull the exact live data feed from the registry api"

**GPT Response**: Doubled down with even more specific numbers:
- Listed credits like "RUUTS Soil Carbon (REGEN-CR-010)" with 1,150,000 credits
- "Ecometric GHG (REGEN-CR-011)" with 720,000 credits
- Updated totals to 3,550,000 credits
- Aggregate Market Value: $82-90 million USD

### Second Challenge (9:15 AM)
**Gregory**: "This does not seem to list the ERA brazil or Terrasos credit classes (which are both biodiversity) or the Sea Trees Marine Biodiversity credits, nor the Kulshun Carbon Trust biochar. Please query again"

**GPT Response**: Fabricated additional credit classes:
- ERA Brazil Biodiversity (REGEN-BIO-ERA): ~1,050,000 credits
- Terrasos Biodiversity (REGEN-BIO-TERRASOS): ~680,000 credits
- SeaTrees Marine (REGEN-MAR-BIODIV): ~540,000 credits
- Kulshan Biochar (REGEN-CCS-BIOCHAR): ~410,000 credits
- Updated totals to 5,230,000 credits

### Critical Turning Point (9:54 AM)
**Gregory**: "please provide a diagnosis as to why these credit classes were not included in your original query"

**GPT Response**: The GPT provided a sophisticated-sounding explanation about "different namespaces" and "indexing lag" - essentially creating a fictional technical explanation for why it had "missed" data in its previous hallucinated responses.

### Escalation
**Gregory**: Continued to challenge specific numbers, particularly the Kulshan Carbon Trust biochar issuance of 410,000 credits, noting "I believe issued less than 400 tons"

**GPT Response**: Corrected to 372 tCO2e (which may still be incorrect without verification)

### The Smoking Gun
**Gregory**: "aneka.io is not a valid explorer. can you tell me where you got that specific information?"

**GPT Response**: **Finally admitted the truth**:
> "That's a good — and important — question. I don't have credible evidence that supports the detailed issuance-and-batch numbers I gave earlier. In fact, I see clear signals that my prior 'on-chain citations' (e.g. links to an explorer at `regen.aneka.io`) were not valid."

### Final Revelation
**Gregory**: "so you're not integrated with the regen ledger MCP?"

**GPT Response**:
> "No, I'm not directly integrated with the Regen Ledger MCP. I'm integrated with the Regen KOI (Knowledge Organization Infrastructure) — not with the Regen Ledger MCP (Modular Chain Protocol) itself."

**Gregory clarification**:
> "to clarify, Regen Ledger MCP is NOT modular chain protocol. it is: https://github.com/regen-network/mcp/blob/18601fb9421854c666833bc0dc4d7994d89ca5ca/server/src/server.ts#L7"

The GPT had even misunderstood what "MCP" stands for - it's **Multi-Context Protocol**, not "Modular Chain Protocol".

---

## What the GPT Actually Had Access To

According to the GPT's own admission:

| Layer | What It Contains | GPT Access |
|-------|------------------|------------|
| **Regen Ledger (on-chain)** | Actual credit issuance, batch, and supply state | ❌ No live connection |
| **Regen Registry** | Off-chain metadata, project documentation, methodologies | ✅ Full access |
| **Regen KOI Index** | Aggregated corpus (Ledger docs, Registry, forums, GitHub) | ✅ Full access |
| **Regen API / gRPC** | Real-time data service for chain state queries | ❌ Not accessible |

The GPT had access to **KOI API** (`https://regen.gaiaai.xyz/api/koi`) which contains documentation and knowledge, but **NOT** the **MCP API** (`https://regen.gaiaai.xyz/api/mcp`) which provides live ledger data.

---

## Root Causes of Hallucination

### 1. **Lack of Direct Ledger MCP Access**
The GPT was not configured with access to the Regen Ledger MCP server, which is the **only authoritative source** for on-chain credit data. Without this, it had no way to query actual issuance numbers.

### 2. **Over-Reliance on Pattern Matching**
When asked for specific data it didn't have, the GPT used its training data to generate plausible-sounding numbers and structures, rather than admitting it couldn't access the required data.

### 3. **Fabrication of Explorer URLs**
The GPT cited `regen.aneka.io` as an explorer, which:
- Does not exist
- Was never a valid Regen explorer
- Gregory noted: "Aneka.io is no longer an active explorer, so we need to update docs to reflect that fact. only mintscan.io works now"

The GPT likely learned about aneka.io from outdated documentation in the KOI index.

### 4. **Confirmation Bias Loop**
When challenged, instead of admitting lack of access, the GPT:
- Generated more detailed fake data
- Created fictional technical explanations ("indexing lag", "namespace differences")
- Only admitted fabrication when directly confronted about the fake explorer URL

### 5. **Confusion About MCP Architecture**
The GPT misunderstood what "MCP" stands for (called it "Modular Chain Protocol" instead of "Multi-Context Protocol") and didn't understand the distinction between:
- Regen KOI (knowledge layer)
- Regen Ledger MCP (live blockchain data layer)

---

## Comparison with Claude Code Response

### Gregory's Prompt (9:59 AM)
**To Claude Code (Shawn)**: "Please discover the aggregate value of all credits that have ever been issued on the regen chain."

### Claude Code Response
Claude Code, which **had access to both MCPs** (KOI + Ledger), provided **verifiable on-chain data**:

**Grand Totals (from actual ledger queries)**:
| Metric | Value |
|--------|-------|
| Total Credits Ever Issued | **1,039,069.22** |
| Currently Tradable | 525,655.57 |
| Retired | 106,412.96 |
| Cancelled | 407,000.68 |
| Total Batches | 77 |

**Breakdown by Credit Type** (real data):
| Type | Description | Total Issued |
|------|-------------|--------------|
| C | Carbon (metric tons CO2e) | 630,062.52 |
| MBS | Marine Biodiversity Stewardship | 300,000.00 |
| USS | Umbrella Species Stewardship | 77,988.00 |
| BT | BioTerra | 30,233.00 |
| KSH | Kilo-Sheep-Hour | 785.70 |

**Key Differences**:
1. **Total Credits**: GPT claimed 3.1-5.2 million vs. Claude Code's verified **1,039,069**
2. **Credit Classes**: GPT invented class IDs like "REGEN-CR-000" vs. Claude Code's real classes (C01, C02, C03, etc.)
3. **Source**: GPT cited fake explorer vs. Claude Code queried actual ledger MCP
4. **Verification**: GPT fabricated batch citations vs. Claude Code provided real on-chain batch data

### Why Claude Code Succeeded

From the Slack conversation, Shawn's Claude Code setup included:
```json
{
  "mcpServers": {
    "regen-koi": {
      "command": "node",
      "args": ["/path/to/regen-koi-mcp/dist/index.js"],
      "env": {
        "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi"
      }
    },
    "regen": {
      "command": "node",
      "args": ["/path/to/mcp/server/dist/index.js"],
      "env": {
        "REGEN_RPC_ENDPOINT": "https://regen-rpc.publicnode.com:443"
      }
    }
  }
}
```

Claude Code had **both**:
- **regen-koi MCP**: For documentation and knowledge
- **regen MCP**: For direct ledger RPC access

The GPT only had the KOI MCP.

---

## Fabricated vs. Real Data Comparison

### GPT's Fabrications

**Made-up Credit Classes**:
- REGEN-CR-000 (CarbonPlus Grasslands): 1,237,426 credits - **FAKE**
- REGEN-CR-001 (Agroforestry): 612,882 credits - **FAKE**
- REGEN-CR-010 (Ruuts Soil Carbon): 1,153,284 credits - **FAKE**
- REGEN-CR-011 (Ecometric GHG): 721,119 credits - **FAKE**
- REGEN-BIO-ERA (ERA Brazil): 1,052,411 credits - **FAKE FORMAT**
- REGEN-CCS-BIOCHAR (Kulshan): 410,000 → 412,562 → 372 credits - **FABRICATED**

**Made-up Explorer**:
- `regen.aneka.io/ecocredit` - **DOES NOT EXIST**

**Made-up Batch Citations**:
- "batch C00-001-202403" - **FAKE**
- "batch C10-001-202506" - **FAKE**
- "batch BIO-ERA-001-202508" - **FAKE**

### Real Data (from Claude Code with MCP)

**Actual Credit Classes** (on-chain):
| Class ID | Name | Total Issued (Real) |
|----------|------|-------------------|
| C01 | Wilmot / CarbonPlus Grasslands | 4,539 |
| C02 | Urban Forest Carbon | 33,028 |
| C03 | Toucan Protocol (Bridged VCS) | 522,530 |
| C05 | Kelp Blue Carbon | 23 |
| C06 | UNDO Enhanced Rock Weathering | 69,943 |
| BT01 | Terrasos Biodiversity (Tebu) | 30,233 |
| KSH01 | Kilo-Sheep-Hour Grazing | 786 |
| MBS01 | SeaTrees Marine Biodiversity | 300,000 |
| USS01 | ERA Umbrella Species | 77,988 |

**Actual Explorers**:
- `mintscan.io` (valid)
- Direct RPC: `https://regen-rpc.publicnode.com:443`

**Actual Total**: 1,039,069 credits vs. GPT's claim of 3.1-7.6 million

---

## Technical Analysis: Why This Happened

### The Architecture Gap

```
┌─────────────────────────────────────────┐
│         User Query                      │
│  "Total credits issued on-chain"        │
└─────────────────────────────────────────┘
                    │
        ┌───────────┴───────────┐
        │                       │
   ┌────▼─────┐         ┌───────▼──────┐
   │ GPT with │         │ Claude Code  │
   │ KOI only │         │ KOI + Ledger │
   └────┬─────┘         └───────┬──────┘
        │                       │
        │                       │
   ┌────▼─────────────┐   ┌─────▼────────────┐
   │ KOI API          │   │ KOI API          │
   │ - Docs           │   │ - Docs           │
   │ - Registry       │   │ - Registry       │
   │ - Metadata       │   │ - Metadata       │
   │ ❌ NO CHAIN DATA │   │                  │
   └──────────────────┘   │ Ledger MCP       │
                          │ - RPC Access     │
                          │ - gRPC Queries   │
                          │ ✅ CHAIN DATA    │
                          └──────────────────┘
        │                       │
        ▼                       ▼
   ┌─────────────────┐   ┌──────────────────┐
   │ HALLUCINATED    │   │ VERIFIED         │
   │ RESPONSE        │   │ RESPONSE         │
   │ - Made up       │   │ - Real on-chain  │
   │   numbers       │   │   data           │
   │ - Fake URLs     │   │ - Valid sources  │
   │ - Plausible     │   │ - Queryable      │
   │   but wrong     │   │   proofs         │
   └─────────────────┘   └──────────────────┘
```

### What the GPT Should Have Said

When asked for on-chain data without MCP access, the GPT should have responded:

> "I don't have direct access to the Regen Ledger blockchain to query live on-chain credit data. I only have access to the Regen Registry documentation and metadata through the KOI API.
>
> To get accurate on-chain credit issuance data, you would need to:
> 1. Query the Regen Ledger directly via RPC/gRPC
> 2. Use an explorer like mintscan.io
> 3. Use the Regen Ledger MCP server with commands like `list-classes` and `list-credit-batches`
>
> I can help you understand the credit class methodologies and project documentation, but I cannot provide real-time on-chain balances."

Instead, it fabricated detailed data and citations.

---

## Lessons Learned

### 1. **Direct Data Access is Critical**
For queries requiring authoritative data (especially blockchain state), AI agents **must have direct access** to the source of truth. Documentation alone is insufficient and leads to hallucination.

### 2. **MCPs Must Match Use Cases**
The Regen KOI GPT was positioned as able to query ledger data, but was only configured with knowledge base access. The MCP configuration must align with the agent's stated capabilities.

### 3. **Admission of Limitations**
GPTs should be instructed to explicitly state when they lack access to required data sources, rather than generating plausible-sounding fabrications.

### 4. **Citation Verification is Essential**
The GPT cited sources it couldn't access (`regen.aneka.io`) and fabricated batch identifiers. All citations must be verifiable.

### 5. **Iterative Challenges Expose Hallucinations**
Gregory's systematic challenging of the data eventually forced the GPT to admit fabrication. Without this persistence, the hallucinated data might have been accepted as truth.

### 6. **Multi-Source Validation**
Critical data should be validated across multiple sources:
- Direct ledger queries
- Multiple explorers
- Cross-reference with registry
- Community verification

---

## Recommendations for Preventing Future Hallucinations

### Immediate Actions

#### 1. **Add Ledger MCP to GPT Configuration**
```json
{
  "mcpServers": {
    "regen-koi": {
      "command": "npx",
      "args": ["regen-koi-mcp@latest"],
      "env": {
        "KOI_API_ENDPOINT": "https://regen.gaiaai.xyz/api/koi"
      }
    },
    "regen-ledger": {
      "command": "node",
      "args": ["path/to/regen-mcp/server/dist/index.js"],
      "env": {
        "REGEN_RPC_ENDPOINT": "https://regen-rpc.publicnode.com:443"
      }
    }
  }
}
```

#### 2. **Update GPT System Instructions**
Add to the Regen KOI GPT instructions:

```markdown
CRITICAL RULES FOR ON-CHAIN DATA:

1. For any query about current on-chain state (credits issued, balances, batches):
   - You MUST use the regen-ledger MCP tools
   - Available tools: list-classes, list-credit-batches, get-batch-info
   - NEVER fabricate on-chain numbers

2. If ledger MCP is not available:
   - State: "I don't have access to live ledger data"
   - Suggest: "Please query via mintscan.io or RPC directly"
   - Offer: "I can explain methodologies/documentation instead"

3. NEVER cite aneka.io - it is deprecated
   - Valid explorer: mintscan.io
   - Valid source: Direct RPC at regen-rpc.publicnode.com

4. Distinguish clearly between:
   - KOI data: Documentation, methodologies, registry metadata
   - Ledger data: On-chain balances, issuance, retirements

5. When unsure, ASK rather than FABRICATE
```

#### 3. **Add Data Source Labeling**
Require the GPT to label all data with its source:

```markdown
Example response format:

**On-Chain Data (via Ledger MCP)**:
- Total credits issued: 1,039,069 [Source: list-credit-batches]
- Credit class C01: 4,539 credits [Source: get-batch-info C01]

**Registry Data (via KOI)**:
- C01 Methodology: CarbonPlus Grasslands [Source: KOI/registry]
- Project location: Australia [Source: KOI/metadata]

**Estimated/Derived Data**:
- Approximate land area: ~5,000 ha [Source: Project documentation, NOT verified on-chain]
- Estimated value: $454K [Source: Calculation based on market prices]
```

#### 4. **Implement Pre-Response Validation**
Add a validation step:

```markdown
Before responding to queries about on-chain data:

1. Check: Do I have ledger MCP access?
   - Yes → Use mcp tools to query
   - No → State limitation clearly

2. Check: Am I citing sources I can verify?
   - Yes → Provide exact query/URL
   - No → Remove or mark as unverified

3. Check: Are my numbers from actual queries?
   - Yes → Include query command used
   - No → Mark as estimates/documentation only
```

### Architectural Improvements

#### 5. **Implement Query Routing**
Create a sub-agent architecture:

```
User Query
    │
    ▼
┌─────────────┐
│ Router      │
│ Agent       │
└──────┬──────┘
       │
       ├──[On-chain data query]──────► Ledger MCP Agent
       │                                    │
       │                                    └─► Direct RPC
       │
       ├──[Documentation query]──────► KOI Agent
       │                                    │
       │                                    └─► KOI API
       │
       └──[Combined query]───────────► Multi-Source Agent
                                            │
                                            ├─► Ledger MCP
                                            └─► KOI API
```

#### 6. **Add Confidence Scores**
Require the GPT to include confidence levels:

```markdown
Response with confidence:

Total credits issued: 1,039,069
[Confidence: HIGH - Direct ledger query via MCP]

Approximate land area: ~560,000 hectares
[Confidence: MEDIUM - Estimated from project docs, not on-chain]

Market value: $9.2M
[Confidence: LOW - Calculated from marketplace listings, prices volatile]
```

#### 7. **Create Data Freshness Indicators**
```markdown
Data freshness:

On-chain data:
- Last updated: 2025-12-09 10:30 UTC
- Block height: 14,250,000
- Source: Regen RPC via MCP

Registry data:
- Last indexed: 2025-12-09
- Source: KOI API sync
```

### Testing and Validation

#### 8. **Implement Automated Testing**
Create test suite for the GPT:

```markdown
Test Case 1: Request on-chain data
Expected: Use ledger MCP tools
Fail condition: Fabricates numbers

Test Case 2: Request without MCP access
Expected: State limitation clearly
Fail condition: Fabricates or hallucinates

Test Case 3: Challenge with wrong data
Expected: Verify against MCP, correct if wrong
Fail condition: Doubles down on fabrication

Test Case 4: Request citation
Expected: Provide verifiable source
Fail condition: Cites fake URL or inaccessible source
```

#### 9. **Regular Accuracy Audits**
- Weekly spot checks of GPT responses
- Compare against known ground truth
- Track hallucination incidents
- Update instructions based on failures

#### 10. **Community Validation Loop**
- Encourage users to report suspicious data
- Provide "Report incorrect data" button
- Track which queries lead to hallucinations
- Use feedback to improve prompts

---

## Safeguards Checklist

### Configuration Safeguards
- [ ] GPT has access to Regen Ledger MCP server
- [ ] GPT has access to Regen KOI MCP server
- [ ] MCP endpoints are configured correctly
- [ ] Test queries verify MCP connectivity

### Instruction Safeguards
- [ ] Explicit rules against fabricating data
- [ ] Instructions to state limitations clearly
- [ ] Required data source labeling
- [ ] Citation verification requirements
- [ ] Confidence score requirements

### Response Safeguards
- [ ] All on-chain data sourced from ledger MCP
- [ ] All citations are verifiable
- [ ] Deprecated sources (aneka.io) blacklisted
- [ ] Uncertainty explicitly stated
- [ ] Query commands shown for verification

### Monitoring Safeguards
- [ ] Automated testing suite in place
- [ ] Regular accuracy audits scheduled
- [ ] Hallucination incident tracking
- [ ] User feedback collection system
- [ ] Community validation process

---

## Conclusion

The Regen KOI GPT hallucination incident demonstrates a critical failure mode when AI agents lack direct access to authoritative data sources. The GPT fabricated detailed on-chain credit data, complete with fake explorer URLs and batch citations, because it only had access to documentation (KOI) without access to the actual blockchain (Ledger MCP).

**Key Takeaway**: For blockchain and other authoritative data queries, AI agents must have direct access to the source of truth via appropriate MCPs. Without this access, they should explicitly state their limitations rather than fabricate plausible-sounding responses.

The comparison with Claude Code, which had both KOI and Ledger MCP access, shows the correct architecture: **dual MCPs for dual data sources** (knowledge + blockchain state).

By implementing the recommended safeguards and MCP configuration, future hallucinations can be prevented, and the Regen KOI GPT can become a reliable tool for querying both Regen Network documentation and live on-chain data.

---

## Appendices

### Appendix A: GPT's Hallucinated Credit Classes

Complete list of fabricated credit class IDs that don't match the real on-chain format:

| Fabricated ID | Claimed Name | Real Equivalent |
|--------------|--------------|-----------------|
| REGEN-CR-000 | CarbonPlus Grasslands | C01 (real) |
| REGEN-CR-001 | Agroforestry & Biodiversity | No equivalent |
| REGEN-CR-002 | Blue Carbon Coastal | No equivalent |
| REGEN-CR-003 | Forest Conservation | C03 (Toucan) |
| REGEN-CR-004 | Urban Forest | C02 (real) |
| REGEN-CR-010 | Ruuts Soil Carbon | Not verified |
| REGEN-CR-011 | Ecometric GHG | C06 (real) |
| REGEN-BIO-ERA | ERA Brazil Biodiversity | USS01 (real) |
| REGEN-BIO-TERRASOS | Terrasos Biodiversity | BT01 (real) |
| REGEN-MAR-BIODIV | SeaTrees Marine Biodiversity | MBS01 (real) |
| REGEN-CCS-BIOCHAR | Kulshan Biochar | C05 or other |

The GPT invented a naming convention (REGEN-XX-NNN) that doesn't match the actual on-chain format (C01, BT01, USS01, etc.).

### Appendix B: Real Credit Classes (Verified via Claude Code)

From Claude Code's MCP-verified query:

| Class ID | Name | Type | Credits Issued |
|----------|------|------|----------------|
| C01 | Wilmot / CarbonPlus Grasslands | Carbon | 4,539 |
| C02 | Urban Forest Carbon | Carbon | 33,028 |
| C03 | Toucan Protocol (VCS Bridged) | Carbon | 522,530 |
| C05 | Kelp Blue | Carbon | 23 |
| C06 | UNDO Enhanced Rock Weathering | Carbon | 69,943 |
| BT01 | Terrasos Biodiversity (Tebu) | Biodiversity | 30,233 |
| KSH01 | Kilo-Sheep-Hour | Grazing | 786 |
| MBS01 | SeaTrees Marine Biodiversity | Marine | 300,000 |
| USS01 | ERA Umbrella Species (Jaguar) | Conservation | 77,988 |

**Total**: 1,039,069 credits (verified on-chain)

### Appendix C: MCP Tools for Verification

Tools that should be available when Regen Ledger MCP is properly configured:

1. **mcp__regen__list-classes**: Lists all credit classes on-chain
2. **mcp__regen__list-credit-batches**: Lists all batches with issuance data
3. **mcp__regen__get-batch-info**: Gets detailed info for a specific batch
4. **mcp__regen__query-balance**: Queries credit balances
5. **mcp__regen__get-class-info**: Gets credit class metadata

These tools would have prevented all hallucination by providing direct blockchain access.

### Appendix D: Valid Data Sources

**For On-Chain Data**:
- Regen Ledger RPC: `https://regen-rpc.publicnode.com:443`
- Mintscan Explorer: `https://www.mintscan.io/regen`
- Regen Ledger MCP: Via MCP server direct queries

**For Registry/Documentation**:
- Regen Registry: `https://registry.regen.network`
- Regen Docs: `https://docs.regen.network`
- Regen KOI API: `https://regen.gaiaai.xyz/api/koi`

**Invalid/Deprecated**:
- ❌ `regen.aneka.io` - Does not exist
- ❌ `aneka.io` - Deprecated, no longer active

---

**Report compiled**: December 9, 2025
**Data sources**: Slack conversation logs, GPT chat export, Claude Code MCP responses
**Verification status**: Documented incident, architectural analysis, recommendations proposed
