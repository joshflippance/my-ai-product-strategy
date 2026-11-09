# My AI Product Strategy

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS your strategy — version-controlled, board-ready, portable.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [x] | `02-the-moat/` |
| **The Margin** | M3 | [x] | `03-the-margin/` |
| **The Contract** | M4 | [x] | `04-the-contract/` |
| **The Guardrails** | M5 | [ ] | `05-the-guardrails/` |
| **The Pitch** | M6 | [ ] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Season Draft for Cottage Book: AI drafts a co-owned cottage's summer from each branch's wish list and share, with hard limits checked in code
- **AI Value Archetype:** Oracle
- **Vulnerability Scores:** Moat 2/5 · Data 2/5 · Platform 3/5
- **Top Risk:** A free chatbot can draft the season, so the value must come from the guardrail, fairness history and the calendar it lands in
- **Confidence:** M
- **Prototype:** [Season Draft](https://claude.ai/artifact/W67a6fskoYcuErZ2vFydV5)
- **Kill Criteria:** Fewer than 3 of 5 real co-owned cottages adopt the draft with 2 or fewer week changes, or a draft breaks a stated hard limit without the guardrail catching it

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

**Moat summary:** The moat is the record, not the model. Season Draft scores 6/20 against Family Cottage's 7/20; they lead on joined-up domain data, and neither captures corrections. Winning means building the Correction loop first: every draft stored against the family's final schedule, so next season starts from last year. The model is swappable (Partial today, 48-hour ready once `lib/ai.ts`, failover and the golden set ship).

- **Data Flywheel Score:** 6/20
- **Weakest Loop:** Correction (draft edits aren't captured yet)
- **Competitive Position:** Axes are AI drafting depth and co-ownership model depth. Cottage Book is ahead on AI drafting; Family Cottage is ahead on joined-up co-ownership data (bookings, fairness, expenses, documents).
- **Encroachment Defense:** Own the record, not the draft: capture every edit so next season starts from last year, and land drafts as real bookings with the guardrail and cost ledger
- **Vendor Portability:** Partial (single file, no adapter, fallback or eval yet)

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** 84.5% (100 cottages at 48 CAD a year, 62 CAD fixed hosting a month)
- **Gross Margin (AI-adjusted):** 85.7% overall; the Season Draft add-on itself about 97%
- **Pricing Model:** Hybrid, penetration priced: 4 CAD a month base plus an outcome-based 20 CAD per settled season, charged only when the draft is locked in as bookings
- **Cascading Strategy:** Small tier reads limits and triages, mid writes explanations and the family note, frontier drafts the season; 80% / 20% cascade, blended 0.025 CAD a request
- **Break-even at:** Gross break-even at 16 paying cottages (62 CAD fixed hosting / 4 CAD a month); each Season Draft season covers its own AI cost about 33 times over

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** 92% golden-set pass rate (band 90 to 95), zero hard-limit breaches shipped, hallucination <1%, first draft p95 <45 s
- **Golden Dataset:** 27 rows, 7 adversarial (v1 target about 150); rule judge in CI plus LLM rubric, run on both frontier and mid tiers
- **Confidence UX:** Tiered per week (Clear / Close call / Needs your call); guardrail breaches and contested weeks block lock-in until the organiser decides; reasoning, override, adjustable threshold and saved corrections
- **HITL Architecture:** Weeks under 50% confidence or breaking a hard limit go to the organiser as "Needs your call"; the season can't lock until resolved; choices become corrections and golden rows
- **Failure Mode Coverage:** 18 failure modes listed, all with a test or control defined; red team found wish-list gaming, stale drafts, lock-in races and misleading note numbers (fixes designed, not built)

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales — and what compounds.**

- **Compounding System:** Three learning loops designed, none active yet (recursive learning missing, cross-domain broken, network missing); fails the 3-month freeze test today. Fix: use corrections within the season, monthly golden rows, anonymous cross-cottage patterns
- **Governance Posture:** AI drafts and tags on its own; locking in, sending and charging need the owner or organiser; shares, roles, bookings and merges are never automatic. Audits every PR, weekly, monthly and quarterly
- **Shadow AI Status:** __ tools found, __ triaged
- **Agent Boundaries:** One agent (weekly feedback triage): reads feedback, writes verdicts, opens a PR, never merges. Season Draft is a single call, not an agent
- **Regulatory Exposure:** PIPEDA (Quebec Law 25 if Quebec members); EU AI Act minimal risk, only if EU residents join

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):**
- **Horizon 2 (Next):**
- **Horizon 3 (Bet):**
- **Board Narrative:** [1-sentence thesis]
- **Key Metric:**

→ Details: [`06-the-pitch/`](06-the-pitch/)
