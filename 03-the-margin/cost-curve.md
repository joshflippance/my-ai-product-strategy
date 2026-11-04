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
| Avg requests/user/month | 0.5 (6 drafts a season, averaged over 12 months) | 1.5 |
| Cost per request (blended) | 0.05 CAD | 0.15 CAD |
| Monthly COGS per user | 0.025 CAD | 0.225 CAD |
| Revenue per user/month | 5.67 CAD | 5.67 CAD |
| Gross margin per user | 5.65 CAD | 5.45 CAD |
| Gross margin % | 99.6% | 96.0% |

**Cost per request assumption:** one draft is about 2,500 input tokens (prompt, 4 branches, 11 weeks) and 2,000 output tokens (limits, assignments, tradeoffs, family note). At Sonnet-class list prices (3 USD per million input, 15 USD per million output) that is about 0.04 USD, or 0.05 CAD.

**What it means:** AI inference is not the margin risk. Even at 3x it stays well above the 40% line. The real pressure on a 68 CAD yearly plan is payment fees and fixed hosting at low volume, not the model.

## Cost Model

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) | 0.025 CAD | 0.5 drafts a month at 0.05 CAD each |
| Inference (cascading/triage) | 0 | No cascade yet; one model handles every draft |
| Infrastructure | To confirm | Shared fixed hosting (Vercel, Supabase), not driven by AI use; confirm from the bills |
| Data/storage | ~0 | A few KB of JSON per draft |
| Human-in-the-loop | 0 | The family organiser reviews each draft; no paid reviewer |
| **Total AI COGS** | **0.025 CAD** | |

## Cascading Strategy
<!-- Cheap model → frontier model routing logic -->

**Triage model:**
**Frontier model:**
**Routing rule:**
**Expected cascade ratio:**

## Pricing Model

**Current pricing:**
**Proposed AI pricing:**
**Model:** seat-based / usage-based / outcome-based / hybrid

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | COGS 0.075 CAD; margin 99.6% to 98.7% | Absorb. No change needed. |
| Heaviest segment doubles | Requests 0.5 to 1.0 a month; COGS 0.05 CAD; margin 99.1% | Absorb. Watch for heavy redrafting as a sign the first draft misses. |
| Model provider raises prices 50% | COGS 0.0375 CAD; margin 99.3% | Absorb, then move triage to a cheaper tier via `lib/ai.ts` (see kill switch). |

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):**
**After (AI-enabled):**
**Net margin shift:**
