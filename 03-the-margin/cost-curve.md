# Cost Curve & Pricing Strategy

## Packaging Decision

| Leader | Filler | Killer | Killer usage % | Bundle or add-on |
|--------|--------|--------|----------------|------------------|
| Shared booking calendar | Shared costs and balances | Season Draft | About 25% (estimate) | Add-on, per season |

**Why:** Families come for the calendar, the one link that ends "who has the long weekend?" in the group chat. Shared costs lift value for co-owners and match Family Cottage's expense splits. Season Draft is the only feature with a real AI cost per use, and it only matters to co-owned cottages with branches, an estimated 25% of cottages. Under the 70% rule that makes it an add-on: for example, 20 CAD a season per cottage on top of the 48 CAD plan, so the 75% who never use it don't pay for it.

**Assumption to test:** the 25% usage figure is an estimate. No cottage has used Season Draft yet.

## Margin Calculator

Unit: one cottage on the Season Draft add-on, per month, in CAD. Revenue is the 48 CAD base plan plus the 20 CAD add-on, so 68 CAD a year. Stress column triples both requests and cost per request.

| Input | My number | Stress (3x) |
|-------|-----------|-------------|
| Avg requests/user/month | 2 (6 draft sessions a season, about 4 AI calls each, averaged over 12 months) | 6 |
| Cost per request (blended) | 0.029 CAD (see cost curve) | 0.087 CAD |
| Monthly COGS per user | 0.058 CAD | 0.52 CAD |
| Revenue per user/month | 5.67 CAD | 5.67 CAD |
| Gross margin per user | 5.61 CAD | 5.15 CAD |
| Gross margin % | 99.0% | 90.8% |

**Cost per request assumption:** blended from the cost curve below. Updated from a first single-model estimate (0.5 requests a month at 0.05 CAD) once Season Draft was split into tiers.

**What it means:** AI inference is not the margin risk. Even at 3x it stays well above the 40% line. The real pressure on a 68 CAD yearly plan is payment fees and fixed hosting at low volume, not the model.

## Cost Curve: Features to Tiers

Prices are assumed list prices, not looked up: small (Haiku-class) 1 USD in / 5 USD out per million tokens, mid (Sonnet-class) 3 / 15, frontier (Opus-class) 5 / 25. 1 USD = 1.38 CAD.

| Feature | Complexity | Model tier | Cost/req | Volume % | Weighted |
|---------|-----------|------------|----------|----------|----------|
| Read hard limits from wish lists; weekly feedback triage | Simple | Small | 0.004 CAD (about 1,500 in / 300 out) | 40% | 0.0016 CAD |
| "Why not me?" explanations; family note | Medium | Mid | 0.017 CAD (about 2,000 in / 400 out) | 35% | 0.006 CAD |
| Season draft (assign every week, tradeoffs, confidence) | Complex | Frontier | 0.086 CAD (about 2,500 in / 2,000 out) | 25% | 0.0215 CAD |
| **Blended** | | | | **100%** | **0.029 CAD** |

**Blended cost per add-on cottage per month:** 2 requests x 0.029 CAD = 0.058 CAD. Sending every call to the frontier model would cost 0.172 CAD, so the cascade cuts AI COGS by about two thirds.

## Cost Model

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) | 0.0435 CAD | Frontier season drafts plus mid-tier explanations and notes |
| Inference (cascading/triage) | 0.0032 CAD | Small tier reads hard limits and runs feedback triage |
| Infrastructure | To confirm | Shared fixed hosting (Vercel, Supabase), not driven by AI use; confirm from the bills |
| Data/storage | ~0 | A few KB of JSON per draft |
| Human-in-the-loop | 0 | The family organiser reviews each draft; no paid reviewer |
| **Total AI COGS** | **0.058 CAD** | 2 requests a month at a blended 0.029 CAD (rounding) |

## Cascading Strategy
<!-- Cheap model → frontier model routing logic -->

**Triage model:** Small tier (Haiku-class). Reads each branch's hard limits out of the wish lists, and runs the weekly feedback triage.
**Frontier model:** Frontier tier (Opus-class). Drafts the season: assigns every week against shares, writes the tradeoffs and confidence tags. A mid tier (Sonnet-class) handles "Why not me?" explanations and the family note.
**Routing rule:** Route by task type in `lib/ai.ts`: extraction and classification go small, explanation and writing go mid, the full draft goes frontier. If the code guardrail finds a hard-limit breach, rerun the draft once on frontier with the breach named; if it still fails, flag the week to the organiser instead of retrying.
**Expected cascade ratio:** 75% / 25% (small and mid / frontier)

## Pricing Model

**Strategy:** Penetrate. Win co-owned cottages before Family Cottage adds AI. The 48 CAD base already undercuts their 44.99 a year (probably USD, about 62 CAD), and the add-on stays cheap.
**Unit of work:** One drafted season per cottage, with unlimited redrafts inside it. It meters the outcome families want, a settled summer, and keeps the redrafts that build trust free.
**Current pricing:** 48 CAD a year per cottage (4 CAD a month), owner pays, family members free. Eels Lake founder price 36 CAD a year.
**Proposed AI pricing:** Base 4 CAD a month, plus Season Draft at 20 CAD per drafted season.
**Model:** Hybrid (base subscription plus outcome-based add-on per season)

**Labor test:** The organiser of a co-owned cottage spends several hours each spring collecting wishes, settling clashes and re-sending the schedule. At even 25 CAD an hour, two hours is 50 CAD of work against a 20 CAD season, so the price is a giveaway, which is the point of a penetration price.

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | COGS 0.17 CAD; margin 99.0% to 96.9% | Absorb. No change needed. |
| Heaviest segment doubles | Requests 2 to 4 a month; COGS 0.12 CAD; margin 98.0% | Absorb. Watch for heavy redrafting as a sign the first draft misses. |
| Model provider raises prices 50% | COGS 0.087 CAD; margin 98.5% | Absorb. Test the draft on the mid tier against the golden set; move it down if it passes. |

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):**
**After (AI-enabled):**
**Net margin shift:**
