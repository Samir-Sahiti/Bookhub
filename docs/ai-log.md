# 🤖 AI Development Log — VibeReads

This log tracks all meaningful AI tool usage across the project lifecycle.
Each entry covers what was built, which tools were used, the prompts that worked,
the quality of output, and an honest estimate of time saved.

---

## Entry #1 — Sprint 1: Product Foundation

**Period:** March 23–27, 2026
**Authors:** Samir Sahiti, Fisnik Percuku, Yllka Nuredini

---

### 1. Competitive Analysis

**Tool:** Claude (claude.ai)
**Task:** Map the competitive landscape — Goodreads, StoryGraph, Literal, and The StoryGraph vs our platform positioning.

**Prompt used:**
> "We're building a book discovery platform with AI-powered vibe search, reading clubs, a writer publishing hub, reading challenges, and mood profiles. Our main competitor is Goodreads. Do a thorough competitive analysis covering: core features, search capability, community features, AI usage, and key weaknesses. Present it as a comparison table, then write a paragraph on the gap we're targeting."

**Output quality:** 4/5 — the comparison table was accurate and well-structured. The gap analysis aligned closely with what we already believed, which validated our direction rather than surprising us. Minor issue: Claude slightly overstated StoryGraph's AI capabilities, which we corrected manually.

**Time saved:** ~3 hours (researching, reading, and writing this manually would have taken most of a day across the team).

---

### 2. Product Definition Document (PRD first draft)

**Tool:** Claude (claude.ai)
**Task:** Draft the problem statement, solution overview, target users, and Jobs-to-be-Done sections of the project plan.

**Prompt used:**
> "Here is our product idea: a modern book discovery and community platform. Our core innovation is vibe-based semantic search — users type a mood or plot description and get AI-matched results. Secondary features include reading clubs, writer publishing, reading challenges, and mood profiles. Write a full product definition document covering: the problem with current platforms (focus on Goodreads), our solution with a bullet-point feature list, three user segments (primary, secondary, tertiary), and a Jobs-to-be-Done framework for the primary user."

**Iteration:** We ran two follow-up prompts to expand the writer hub and mood profile sections after the instructor's feedback that we should develop the platform beyond just search.

**Output quality:** 4.5/5 — the initial draft was production-ready with minor edits. The JTBD framing was particularly strong and saved significant PM time. We refined the tone and added specific technical details (pgvector, SignalR, RabbitMQ) manually.

**Time saved:** ~4 hours. Writing a document this detailed from scratch would have been a full afternoon.

---

### 3. User Story Writing

**Tool:** Claude (claude.ai)
**Task:** Draft all 13 user stories with acceptance criteria and edge cases for the product backlog.

**Prompt used:**
> "Write 10 user stories for a book discovery platform in this format: As a [persona], I want to [action], so that [outcome]. For each story include: priority (Must Have / Should Have / Could Have), two acceptance criteria in Given/When/Then format, and notes on edge cases. Cover these stories: vibe search, book results page, book detail page, register & login, submit a review, reading list, AI review moderation, live activity feed, create a reading club, and club reading feed. Be specific — reference the tech stack where relevant: pgvector, SignalR, RabbitMQ, Keycloak, TanStack Query."

**Iteration:** After the pitch feedback, we used Claude to add 3 additional stories for the new features — writer publishing hub, reading challenges, and mood profiles — using the same format and referencing the existing stories for consistency.

**Output quality:** 4/5 — acceptance criteria were detailed and technically accurate. Some edge cases were generic and required manual sharpening (e.g. the Keycloak token refresh scenario in US-004 was added by us, not Claude). Story numbering and backlog summary table were generated cleanly.

**Time saved:** ~5 hours across the team. Writing 13 detailed stories with two acceptance criteria each from scratch would have been a significant chunk of Sprint 1.

---

### 4. Wireframe Generation

**Tool:** Figma AI (Make) + v0.dev (component references)
**Task:** Generate initial wireframe layouts for the 8 required screens.

**Approach:** Used Figma Make to generate rough layout suggestions for each screen, then manually refined proportions, component placement, and flow. v0.dev was used separately to explore component ideas for the vibe search input and the book card design — not as direct output but as visual reference.

**Screens generated with AI assistance:**
- US-001: Vibe search homepage (empty state + results state)
- US-003: Book detail page
- US-009: Reading club dashboard

**Screens done manually (AI used only for reference):**
- US-005: Review submission form
- US-006: Reading list
- US-008: Challenge discovery page
- US-010: Writer publishing hub
- US-011: Mood profile builder

**Output quality:** 3.5/5 — Figma AI is useful for rough structure but the layouts required significant manual cleanup. Proportions were off on mobile views and component hierarchy needed rethinking. Most valuable as a starting point, not a final output.

**Time saved:** ~2 hours on the three AI-assisted screens. The manual screens took approximately 45 minutes each.

---

### 5. OKR Drafting

**Tool:** Claude (claude.ai)
**Task:** Draft Q2 OKRs for the platform aligned with our North Star metric (Weekly Active Reviewers).

**Prompt used:**
> "We're building a book discovery platform launching in June 2026. Our North Star metric is Weekly Active Reviewers. Draft Q2 OKRs with one Objective and 4 Key Results. The KRs should cover: registered users, reviews submitted, reading club activity, and writer hub engagement. Make them ambitious but achievable for a student project team of 3 over 12 weeks."

**Output quality:** 4/5 — the KR numbers were well-reasoned and the framing was clean. We adjusted KR3 (active clubs from 30 to 50) and added KR4 for challenge enrollments manually after team discussion.

**Time saved:** ~1 hour.

---

### Summary Statistics — Entry #1

| Metric | Value |
|---|---|
| Total AI interactions | 9 (including follow-up prompts) |
| Tools used | Claude (primary), Figma AI, v0.dev |
| Estimated hours saved | ~15 hours across the team |
| Highest-value use | User story writing + PRD drafting |
| Lowest-value use | Wireframe generation (required heavy manual cleanup) |

**Top prompting insight from this sprint:**
Specificity is everything. Prompts that referenced our actual tech stack (pgvector, SignalR, RabbitMQ, Keycloak) produced far more useful output than generic prompts. When Claude knows the constraints, the output fits the architecture rather than describing a generic SaaS app.

---

*Next entry: Sprint 2–4 (Frontend MVP — component scaffolding, Zod schemas, Playwright tests)*
