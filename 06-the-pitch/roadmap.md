# Three-Horizon Roadmap & Board Pitch

Product: Season Draft for Cottage Book (cottagebook.ca). Owner: Josh Flippance, founder and solo builder.

## Roadmap

### Horizon 1 — Now (0-3 months)
*Quick wins. Ship with existing capabilities.*

Revised after the AI Bet Evaluator (2.5/5): the bet has no outside evidence yet, so Horizon 1 exists to get it before building more.

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| **Recruit 5 named co-owned cottages** from the Eels Lake launch and offer codes, and interview each about how they settled last summer | 5 cottages confirmed by name by 31 January 2027, each agreeing to the 20 CAD price if the season settles | M |
| **Season Draft beta with correction capture** in the spring 2027 planning window: every draft saved next to the final schedule, "Your call" edits fed into redrafts (M1 bet, M2 weakest loop) | Settle rate: 3 of 5 lock in with 2 or fewer week changes; override rate falls from first to second draft | M |
| **Golden set from real wish lists, running in CI**: beta cottages' wish lists (with consent) become golden rows next to the 27 synthetic ones; any hard-limit breach blocks release (M4) | 92% pass rate, 0 hard-limit breaches shipped, measured token cost per draft replacing the assumed 0.60 CAD a season | H |

### Horizon 2 — Next (3-9 months)
*Bets. Requires new capabilities or integrations.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| **Outcome pricing live**: 20 CAD per settled season through Stripe, on top of the 48 CAD base plan (M3), alongside Stripe's existing May 2027 launch. Only if the beta passes the kill criteria | Settle rate, and add-on adoption against the 25% estimate | M |
| **`lib/ai.ts` with a backup provider** (M2 kill switch), built when the paid add-on makes an outage cost revenue, not before | 48-hour provider swap proven on the golden set | H |

### Horizon 3 — Bet (9-18 months)
*Moonshots. High uncertainty, high potential.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| **Multi-season fairness ledger**: who got which holiday and nights against share carry across years, so leaving means losing the record (M2 defense) | Year-2 retention of co-owned cottages | M |
| **Network intelligence**: anonymous cross-cottage patterns (how holiday clashes settle) set defaults for new cottages, through an aggregate-only function that keeps tenant isolation (M2, M5) | First-draft acceptance for new cottages approaches returning cottages | L |

**Deliberately not on the roadmap yet:** the four red-team fixes (wish-list gaming, stale drafts, lock-in races, code-written note numbers) and receipt photos. The red-team fixes are designed and their golden rows (24 to 27) already block release, so the beta can't ship a draft that fails them; building them is pulled forward only if the beta shows the failure.

## AI Evaluation
*Course AI Bet Evaluator, all eight dimensions, run on 2026-11-16 against this repo's README. Answered by an independent reviewer, not the author of the strategy.*

| Dimension | Score | Finding | Action taken |
|-----------|-------|---------|--------------|
| Bet Validation | 2/5 | Clear, falsifiable kill criteria, but no interviews, usage or named beta cottages; validation only happens once a year, at spring planning | H1 now starts with 5 named cottages and interviews by 31 January 2027 |
| Capability Assessment | 3/5 | Working prototype and code guardrail; most promised pieces (`lib/ai.ts`, CI golden set, correction capture, red-team fixes, Stripe) not built; one founder carries everything | H1 cut to recruit, beta with correction capture, and the golden set; the provider adapter moved to H2 |
| Impact Analysis | 1.5/5 | About 485 CAD a year at an assumed 100 cottages; no market size or path from 1 to 100 cottages | Pitch reframed as retention first, revenue second |
| Defensibility Check | 2/5 | Right defense (the record), but the correction loop and fairness ledger aren't built; Family Cottage leads 7/20 to 6/20; fails the freeze test | Correction capture ships inside the beta, so the first season creates the record |
| Pricing Alignment | 2.5/5 | Outcome pricing fits value and survives 10x users and 3x inference; no willingness-to-pay signal; card fees likely exceed AI cost | Beta cottages agree to the 20 CAD price up front; card fees named in the economics |
| Trust & Reliability | 3.5/5 | Strongest area: deterministic guardrail, visible confidence, lock-in blocked on contested weeks, numeric contract; all golden rows synthetic, CI not running, confidence thresholds uncalibrated | Real wish lists become golden rows; check that Clear weeks are edited less than Close calls |
| Governance & Scale | 3/5 | Clear autonomy boundaries and a scoped agent; shadow AI audit is hypothesis-driven; all three learning loops inactive | Rerun the audit with beta families using the one-question survey |
| Gap Identification | 3/5 | Bet weakest, Moat next; untested: the pain, the 25% share, willingness to pay, token costs, recruitability | Evidence gaps listed below; each beta step replaces an assumption with a measurement |

**Overall Score:** 2.5/5. Careful trust and margin design on top of a bet with no outside evidence yet.
**Biggest Risk:** failing to recruit 5 co-owned cottages before spring 2027 planning, so the kill test never runs.
**Top 3 Actions:** recruit and confirm 5 named cottages with a 20 CAD commitment; build correction capture and lock-in before anything in H2 or H3; replace assumed numbers (token costs, the 25% share, market size, payment fees) with measured or sourced ones.

**Still assumed, not measured:** the hours families spend settling a summer, the 25% co-owned share, willingness to pay 20 CAD, token cost per draft, model list prices, card fees, and the size of the co-owned cottage market.

## Board Pitch
*Generated with the course Pitch Builder for a Founders / Funding Committee audience, 2026-11-16.*

**Thesis (1 sentence):**
Families who co-own a cottage spend hours every spring negotiating the summer in a group chat; Season Draft settles it fairly in one draft, and every season it settles makes the family's fairness record harder to leave, which makes it a retention engine first and a revenue line second.

**The case:**
1. Why now: Cottage Book is already live at cottagebook.ca with the pieces a fair draft needs: bookings, family branches with shares, and a shared cost ledger, all under tenant isolation. In the last year models became good enough to read a free-text wish list ("nothing before July 23", "the wedding weekend") and explain a tradeoff in plain words, at about 0.60 CAD a season. Family Cottage, the closest competitor, sells branches, fairness and expense splits to co-owners but has no AI draft yet. Why this team: a 20-year SaaS product leader who built and runs the product solo, already inside the Eels Lake cottage community where the first outside owners come from. The window is the spring 2027 planning season; miss it and the bet waits a year.
2. What's defensible: Honestly, not much yet. A free chatbot can draft a rough season today, and the flywheel scores 6/20 against Family Cottage's 7/20. The defense is the record, not the model (M2): drafts that become real bookings, a code guardrail that checks every week against each family's hard limits, and corrections plus a multi-season fairness history that make next year's draft better and leaving costly. None of that compounds until correction capture ships, so it ships inside the beta, not after it.
3. The economics: About 0.60 CAD of AI per settled season against a 20 CAD outcome price, about 97% gross on the add-on, and above 90% even at 3x inference prices (M3). Card fees on a 20 CAD charge (about 0.90 CAD at an assumed 2.9% plus 0.30) cost more than the AI. The revenue is small: about 485 CAD a year at an assumed 100 cottages, with no sized market or path to 100 yet. So the case is retention, not revenue: does a co-owned cottage with a settled season and a fairness record stay? Token costs, the 25% co-owned share and willingness to pay are all still assumptions the beta replaces with measurements.

**The risks:**
1. Trust / failure modes: The headline failure is a draft that gives a family a week they said they couldn't do, or tells every member about another branch's private plans in a cottage set to hide bookings. The M4 contract catches both: a code guardrail on every hard limit, per-week confidence (Clear, Close call, Needs your call), no lock-in until the organiser resolves contested weeks, and a 27-row golden set with 7 adversarial cases that blocks release on any breach. Weakness the evaluator flagged: every golden row is synthetic and CI isn't running yet, so beta wish lists become golden rows.
2. Scale / governance: At 10x, AI cost stays in cents; what breaks is one founder as on-call, reviewer and privacy officer, and Quebec Law 25 the moment a Quebec resident joins (M5). Governance is written down: AI drafts on its own, but locking in, sending and charging need a human, and the one agent can't merge. All three learning loops are inactive today, and the shadow AI audit found zero confirmed workarounds, so the signals are hypotheses until families use it.
3. Competitive: Family Cottage adds an AI draft on the co-owner data it already holds within 6 to 12 months, before Cottage Book has a fairness record worth staying for. The kill: fewer than 3 of 5 beta cottages settle a season with 2 or fewer week changes, or 5 named cottages can't be recruited by 31 January 2027.

**The ask:**
Founder time of about 30 hours a month and under 50 CAD of AI cost, no new cash or hires. For it: 5 named co-owned cottages recruited and interviewed by 31 January 2027, a Season Draft beta with correction capture through the spring 2027 planning window, real wish lists turned into golden rows, and a go or stop decision by 31 May 2027. Paused while this runs: round robin picks, receipt photos, the provider failover adapter, and expansion beyond Ontario.

### Presenter notes
- **Opening line (literally say this first):** "Every spring, families who share a cottage spend hours in a group chat fighting over who gets Canada Day; I want 5 of them to let an AI settle it, and I'll stop if 3 don't."
- **If you only get 60 seconds:** Season Draft settles a co-owned cottage's summer in one fair draft and turns each settled season into a record that keeps the family on Cottage Book. The biggest risk is that I can't recruit 5 real co-owned cottages before spring planning, so the test never runs. I'm asking for 30 hours a month and under 50 CAD to recruit them by 31 January and decide go or stop by 31 May.
- **The one question they'll ask first:** "You have one family and zero outside evidence; why should we believe anyone pays for this?" Answer: "You shouldn't yet, which is why the ask is a 5-cottage test with a 20 CAD commitment up front and a kill rule, not a launch."

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:** Families who co-own a cottage will accept an AI-drafted summer if it shows every branch's fair share in nights and explains each clash. Cottage Book already tracks branches and shares, so turning a group-chat negotiation into one draft is worth paying for. Kill it if fewer than 3 of 5 cottages adopt the draft.

**Now:** The AI draft itself is the easy part; a free chatbot can do a rough one, so the value is the record around it: a code guardrail families can trust, corrections that compound, and a fairness history that is hard to leave. AI cost is not the risk (about 97% gross on the add-on), so price on the outcome, 20 CAD only when a season settles. The bet is still unproven with real families, so the next six months exist to recruit 5 real co-owned cottages and test the bet against the same kill criteria in the spring 2027 planning window, before building anything bigger.

## AI Bet Evaluator Output (full)
*Course AI Bet Evaluator, all eight dimensions selected, run on 2026-11-16 against this repo's README. The tool's prompt was answered by an independent reviewer, not the author of the strategy. Recorded as returned; the summary table and the actions taken are in the AI Evaluation section above.*

**Bet Validation**, Score: 2/5
- Strengths: The hypothesis is falsifiable and the kill criteria are explicit: fewer than 3 of 5 real co-owned cottages lock in a draft with 2 or fewer week changes, or any hard-limit breach gets past the guardrail. The diagnostic is honest (Confidence M, "no co-owned cottage has tried it yet").
- Gaps: There is no user evidence. No interviews, no usage, no recruited beta cottages named. The "hours every spring" pain is the founder's own estimate. The shadow AI audit found 0 seen workarounds and says "every build decision rests on one family." Validation is seasonal: real wish lists exist once a year, so missing the spring 2027 planning window pushes the test out a year. Five cottages is too small a sample to tell signal from noise.
- Recommendation: Before building anything more, name and commit 5 co-owned cottages and run 5 interviews about how they settled last summer. Lock the beta to the spring 2027 planning window.

**Capability Assessment**, Score: 3/5
- Strengths: A working prototype exists. The guardrail runs in code. Scope is modest: a single model call, not an agent. Tenant isolation and the booking conflict check already exist in the product.
- Gaps: Most of what's promised isn't built yet: `lib/ai.ts`, the failover adapter, the golden set running in CI, correction capture, all four red-team fixes, and Stripe (payments aren't live until May 2027). One founder at about 30 hours a month is the builder, reviewer, on-call and privacy officer.
- Recommendation: Cut H1 to the beta plus correction capture. Ship the adapter only when a second provider is actually needed.

**Impact Analysis**, Score: 1.5/5
- Strengths: The economics are internally consistent, and the strategy admits that fixed hosting, not AI, sets the margin.
- Gaps: Even at 100 cottages, an assumed number with no path to it, the uplift is about 40 CAD a month (485 CAD a year), and that assumes all 25 drafted seasons settle. That is a small gain against roughly 90 founder hours in the beta alone. The 25% co-owned share is an estimate. There is no market size for co-owned cottages and no acquisition plan.
- Recommendation: Size the co-owned cottage market in Ontario and Quebec and lay out how Cottage Book gets from 1 to 100 cottages. Without that, the feature is a retention hook, not a revenue line, and it should be pitched that way.

**Defensibility Check**, Score: 2/5
- Strengths: The strategy candidly concedes that a free chatbot drafts well enough. The defense it picks, the record (corrections and a multi-season fairness ledger) plus bookings that actually land, is the right one.
- Gaps: Flywheel 6/20, behind Family Cottage at 7/20. The correction loop isn't built. The ledger is H3. It fails its own 3-month freeze test. Family Cottage already has the co-owner data and the users. Switching costs today are close to zero.
- Recommendation: Treat correction capture and the year-one fairness record as the product itself, and have them live before the first beta season locks.

**Pricing Alignment**, Score: 2.5/5
- Strengths: Outcome pricing per settled season is well matched to how value is delivered. A 10x power user costs cents, since redrafts are unlimited, and the add-on holds above 90% gross at 3x inference.
- Gaps: There is no willingness-to-pay signal at all; the "labor test" is an assumption. Per-call token counts and model prices are "assumed, not looked up." Payment fees are left out, and on a 20 CAD charge they likely cost more than the AI. Undercutting a competitor that has users, with one cottage, is risky.
- Recommendation: In the beta, ask each cottage to commit to the 20 CAD price before lock-in. Log real token counts from the prototype.

**Trust & Reliability**, Score: 3.5/5
- Strengths: This is the strongest part of the strategy. The guardrail is deterministic. Confidence tiers are visible, "Needs your call" blocks lock-in, and the human in the loop is the organiser. There is a numeric contract (92% pass, zero breaches, p95 under 45 s). The 27 golden rows include 7 adversarial cases and privacy cases.
- Gaps: All 27 rows are synthetic, built from one illustrative cottage. CI isn't running. The 50% and 90% confidence thresholds come from the model's own tags with no calibration evidence. There is no uptime promise.
- Recommendation: Turn each beta cottage's real wish lists into golden rows. Measure whether "Clear" weeks are actually edited less often.

**Governance & Scale**, Score: 3/5
- Strengths: Autonomy boundaries are clear, the triage agent can't merge, and PIPEDA and Law 25 triggers are named.
- Gaps: The shadow AI audit is hypothesis-driven: it searched only the founder's Gmail and couldn't access the feedback table. All three learning loops are inactive. One person carries the whole governance load.
- Recommendation: Run the audit again with beta families directly, using the one-question survey the strategy already proposes.

**Gap Identification**, Score: 3/5
- Strengths: The strategy is self-aware about weak moat scores, unbuilt loops and unproven adoption.
- Gaps: The weakest component is the Bet, with the Moat close behind. Untested assumptions include the pain itself, the 25% share, willingness to pay, token costs and recruitability. Questions it can't answer today: where do 5 co-owned cottages come from, how many exist, and why spend founder time here instead of on growing the base product?
- Recommendation: Add a one-page evidence log that ties every number to a source, marked seen or assumed.

- **Overall Score:** 2.5/5. Careful trust and margin design built on top of a bet with no outside evidence.
- **Biggest Risk:** Failing to recruit 5 co-owned cottages in time for spring 2027 planning. Then the kill test never runs, and the strategy stays a well-documented hypothesis for another year.
- **Top 3 Actions:**
  1. Recruit and confirm 5 co-owned cottages by name now, with a 20 CAD price commitment, ahead of spring planning.
  2. Build correction capture and the lock-in flow before anything in H2 or H3, so the beta generates the record that is the moat.
  3. Replace the assumed numbers (token costs, 25% share, market size, payment fees) with measured or sourced figures, and reframe the board case around retention unless revenue at scale can be shown.
