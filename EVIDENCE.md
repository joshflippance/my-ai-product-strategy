# Evidence Log

Every key number in this strategy, where it comes from, and how much to trust it. Added after the AI Bet Evaluator flagged that the strategy mixes measured and assumed figures.

**Status:** *Seen* = observed in the product, the repo or real data. *Sourced* = from a named outside source. *Self-scored* = my own rating against a course framework. *Assumed* = an estimate the Season Draft beta is meant to replace.

## Users and demand
| Claim | Value | Source | Status |
|-------|-------|--------|--------|
| Families using Cottage Book | 1 family dogfooding, plus 1 cottage from the Eels Lake launch post | Cottage Book `docs/PRD.md` and `docs/BACKLOG.md` (item 5, 2026-10-26) | Seen |
| Co-owned cottages that have used Season Draft | 0 | Prototype only; no beta yet | Seen |
| Time families spend settling a summer | About 2 hours a spring for the organiser | Founder estimate, used in the M3 labor test | Assumed |
| Share of cottages that are co-owned with branches | About 25% | Founder estimate (M3 packaging) | Assumed |
| Willingness to pay 20 CAD per settled season | Untested | No price conversation yet | Assumed |
| AI workarounds users have built | 0 seen of 10 listed | Gmail search, 2026-11-09; in-app feedback not reviewed | Seen (0) / Assumed (10) |
| Size of the co-owned cottage market | Unknown | Not researched | Missing |

## Pricing and competition
| Claim | Value | Source | Status |
|-------|-------|--------|--------|
| Cottage Book base price | 48 CAD a year per cottage; 36 CAD Eels Lake founder price | Cottage Book pricing page and PRD | Seen |
| Season Draft price | 20 CAD per settled season | Decision in M3; not tested with buyers | Assumed |
| Family Cottage price | 44.99 a year per property (probably USD) | Cottage Book PRD, ADR-023, from the competitor's site | Sourced |
| Family Cottage has no AI draft | As of October 2026 | Competitor's public site and PRD ADR-023 | Sourced |

## Costs
| Claim | Value | Source | Status |
|-------|-------|--------|--------|
| Tokens per season draft | About 2,500 in and 2,000 out | Estimated from the prototype's prompt size | Assumed |
| Model list prices | Small 1/5, mid 3/15, frontier 5/25 USD per million tokens | Not looked up | Assumed |
| Exchange rate | 1 USD = 1.38 CAD | Not looked up | Assumed |
| AI cost per settled season | About 0.60 CAD | Derived from the three lines above | Assumed |
| Fixed hosting | About 62 CAD a month | Vercel Pro plus Supabase Pro at list price, not actual bills | Assumed |
| Card fees on a 20 CAD charge | About 0.90 CAD (2.9% plus 0.30) | Standard card rate, not confirmed for this account | Assumed |
| Organiser's adjacent AI spend | About 35 CAD a month (ChatGPT Plus plus Splitwise Pro) | List prices, not checked | Assumed |
| Scale used in the board economics | 100 cottages, 25 on Season Draft | Planning scenario | Assumed |

## Trust, governance and scoring
| Claim | Value | Source | Status |
|-------|-------|--------|--------|
| Golden set | 27 rows, 7 adversarial, all synthetic | `04-the-contract/golden-dataset.md` | Seen |
| Golden set running in CI | Not yet | Planned for Horizon 1 | Seen |
| Provider does not train on API inputs | Anthropic may not train on customer content | Anthropic Commercial Terms of Service | Sourced |
| Quebec Law 25 applies once Quebec residents join | No minimum size; applies wherever the business is | BCLP, "Quebec Law No. 25: a little-known privacy law with a big reach" | Sourced |
| Vulnerability scores | Moat 2, Data 2, Platform 3 (of 5) | M1 diagnostic | Self-scored |
| Data flywheel | 6/20; Family Cottage 7/20 | M2 flywheel scorer | Self-scored |
| AI Bet Evaluator | 2.5/5 overall | Course tool, 2026-11-16 | Seen |

## What the beta replaces first
1. Willingness to pay: each of the 5 beta cottages agrees to the 20 CAD price up front.
2. The pain: 5 interviews about how each family settled last summer, and how long it took.
3. AI cost: real token counts logged per draft, replacing the 0.60 CAD estimate.
4. Card fees and hosting: actual Stripe and Vercel/Supabase bills.
