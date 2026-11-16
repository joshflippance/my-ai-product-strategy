# Three-Horizon Roadmap & Board Pitch

Product: Season Draft for Cottage Book (cottagebook.ca). Owner: Josh Flippance, founder and solo builder.

## Roadmap

### Horizon 1 — Now (0-3 months)
*Quick wins. Ship with existing capabilities.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| **Season Draft beta with 5 co-owned cottages**, using their real wish lists (M1) | 3 of 5 settle a season with 2 or fewer week changes (the kill criteria) | M |
| **Correction capture**: save every draft next to the final schedule and feed "Your call" edits into redrafts (M2 weakest loop, M5 fix) | Override rate falls between a family's first and second draft | H |
| **`lib/ai.ts` and the golden set in CI**: one AI interface with a backup provider, and 27 golden rows gating every release on frontier and mid tiers (M2 kill switch, M4) | 92% golden pass rate, 0 hard-limit breaches shipped, 48-hour provider swap proven | H |

### Horizon 2 — Next (3-9 months)
*Bets. Requires new capabilities or integrations.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| **Outcome pricing live**: 20 CAD per settled season through Stripe, on top of the 48 CAD base plan (M3), alongside Stripe's existing May 2027 launch | Settle rate, and add-on adoption against the 25% estimate | M |

### Horizon 3 — Bet (9-18 months)
*Moonshots. High uncertainty, high potential.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| **Multi-season fairness ledger**: who got which holiday and nights against share carry across years, so leaving means losing the record (M2 defense) | Year-2 retention of co-owned cottages | M |
| **Network intelligence**: anonymous cross-cottage patterns (how holiday clashes settle) set defaults for new cottages, through an aggregate-only function that keeps tenant isolation (M2, M5) | First-draft acceptance for new cottages approaches returning cottages | L |

**Deliberately not on the roadmap yet:** the four red-team fixes (wish-list gaming, stale drafts, lock-in races, code-written note numbers) and receipt photos. The red-team fixes are designed and their golden rows (24 to 27) already block release, so the beta can't ship a draft that fails them; building them is pulled forward only if the beta shows the failure.

## Board Pitch

**Thesis (1 sentence):** Families who co-own a cottage spend hours every spring negotiating the summer in a group chat; Season Draft settles it fairly in one draft, and every season it settles makes the family's fairness record harder to leave.

**The case:**
1. **Why now:** Cottage Book already holds the bookings, branches, shares and shared costs a fair draft needs, and models are now good enough to read a free-text wish list and explain a tradeoff in plain words. Family Cottage, the closest competitor, has the co-owner features but no AI yet, and a free chatbot can already do a rough draft, so the window to own the settled-season record is now.
2. **What's defensible:** the record, not the model. A chatbot can draft a season; only Cottage Book turns it into real bookings under tenant isolation, checks every week against each family's hard limits in code, and keeps the fairness history and corrections that make next season's draft better. Today the moat is thin (flywheel 6/20, Family Cottage 7/20), and Horizon 1 and 3 are aimed at exactly that gap.
3. **The economics:** a settled season costs about 0.60 CAD of AI against 20 CAD of revenue, about 97% gross on the add-on. At 100 cottages with 25 on Season Draft, gross margin moves from 84.5% to 85.7% and revenue per cottage rises about 10%. Even at 3x inference prices the add-on stays above 90% gross. Fixed hosting, not AI, sets the margin.

**The risks:**
1. **Trust / failure modes:** fairness is emotional, and one bad draft can end a family's trust. Mitigations: a code guardrail on every hard limit, per-week confidence (Clear, Close call, Needs your call), no lock-in until the organiser resolves contested weeks, and a 27-row golden set with 7 adversarial cases gating every release.
2. **Scale / governance:** one founder is the on-call, the reviewer and the privacy officer. Governance is written down (autonomy boundaries, escalation triggers, audit cadence, one tightly scoped agent), and Quebec Law 25 applies once Quebec residents join. The shadow AI audit is mostly hypothesis until more families use the product.
3. **Competitive:** Family Cottage could add an AI draft in 6 to 12 months on data it already has, and ChatGPT is free today. The defense only holds if the correction loop and fairness ledger are built before they move.

**The ask:** Approve a 90-day Season Draft beta with 5 co-owned cottages: about 30 hours of build a month and under 50 CAD of AI cost. Continue to outcome pricing in Horizon 2 only if 3 of 5 cottages settle a season with 2 or fewer week changes; otherwise stop and keep Cottage Book a booking calendar.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:** Families who co-own a cottage will accept an AI-drafted summer if it shows every branch's fair share in nights and explains each clash. Cottage Book already tracks branches and shares, so turning a group-chat negotiation into one draft is worth paying for. Kill it if fewer than 3 of 5 cottages adopt the draft.

**Now:** The AI draft itself is the easy part; a free chatbot can do a rough one, so the value is the record around it: a code guardrail families can trust, corrections that compound, and a fairness history that is hard to leave. AI cost is not the risk (about 97% gross on the add-on), so price on the outcome, 20 CAD only when a season settles. The bet is still unproven with real families, so the next 90 days exist to test it against the same kill criteria before building anything bigger.
