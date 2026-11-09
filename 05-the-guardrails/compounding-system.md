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

**Scope:**
**Autonomy boundaries:**
**Escalation triggers:**
**Audit cadence:**
**Regulatory exposure (EU AI Act / other):**

## Agent Topology
<!-- If using agents: what can each agent do? What can't it do? Who approves what? -->

## Shadow AI Audit

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
| | | H / M / L | keep / govern / kill |
| | | H / M / L | keep / govern / kill |
| | | H / M / L | keep / govern / kill |

**Total tools found:**
**Tools after triage:**
**Estimated hidden spend:**
