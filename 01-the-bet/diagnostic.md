# Three-Axis Vulnerability Diagnostic

## Product
<!-- Name the product you're diagnosing. Real product at your company — not a hypothetical. -->

**Product:** Cottage Book (Season Draft feature)
**Your Role:** Founder, solo builder

---

## Scores

### Contextual Moat — 2/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:** A family could leave easily in the off season. Branches, shares and the cost ledger add some stickiness once a cottage actually uses them, but only one cottage does today.

**Named attacker (from partner challenge):** Family Cottage (familycottage.app), which already sells co-owners branches, fairness tracking, round robin picks and expense splits.

---

### Data Advantage — 2/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:** Season over season fairness history (who got which holiday, nights used against share) compounds per cottage, and a general model never sees it. Today it is tiny and lives in one cottage.

**Named attacker (from partner challenge):** ChatGPT or Claude used directly. An organiser pastes the wish lists into a chatbot and gets a decent draft for free.

---

### Platform Exposure — 3/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:** Scored higher = safer. Google Calendar or Apple Family could add shared calendars with AI suggestions, but they are unlikely to model branches, shares and costs. As a solo builder I can pivot quickly.

**Named attacker (from partner challenge):** Google Calendar and Apple Family sharing with built-in AI scheduling.

---

## Top Vulnerability
<!-- One line: what's the single biggest strategic risk? -->
A free chatbot is good enough to draft the season, so the AI draft alone won't justify paying; the value has to come from the guardrail, the fairness history and the calendar the draft lands in.

## Confidence Level
<!-- H / M / L — how confident are you in this bet after the diagnostic? -->
M. The pain is real and the prototype works, but moat and data score low and no co-owned cottage has tried it yet.
