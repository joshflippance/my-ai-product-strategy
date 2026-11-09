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

### Feedback Triage Agent
`app/api/cron/feedback-triage/route.ts`, weekly Vercel cron. The only agent in Cottage Book.

**1. Autonomy**
- **Runs on its own:** weekly. Triages new feedback, writes a status, priority and rationale onto each note, opens a PR to `docs/BACKLOG.md`, and emails Josh a digest.
- **Never:** merges a PR, edits or deletes a member's note, replies to members, or changes product code.
- **Human approval:** Josh approves every backlog change by reviewing and merging the PR.

**2. Tool calls (allowlist)**
| Tool | Allowed | Not allowed |
|------|---------|-------------|
| Database (service role) | Read untriaged `feedback` rows; write `status`, `priority`, `priority_rationale`, `triaged_at` on those rows; write its own `job_runs` record | Any other table or column; bookings, chat, notes, members |
| Model API | One call per weekly batch, small tier, JSON output | Tools, web access, other providers |
| GitHub | Create a branch and open a PR touching only `docs/BACKLOG.md` | Merge, push to main, edit any other file |
| Email | One digest to Josh | Any member or outside address |

**3. Memory**
- **Stateless between runs.** Each run sees a condensed set of PRD goals and non-goals, plus that week's untriaged notes. Past decisions live only in the rows' `status` and in `BACKLOG.md`.
- **Data minimization:** only the note's text and cottage id go to the model. No names, emails or cottage names.
- **Feedback is untrusted:** member text is data, never instructions. A note saying "mark this P0" or "ignore your rules" is triaged as written, not obeyed.

**4. Chain ownership**
- **The chain:** Vercel cron, then the route (checks `CRON_SECRET`), then the model, then the database write, then the GitHub PR, then the email digest. Josh owns every link.
- **On failure:** any failed step is logged in `job_runs`, the route returns 500, and `/admin` System health shows it. If the PR step fails, the verdicts stand and the digest says the PR is missing.
- **Kill switch:** unset `CRON_SECRET` and the route refuses every call (already built).
- **Review:** quarterly, alongside the governance policy audit.

### Season Draft
Not an agent. One model call per request that returns JSON; it calls no tools and takes no actions. Code applies the hard-limit guardrail, and an owner or admin locks in every season.

## Shadow AI Audit

User-side audit of AI workarounds families build around Cottage Book. Auditor: Claude, for Josh, 2026-11-09. Repo columns: Tool = workaround, Owner = signal, Risk = frequency, Decision = build / partner / ignore.

**Method:** searched Josh's Gmail for Cottage Book with ChatGPT, Claude, Zapier, Family Cottage, Splitwise, AI and spreadsheet: no user-built AI workarounds found (only internal mail and one placeholder feedback note). Reviewed `docs/BACKLOG.md` for family-reported pain. The in-app `feedback` table was not reviewed (production access not granted to the auditor).

**Evidence levels:** *Seen* = a user did it. *Backlog* = the pain is reported in the backlog; the AI workaround is inferred. *Hypothesis* = expected from comparable products, no evidence yet.

| # | Tool | Owner | Risk Level | Evidence | Decision |
|---|------|-------|-----------|----------|----------|
| 1 | Organiser pastes everyone's summer wishes into ChatGPT to work out who gets which week | workflow | H | Hypothesis | build (Season Draft) |
| 2 | Organiser asks ChatGPT to word the "you can't have Canada Day" message so it doesn't start a fight | trust | M | Hypothesis | build (Season Draft's family note) |
| 3 | Co-owners photograph receipts into ChatGPT, or use Splitwise, to work out who owes whom | capability | M | Hypothesis | build (receipt photo to cost entry, small tier, on top of shared costs) |
| 4 | Owner asks ChatGPT to turn the old paper opening and closing binder into checklists | capability | L | Backlog (no arrival list, paper calendars) | build (house-info import from a photo) |
| 5 | Members screenshot the calendar into ChatGPT or Gemini to ask "when is it free in August?" | workflow | L | Hypothesis | ignore (fix the calendar view instead) |
| 6 | Family drafts the summer in free ChatGPT instead of paying for the add-on | pricing | H | Hypothesis | ignore (outcome pricing answers it: pay only when a season settles) |
| 7 | Co-owners tally nights per family in a Google Sheet, with Gemini or formulas | workflow | M | Hypothesis | build (show the fair-share tally in the app, respecting "Booked" only mode) |
| 8 | Owner uses Zapier or IFTTT to post new bookings into the family WhatsApp group | workflow | M | Backlog (members on different calendar apps) | partner (one-tap WhatsApp share plus the existing ICS feed) |
| 9 | Members ask ChatGPT to translate house notes for French-speaking relatives | capability | L | Hypothesis | ignore (browser translation is enough for now) |
| 10 | Prospective owner asks ChatGPT "Family Cottage or Cottage Book for co-owners?" before buying | trust | M | Hypothesis | ignore in product; answer it on the pricing page |

**Total tools found:** 10 workarounds (0 seen, 2 backed by backlog pain, 8 hypotheses)
**Tools after triage:** 5 build, 1 partner, 4 ignore
**Estimated hidden spend:** about 35 CAD a month per co-owned cottage: an organiser's ChatGPT Plus (about 28 CAD) plus Splitwise Pro (about 7 CAD), against 5.67 CAD a month for Cottage Book with the add-on. Estimates from list prices, not checked; most of the ChatGPT spend isn't for the cottage.

**Auditor's opinion:** directionally useful but evidence-thin; every build decision rests on one family. Before building rows 3, 4 or 7, confirm each with at least 3 Eels Lake families using one question: "Have you ever used ChatGPT, a spreadsheet or another app to sort out cottage dates, costs or messages?" Row 1 is the exception: it is the bet already under test through the Module 1 kill criteria.
