# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 1/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 2/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 2/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 1/5 |

### Correction Loop - 1/5
**What you capture today:** Nothing. An organiser can reassign any week in Season Draft (marked "Your call"), but the edit isn't saved, so the next draft starts from zero.
**How it compounds:** Once each draft is stored next to the family's final schedule, every edit becomes a labelled example of what this family calls fair, fed into next season's draft.

### Preference Loop - 2/5
**What you capture today:** Cottage Book stores every booking per branch, but Season Draft doesn't read it yet. Wish lists and last year's history are typed in fresh each season.
**How it compounds:** Each season adds who got which holiday and nights used against share, so "last year" fills itself in and the fairness ranking gets sharper per family.

### Domain Context Loop - 2/5
**What you capture today:** Bookings, branches and shares, shared costs, chat and house info all live in Cottage Book, but Season Draft only reads the wish lists.
**How it compounds:** Branch shares already drive both fairness and cost splits. Feeding booking history, cost balances and date talk in chat into the draft would make each area improve the others.

### Network Loop - 1/5
**What you capture today:** Nothing across cottages. Tenant isolation is a hard rule, so no cottage sees another's data, and there is one cottage today.
**How it compounds:** Later, opt-in anonymous patterns (how families settle holiday clashes, what share splits they choose) could set better defaults for new cottages without exposing any family's data.

**Total Flywheel Score: 6/20**
**Weakest Loop:** Correction (tied with Network at 1/5; Correction chosen because it's the cheapest to fix and the one a free chatbot can't copy)
**Fix for weakest loop:** Save every AI draft next to the family's final schedule, record each week they changed and why, and feed last season's edits into next season's prompt as "this family's corrections".

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:** OpenAI (ChatGPT)
**Vector:** An organiser pastes the branches' wish lists into ChatGPT, or a shared ChatGPT group chat, and gets a season draft and family note for free.
**Time-to-threat:** Now, 0 to 6 months. It already works well enough.
**% of value at risk:** 50%. The draft itself is exposed; the calendar, guardrail, fairness history and cost ledger it lands in are not.

### 2. Vertical Competitor
**Attacker:** Family Cottage (familycottage.app)
**Vector:** Already sells co-owners branches, nights-per-family fairness, round robin picks and expense splits. An AI season draft is one more feature on data they already hold.
**Data they have that I don't:** Booking and expense history across many co-owned properties today, versus one cottage for Cottage Book.
**Time-to-threat:** 6 to 12 months.
**% of value at risk:** 60%.

### 3. Adjacent Expansion
**Attacker:** Cozi / TimeTree (family calendar apps)
**Vector:** Add a shared-place booking view and an AI "plan our summer" planner on top of the family calendar.
**Distribution advantage:** Millions of families already open them daily, so there's no new app to install or invite people to.
**Time-to-threat:** 12 to 18 months.
**% of value at risk:** 45%.

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** OpenAI (ChatGPT), played as Head of Product
**Attack vector (target the weakest loop):** Correction. Cottage Book throws away every edit a family makes to a draft. ChatGPT keeps every correction in the conversation and in memory, so its second season is better than Cottage Book's.
**Weeks 1-4 - what they ship:** A "Plan a shared stay" template in ChatGPT group chats. Each family member adds their wishes, ChatGPT drafts the season with a fairness table, anyone can say "give Paul the Civic Holiday instead" to redraft, and it exports to Google and Apple Calendar.
**Weeks 5-8 - how they poach users:** Seed the template in cottage and co-ownership Facebook groups and Reddit threads with "stop fighting over the long weekend." Free, no new app to install, and the family is already in ChatGPT.
**Weeks 9-12 - why users don't come back:** Memory. Next spring ChatGPT says "last year Lisa had Canada Day and Paul changed two weeks, here's this year's draft." Cottage Book starts from a blank wish list, so the family never reopens it.
**Your defense:** Own the record, not the draft. Capture every draft against the family's final schedule and every edit with its reason, so next season starts from last year automatically. The draft becomes real bookings with tenant isolation, the hard-limit guardrail, reminders and the shared cost ledger. ChatGPT can draft a season; Cottage Book is where the season actually lives and where its history compounds.
