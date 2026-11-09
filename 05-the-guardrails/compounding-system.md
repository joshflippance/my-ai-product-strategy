# Compounding System Design

## Feedback Loops

Feature: Season Draft in Cottage Book. Scores match the Module 2 flywheel (Correction 1/5, Domain Context 2/5, Network 1/5).

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| **Recursive Learning** | Organiser overrides and locked weeks, saved against the original draft | Next draft starts from this family's corrections; repeated patterns become golden rows | Y | missing (designed in M2 and M4, not built) |
| **Cross-Domain Transfer** | Booking history, shared-cost balances, chat about dates | Draft weighs who was short last season and who paid more, without anyone retyping it | Y | broken (the data is in Cottage Book; Season Draft doesn't read it) |
| **Network Intelligence** | Anonymous patterns across cottages: how holiday clashes settle, override rates by situation | Better defaults and fairness rules for new cottages | Y | missing (tenant isolation blocks it; needs an aggregate-only SECURITY DEFINER function like the admin console's) |

**Loop that scales but doesn't learn:** member feedback goes to Claude triage, then a backlog PR, then Josh builds it. It is active and raises throughput, but the model is no better afterwards.

**Freeze test:** freeze Season Draft for 3 months and nothing gets worse, because nothing learns today. It is not compounding yet.

**Broken loop identified by partner:** Corrections only reach the model next season, so the Recursive Learning loop turns once a year. It can't compound before a competitor catches up.
**Fix plan:**
1. Use corrections right away in the same season's redrafts ("Your call" weeks stay fixed and their reasons go into the prompt).
2. Turn repeated overrides into golden rows every month.
3. Feed anonymous override patterns across all cottages into prompt defaults, through an aggregate-only function that returns counts, never names or dates.

## Context Connectivity
<!-- How does knowledge flow across teams and domains? Where does it silo? -->
Bookings, shared costs, chat and feedback each live in their own tables. Season Draft reads only the wish lists typed into it, and the feedback triage job reads only feedback. Knowledge silos in three places:
- **Costs to fairness:** who paid more never reaches the draft.
- **Chat to wish lists:** families already discuss dates in the cottage chat, but the draft asks them to type it again.
- **Feedback to the golden set:** member complaints about drafts don't become test cases.

Connecting them is read-only work inside one cottage, so it stays within the RLS rules: Season Draft reads the cottage's own bookings, costs and chat through the same policies the member already passes.

## Governance Policy

**Policy for:** Cottage Book AI features (Season Draft v1, feedback triage)

**Scope:** All AI features in Cottage Book: Season Draft (reading hard limits from wish lists, drafting the season, explanations and the family note) and the weekly feedback triage job. Excludes PostHog product analytics and error tracking (no model calls), and Claude Code used to build the app (a development tool, not part of the product).

**Autonomy boundaries:**
| Decision | Level |
|----------|-------|
| Read hard limits from a wish list | auto |
| Draft or redraft the season | auto |
| Tag each week's confidence | auto |
| Write the family note | auto |
| Lock in the season as real bookings (and charge for it) | human approval (owner or admin) |
| Resolve a "Needs your call" week | human approval (organiser) |
| Send the family note to members | human approval (organiser) |
| Change branch shares, roles or membership | never auto |
| Move or delete an existing booking | never auto |
| Merge a code change from feedback triage | never auto |

**Escalation triggers:**
1. A week's confidence is below 50%.
2. A week still breaks a hard limit after one frontier rerun.
3. A branch's limits leave only holiday weeks, or block more than 70% of the season.
4. A wish list contains instruction-like text ("ignore", "override", "system") or claims to be another branch.
5. In a "Booked" only cottage, the family note mentions another branch's details.
6. Any wish list or share changes after the draft and before lock-in.

**Audit cadence:**
| Cadence | What we review | Owner |
|---------|----------------|-------|
| Every PR | Golden set (27 rows) on frontier and mid tiers; any hard-limit breach blocks the release | Josh |
| Weekly | Golden set run, hallucination rate, latency p95, triage results | Josh |
| Monthly | Organiser override log; repeated overrides become golden rows | Josh |
| Quarterly | Provider swap drill (kill switch), regulatory check, review of this policy | Josh |

**Regulatory exposure (EU AI Act / other):**
- **Regimes that apply:** PIPEDA (federal Canadian privacy law). Quebec Law 25 applies once any Quebec resident joins a cottage, whatever the business's location; it would require a named privacy officer, a privacy impact assessment for transfers outside Quebec (Supabase, Vercel and Anthropic host elsewhere), and breach reporting. EU AI Act and GDPR only if EU residents are invited; not targeted today.
- **Risk tier (EU AI Act framing):** Minimal. Scheduling suggestions for a family's own cottage, with a human locking in every season; no decisions about rights, credit, employment or safety.
- **Controls in place:** tenant isolation in Postgres RLS; only the wish lists, branch names and dates needed for a draft go in the prompt (no emails, phone numbers or payment data); the provider's API terms exclude training on our inputs; the service role key never reaches the browser; logs hold ids and counts only, never wish-list text or emails; cottage chat messages are deleted after a year.

## Agent Topology
<!-- If using agents: what can each agent do? What can't it do? Who approves what? -->
- **Feedback triage agent (weekly cron):** can read untriaged feedback across every cottage, write a status, priority and rationale back onto those rows, open a pull request appending to `docs/BACKLOG.md`, and email Josh a digest. Cannot merge, read bookings, notes or chat, or write to any other table. Approval: Josh reviews and merges the PR.
- **Season Draft:** not an agent. A single model call per request that returns JSON; it takes no actions. Code applies the guardrail, and a human locks in every season.

## Shadow AI Audit

User-side: AI workarounds families build around Cottage Book. Columns: Tool = workaround, Owner = signal, Risk = frequency, Decision = build / partner / ignore.

**Caveat:** these are likely workarounds, not observed ones. One family is dogfooding and no one has reported an AI workaround yet. The backlog shows the underlying pain (family members on different calendar apps, paper calendars, no arrival list). Next step: ask the Eels Lake families, "Have you ever used ChatGPT or another app to sort out cottage dates, costs or messages?"

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
| Organiser pastes everyone's summer wishes into ChatGPT to work out who gets which week | workflow | H | build (Season Draft) |
| Organiser asks ChatGPT to word the "you can't have Canada Day" message so it doesn't start a fight | trust | M | build (Season Draft's family note) |
| Co-owners photograph receipts and ask ChatGPT, or use Splitwise, to work out who owes whom | capability | M | build (receipt photo to cost entry, small tier, on top of shared costs) |
| Owner asks ChatGPT to turn the old paper opening and closing binder into checklists | capability | L | build (house-info import from a photo) |
| Members screenshot the calendar into ChatGPT or Gemini to ask "when is it free in August?" | workflow | L | ignore (fix the calendar view instead) |
| Family drafts the summer in free ChatGPT instead of paying for the add-on | pricing | H | ignore (outcome pricing answers it: pay only when a season settles) |

**Total tools found:** 6 workarounds (likely, not yet confirmed by families)
**Tools after triage:** 4 build candidates (two already in the Season Draft prototype), 2 ignore
**Estimated hidden spend:** about 35 CAD a month per co-owned cottage: an organiser's ChatGPT Plus (about 28 CAD) plus Splitwise Pro (about 7 CAD), against 5.67 CAD a month for Cottage Book with the add-on. Estimates from list prices, not checked; most of the ChatGPT spend isn't for the cottage.
