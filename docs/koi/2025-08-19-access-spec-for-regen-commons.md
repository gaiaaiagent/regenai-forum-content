# Permissions and Access Specification for Regen Knowledge Commons

**Summary:** This document defines how knowledge is shared and protected within the Regen Knowledge Commons, ensuring the right people (and agents) have appropriate access. It outlines purpose, access levels, roles (human and AI), implementation methods, and safeguards. **This is a living draft** meant for the internal Regen team and close collaborators, evolving as we refine our knowledge-sharing practices in line with Regen’s mission of collaborative ecological regeneration.

## Purpose

The Regen Knowledge Commons is being established as a repository of collective intelligence to support our work in ecological regeneration. The purpose of this specification is to clearly define who can access what knowledge within this Commons and how that access is managed. By segmenting content into tiers (internal, community, public) and enforcing role-based permissions, we aim to **foster open collaboration while protecting sensitive information**. This framework will enable seamless sharing of knowledge with those who need it, without compromising confidential data. It also sets expectations for AI systems in the Commons, ensuring that human and AI agents handle information responsibly. *(Context:* Regen is actively upgrading its community “Commons” with AI to boost governance and knowledge exchange making a robust access policy timely.)

## Knowledge Access Levels

All content in the Knowledge Commons will be categorized into one of three access levels, indicating its audience and degree of confidentiality:

- **Internal Knowledge** – For RND PBC core team and trusted collaborators with specific permissions granted only. This includes sensitive strategy documents, in-progress research, internal meeting notes, and any data not ready to share broadly. Internal content is restricted to authorized internal users and approved AI agents. It remains hidden from the wider community and public. *Goal:* Enable frank internal communication and early-stage idea development in a private space, with the intent that some of this knowledge may later be refined for broader sharing.
- **Community Knowledge** – For the broader Regen community (Codified into Regen Commons members) (e.g. partners, network members, and vetted contributors). This includes resources like how-to guides, governance proposals, community call notes, and knowledge-share posts that are not strictly internal but still intended for within the Regen network. Community-level content requires login or membership to access. It can be contributed to by community members (with moderation) and is visible to all logged-in community participants, but **not indexed or publicly searchable** on the open web. *Goal:* Empower the Regen community with a rich knowledge base to learn from each other and coordinate, while maintaining a semi-private space for candid exchange.
- **Public Knowledge** – Openly accessible to anyone. This includes published articles, public research reports, blog posts, documentation, and any knowledge asset we deliberately share with the general public. Public content carries no access restrictions – it can be indexed by search engines and cited widely. *Goal:* Advance Regen’s mission and values by sharing knowledge with the world, demonstrating transparency, and inviting broader engagement in ecological regeneration.

Each knowledge asset will be tagged with its access level metadata upon creation. These tags determine its visibility and distribution. **Content can be re-tagged to a wider audience (e.g. internal -> public) once approved** for release, but not the reverse without special permission (to prevent information from being improperly “closed off” after being open). This tiered model balances openness with necessary confidentiality, ensuring that sensitive information is only seen by appropriate groups until it’s ready for public disclosure.

## Roles and Agent Access (Human and AI)

Access to the Knowledge Commons is governed by roles for both human users and AI agents. We outline distinct roles and their permissions:

- **Internal Team (Human)** – Regen staff and key collaborators have the broadest access. They can read *all*knowledge levels (internal, community, public) and contribute content at all levels. For instance, an internal member can create or edit internal documents, participate in community forums, and publish public-facing knowledge. They also have authority to tag content with the appropriate access level. Some internal team members (admins or knowledge managers) may have additional privileges to manage user access and oversee content curation.
- **Community Members (Human)** – Registered members of the Regen community (such as partners, project developers, or participants in Regen’s network) can access **community-level and public knowledge**. They typically cannot see internal-only content. Community members are encouraged to contribute to community knowledge: e.g. posting in community forums, adding to shared docs, or suggesting edits to knowledge base articles. However, their contributions are limited to the community space unless invited to collaborate on internal content. Community contributors may have varying roles (e.g. some might be *Community Editors* with rights to organize content). All community contributions are subject to moderation to ensure quality and security.
- **Public Users (Human)** – Any person on the internet can view public knowledge content without logging in. They have read-only access to public articles, docs, and data. They cannot see community or internal content, nor can they contribute directly (aside from public feedback channels if provided). If a public user wants to contribute, they would need to become an approved community member through the appropriate onboarding process.
- **Internal AI Agents** – AI systems operating on behalf of the Regen internal team (for example, an AI assistant that helps with proposal writing or internal project management). These agents are treated as privileged “users” with an internal-level role, but their access is **carefully scoped and audited**. An internal AI agent may read internal and community knowledge bases as needed to fulfill its tasks (e.g. aggregating data for a draft report), but it is **prohibited from exposing internal content to unauthorized parties**. Such agents operate only in approved environments (e.g. an internal chat or document system) where their outputs remain internal. They must authenticate just like a user, using API keys or credentials tied to an internal role, so that standard access controls apply to their queries. *Example:* A proposal-writing AI assistant (internal agent) can retrieve data from internal research files and community project posts to assemble a draft proposal, but if asked a question by a user without clearance, it will refuse to reveal internal details.
- **External-facing AI Agents** – AI assistants that interact with community members or the public (for example, a bot on the community forum, or a “registry assistant” helping users navigate Regen’s public registry). These agents are assigned the minimum access necessary for their function. By default, an external agent only has access to **public knowledge** (and possibly community knowledge if it is designed for community-only use and the user interacting with it is authenticated as such). They do not have access to internal knowledge. This ensures that an AI answering questions on a public channel cannot inadvertently leak internal information – it literally will not possess that information. If an agent serves the community forum, it might be granted community-level read access (so it can reference community discussions or documentation in responses to logged-in community members), but it will still treat internal content as off-limits. All responses from external agents are additionally filtered to avoid revealing any sensitive data. *Example:* A “Regen Registry Assistant” bot could guide a new user on how to register a project by referencing public registry documentation and community FAQs, but it would not have the ability to pull from internal strategy memos.

**Role-Based Permissions:** Our system uses role-based access control (RBAC) rules to enforce these distinctions. Each user or agent is associated with a role that has specific permissions (e.g. the ability to read certain knowledge levels and/or contribute content). We distinguish between **read access** (viewing content) and **contribute access** (creating or editing content) for each knowledge level. For instance, internal team members have contribute rights for internal and community knowledge bases, whereas a general community member might have read access to most community content but limited contribute rights (perhaps only in certain areas or needing approval). Public users have read access to public content only, and no contribute rights. These granular controls ensure that, for example, **only authorized persons can modify an internal knowledge document**, and that community-contributed content can be sandboxed or reviewed before elevation to broader levels.

## Implementation Approach

To technically implement these permissions and ensure smooth knowledge flow, we will employ several strategies:

- **Tagged Content and Metadata:** Every knowledge asset (document, post, dataset, etc.) will carry a metadata tag indicating its access level (Internal, Community, or Public). This tagging is the cornerstone of our access control. Content repositories and databases will enforce rules based on these tags. For example, an internal wiki page tagged “Internal” will only surface to logged-in internal roles. If the same page is later approved for public release, switching its tag to “Public” will automatically make it visible externally. Consistent tagging will also guide AI behavior – e.g. an AI indexer will know which sections of its index are permissible to show to a given user.
- **APIs and Access Control Layers:** The knowledge commons will be accessible through controlled APIs and application interfaces that check permissions on each request. When a user or AI agent queries the Commons (e.g. searching for a topic or requesting a document), the system will verify their identity and role, then **filter results** to include only content they are allowed to see. This will be implemented via middleware that examines the content’s access tag against the requester’s role. We will leverage existing frameworks for role-based content gating (similar to how enterprise knowledge bases restrict articles based on user groups[brainscape.com](https://www.brainscape.com/flashcards/udemy-practice-test-1-missed-questions-12800437/packs/21244325#:~:text=Read%20access%20determines%20the%20ability,articles%20in%20a%20knowledge%20base)). Additionally, separate API endpoints or keys might be used for internal vs. external contexts. For example, an internal agent calling an “internal search API” must present an internal credential, whereas the public website only uses public endpoints. This separation helps prevent any accidental leakage across the boundaries.
- **Indexing and Search Bots:** A robust search function is essential for the Commons, but it must respect content levels. We plan to deploy custom **indexing bots** that crawl and index knowledge content for search and discovery, under strict constraints. There may be distinct indexers for internal and community content versus public content. *Internal indexers* will build a full index of internal + community + public knowledge, but that index will only be accessible to authenticated internal users/agents. A *public indexer* will index only public-tagged content and power the public search portal. By dividing indexing in this way, we ensure, for example, that a community-only forum post doesn’t appear in public search results. These bots will be configured to read the metadata tags and abide by them. Moreover, all indexing activity will be logged (who/what indexed which document and when) for audit purposes. We will also mark internal/community pages with `noindex` for external search engines, ensuring that Google or other web crawlers cannot index restricted content.
- **Audit Trails and Monitoring:** Implementation will include an auditing system that logs access events – especially for internal content. Every time an internal document is accessed or queried (whether by a human user or an AI agent), the system will record who/what accessed it, when, and for what purpose (where feasible). These logs will be reviewed periodically to detect any anomalies or potential permission misuses. For instance, if an external-facing agent somehow attempts to query internal content, the request would be blocked and flagged in the audit log for investigation. Audit trails create accountability and help refine the access rules over time. We’ll treat AI agent activity with the same level of scrutiny as human activity. If an internal AI agent is summarizing a confidential report, its usage of that report will be logged, and if it tries to output that summary in a public channel, that would be caught by filters (as described below) and logged as well.
- **Secure APIs & Tokens:** We will enforce that all access to the knowledge stores (especially internal/community content) happens over secure channels with proper authentication (e.g. OAuth tokens or API keys tied to roles). No direct public URLs will expose internal content. Even internally, access will be through services that check permissions. This reduces the chance of someone bypassing controls. For AI agents, each agent will have a unique identifier and token with only the permissions it requires – implementing the principle of least privilege. For example, the proposal-writing AI might have read-access to internal research docs but not to HR documents, if not needed.

Through this multi-pronged approach (tagging + RBAC + controlled indexing + auditing), we create a robust infrastructure where knowledge is **discoverable to those who should see it and invisible to those who should not**. It lays the groundwork for scaling our Commons safely as both our human team and AI agents rely on it.

## Privacy and Security Considerations

Protecting privacy and ensuring security are paramount in managing the Knowledge Commons. We incorporate several guardrails, filters, and consent mechanisms:

- **Content Guardrails:** Sensitive information (such as personal data, financial details, or security-sensitive data) will reside only in **Internal** knowledge stores by default, which already limits exposure. Beyond access control, we will implement guardrails within tools and AI systems that handle this content. For example, **AI assistants will be programmed not to divulge personal or sensitive details** even if they have access to them. Prompting and instruction tuning will include explicit policies (e.g. “If content is tagged internal or contains XYZ, do not include it in responses to external queries”). Similarly, internal documents may have additional protections like watermarks or warnings reminding users of their confidentiality.
- **Automated Filters:** We will use automated filters to scan content and outputs for sensitive data. Before any knowledge is published to a broader audience, an automated check (and/or human review) will remove or mask private information (such as individual names, contact info, or location of endangered species sites, etc., depending on context). For AI agent outputs, we’ll implement an output filter layer: even if an internal AI agent is allowed to access raw internal data to do analysis, when it generates a report or answer, that output can be scanned. If it detects an internal-only fact being presented in a channel that is visible to community or public, the system will either block it or redact those parts. These filters ensure **no accidental leakage** of restricted knowledge. On the input side, if an external user asks an AI agent a question that would require internal knowledge to answer, the agent should safely respond that it cannot provide that information, rather than even hinting at internal content.
- **Consent and Contributor Privacy:** We respect the rights and comfort of those who contribute to our Commons. This means:
    - **Human Contributors:** When internal or community members add knowledge (documents, forum posts, data), we will obtain their consent regarding how that content might be used or shared. For example, an internal researcher contributing a draft report knows it’s internal; if later we think about making it public, we will seek permission and review for any sensitive parts. Similarly, community contributors will be informed which of their contributions remain within the community versus which might be highlighted publicly. We will also allow contributors to request removal or reclassification of content they provided if circumstances change (subject to a review process).
    - **Use of Personal Data:** Any personal identifying information (PII) included in the knowledge commons (say a case study including names of farmers, or user profiles) will be handled according to privacy best practices. That might mean anonymizing certain data before moving a piece of content from internal to public, or aggregating information.
    - **AI Training Data:** If we use the knowledge commons content to train AI models or inform AI agents, we will do so with caution and consent. Internal content used for AI will remain within the model’s scope only for internal usage (and we’ll avoid using any private data to train models that operate publicly). Community content would typically be opt-in for AI usage – e.g. we might have a disclaimer that posts on the forum could be used to improve an AI assistant that helps the community, giving users a chance to object or opt out.
- **Security Measures:** The Commons infrastructure will adhere to strong security practices: encrypted connections (TLS) for all data transfer, encryption at rest for the databases especially for internal content, regular security audits, and access logs as noted. User accounts (for humans and AI agents) will have secure authentication (potentially multi-factor for admins). We will also implement authorization checks in depth – not just at the front door, but at every layer where data is fetched or processed. Regular permission audits will be done to remove accounts that no longer need access (for example, if a collaborator’s project ends, their account is downgraded or removed).
- **Human Review and Moderation:** As advanced as our AI and automation will be, human oversight remains critical. A designated **Knowledge Steward** or committee may be appointed to oversee the health of the Commons. They will handle edge cases and sensitive decisions, such as: approving content to move from internal to public, reviewing logs for suspicious behavior, and updating policies as needed. This ensures there is always a human-in-the-loop for accountability and ethical judgment, especially in gray areas that automated rules might not cover.

By combining these privacy and security measures, we aim to **build trust**: team members trust that internal brainstorming won’t leak, community members trust that their semi-private discussions stay in the community, and everyone trusts that public knowledge is shared intentionally and safely. These guardrails also protect Regen’s integrity and reputation by preventing misinformation or unauthorized disclosures.

## Open Questions and Future Considerations

While this specification lays out a clear framework, some questions remain open for discussion as we implement the Knowledge Commons:

- **Optimal Role Granularity:** What is the right level of granularity for roles? We’ve outlined broad categories (Internal, Community, Public, plus perhaps sub-roles like admin or editor). We need to decide if additional roles are necessary. For example, within the internal team, do we need a distinction between “Core Team” vs. “Advisors” with slightly different access? Within community, do we designate certain trusted members as moderators or content curators with elevated privileges? We must also plan how roles can evolve (e.g. a community member becoming an internal collaborator on a specific project – can we easily grant them temporary internal access for that project?). This leads into how flexible and dynamic our access control system is. The question is open on how to implement *role-based access* in a way that’s both secure and not too cumbersome in practice.
- **Contributor Onboarding & Training:** As we invite more people (staff or community) to contribute to the knowledge commons, how do we onboard them so they understand and follow these policies? We may need to create a contributor guide or training covering: how to tag content correctly, what not to post in a public channel, how to handle sensitive information, etc. New internal team members should be briefed on confidentiality protocols for internal knowledge. Community contributors might have to agree to certain guidelines (perhaps a lightweight contributor agreement). Also, should we have an *approval workflow* for new content? For instance, a community-contributed article might require review by an internal moderator before it appears to others. We need to balance openness (making it easy to contribute) with quality control and security (ensuring contributions don’t accidentally violate rules). This is an ongoing area to refine – starting perhaps with strict moderation, then gradually opening as trust and community capacity grows.
- **AI Agent Participation and Governance:** As AI agents become more integrated (some acting as authors or editors in the Commons), how do we govern their behavior long-term? We’ve set rules for what they can access and output, but open questions include: How do we verify an agent is consistently following rules (e.g. if it’s an evolving AI model)? Do we allow community members to deploy their own agents in the Commons eventually (and if so, how to sandbox those)? How do we handle content generated by AI – does it require a human review stamp before being considered “approved” knowledge? We might consider an **“AI usage policy”** appended to this document as the ecosystem grows.
- **Evolution of Access Levels:** Will we always have just the three levels (Internal, Community, Public)? It seems likely but we might later identify a need for sub-categories (for example, “Regen Team Only” vs “Partners” within internal). Also, as more knowledge becomes mature, we hope to graduate a lot of it to Public to benefit the larger movement. We should keep evaluating if the balance of what’s internal vs public is right, or if we can push more knowledge outward over time. This touches on aligning with Regen’s open ethos – ultimately, **knowledge should flow to where it can do the most good**, so we will revisit these boundaries periodically.
- **Integration with Regen’s Governance:** Since Regen is a community-governed network, an open question is how much the community gets to influence or co-govern the Knowledge Commons rules. For now, this document is internally set. In the future, should we have a community-elected committee or use the $REGEN token governance process to ratify certain policies (especially around public knowledge)? This ties into the AI governance as well – making sure any major changes to how knowledge is managed has stakeholder input.

***Note:*** *This Permissions and Access Specification is a living document.* We will update it as we answer the questions above and as real-world use of the Commons reveals new needs. All team members and collaborators are encouraged to provide feedback. By iteratively improving these guidelines, we aim to build a Knowledge Commons that is secure, inclusive, and truly empowering for Regen’s mission.

# Permissions and Access Specification for Regen Knowledge Commons (WIP) V 2

**Summary:**

This document defines how knowledge is shared and protected within the Regen Knowledge Commons, ensuring humans and AI agents have the right access. It introduces a pragmatic framework to foster open collaboration, protect sensitive data, and mitigate risks associated with AI agents (notably the “lethal trifecta” of private data access, untrusted inputs, and external communication).

This is a **living draft** for Regen-aligned organizations and close collaborators. It is not limited to RND PBC. Any discrete org in the ecosystem — such as Regen Foundation, Gaia AI, Ecometric, or future partners — should be able to adopt and implement these controls internally, while interoperating with the broader Commons. The design principle is: **each org can manage its own interior space and permissions with ease, while contributing to the shared Commons responsibly.**

---

## Purpose

The Regen Knowledge Commons is a shared repository of collective intelligence for ecological regeneration. Each participating organization retains sovereignty over its internal/private space, while contributing to community and public layers. Access controls must:

- Enable **collaboration** across the Regen ecosystem,
- Respect each org’s **internal confidentiality needs**, and
- Provide **transparent, trustworthy sharing** with the public.

This balances openness with security, and ensures that Commons participation is not RND-specific but available to all aligned orgs.

---

## Knowledge Access Levels

Knowledge assets are classified and tagged at creation:

1. **Internal** – For an organization’s private workspace (e.g., RND PBC strategy docs, Regen Foundation research drafts, Gaia AI experiments). Restricted to staff and trusted collaborators.
2. **Community** – Shared within the Regen Commons (partners, contributors, network members). Semi-private; not indexed by search engines.
3. **Public** – Fully open knowledge (articles, reports, docs) intentionally released for global access.

**Flow principle:** Content may move **Internal → Community → Public** once approved. Reverse movement (closing knowledge) requires explicit exception.

---

## Roles and Agent Access

### Human Roles

- **Internal Team (Org-specific)** – Staff and collaborators of a given org (e.g., RND PBC, Regen Foundation). Full read/write for their own Internal + Community + Public.
- **Community Members** – Registered members of Regen Commons. Access to Community + Public.
- **Public Users** – Open read-only access to Public knowledge.

### AI Agents

- **Internal Agents** – Scoped to an org’s Internal + Community space. No raw external egress; may only emit structured *intents* to the Membrane Agent.
- **External Agents** – Scoped to Public (+ Community if authenticated). May communicate externally but never access Internal.
- **Membrane Agent** – A shared gateway pattern for all orgs. It mediates external communication, applies policy checks, sanitizes untrusted inputs, enforces allowlists, and ensures human review where needed.

---

## Anti-Trifecta Principle

No single agent may combine:

1. **Access to internal/private data**,
2. **Exposure to untrusted inputs**, and
3. **Unrestricted external communication**.

This is enforced across all orgs:

- Internal agents = Internal data, no direct egress.
- External agents = External comms + untrusted inputs, no Internal data.
- Membrane = mediates between them, with audits and safeguards.

This pattern applies equally to RND PBC, Regen Foundation, Gaia AI, Ecometric, or any other participant.

---

## Implementation Approach

- **Tagged Metadata:** Every org tags content as Internal/Community/Public.
- **RBAC:** Applied at API and database levels per org.
- **Membrane Gateway:** Shared design, but each org may run its own Membrane instance for outbound traffic.
- **Logging & Audits:** All agent actions logged; payload hashes and destinations recorded.
- **Filters & Redaction:** Sensitive content flagged before release.
- **Human Oversight:** High-stakes outbound communications require explicit human approval.

---

## On-Chain Integration (DAO DAO & Registry)

- **DAO DAO:** Provides transparent, community-governed provenance of roles across orgs.
- **Regen Registry:** Anchors wallet-based identity and registry-linked permissions.
- **RBAC Sync:** Maps on-chain roles into off-chain Commons permissions for each org.

**Design spec:**

- On-chain = provenance and legitimacy of who holds roles.
- Off-chain = enforcement of fine-grained access (per org’s documents, indexes, AI agents).

Each org can adopt this hybrid without heavy infrastructure — using DAO DAO for governance legitimacy, while running lightweight local enforcement.

---

## Privacy and Security

- **Org-specific confidentiality:** Each participating org controls its own Internal space.
- **Consent:** Contributors consent to how their contributions may move from Internal → Public.
- **Untrusted Inputs:** All public/community content treated as untrusted; sanitized before ingestion.
- **Agent Safeguards:** Structured intents only; no shared indexes across orgs; outbound actions gated by membranes.
- **Audit Trails:** Logs reviewed across orgs for accountability.

---

## Open Questions

- How to standardize the minimum viable Membrane Agent spec across orgs?
- What balance of on-chain vs. off-chain control works best for cross-org governance?
- How to allow orgs to extend roles flexibly (e.g., Regen Foundation adding “Fellow” vs. RND adding “Advisor”)?
- Should Commons governance eventually set shared baseline rules, with orgs customizing their interior implementation?
