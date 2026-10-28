# My AI Product Strategy

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS your strategy — version-controlled, board-ready, portable.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [x] | `02-the-moat/` |
| **The Margin** | M3 | [ ] | `03-the-margin/` |
| **The Contract** | M4 | [ ] | `04-the-contract/` |
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

- **Gross Margin (current):**
- **Gross Margin (AI-adjusted):**
- **Pricing Model:**
- **Cascading Strategy:**
- **Break-even at:**

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:**
- **Golden Dataset:** __ rows, __ adversarial
- **Confidence UX:** [approach]
- **HITL Architecture:**
- **Failure Mode Coverage:**

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales — and what compounds.**

- **Compounding System:** [describe feedback loops]
- **Governance Posture:** [approach]
- **Shadow AI Status:** __ tools found, __ triaged
- **Agent Boundaries:**
- **Regulatory Exposure:**

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
