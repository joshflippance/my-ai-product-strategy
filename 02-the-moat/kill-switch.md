# Kill Switch Audit

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** | Single vendor, Anthropic. One hard-coded model (`claude-sonnet-5`) and one API key, used by the weekly feedback triage cron (`lib/feedbackTriage.ts`). Season Draft would add a second call to the same vendor. | H | Move the model name to an env var and set up an OpenAI or Gemini key as a tested fallback. |
| **Abstraction** | The call lives in one file, but it is a raw `fetch` to Anthropic's own request and response format. | M | Add `lib/ai.ts`: one `complete(prompt, schema)` function with provider adapters behind it. Triage and Season Draft call only that. |
| **Routing** | None. Every call goes to one model; if Anthropic is down, the job fails. | M | In `lib/ai.ts`, retry once on the primary, then fail over to the second provider, and log which one answered. |
| **Eval** | None for AI output. The isolation tests cover the database, not the model. | H | Seed a golden set of 10 sample seasons (including the Eels Lake example) with expected hard limits. A test fails if any draft breaks one; the guardrail code is the grader. |

## Portability Score
<!-- Ready / Partial / Locked -->
Partial. Plain HTTP, a single file and a well-specified JSON output make a swap a day's work, but there is no adapter, no fallback and no eval to prove a new provider is good enough.

### Path to 48-hour swap readiness
- **This week:** model name in an env var, and `lib/ai.ts` with an Anthropic adapter; move triage onto it.
- **This month:** second provider adapter (OpenAI or Gemini) with retry and failover, and Season Draft built on `lib/ai.ts` from day one.
- **This quarter:** golden set of 10 seasons running in CI against both providers, so a switch is proven before it's made.

## If Anthropic doubles pricing tomorrow:
<!-- What's your 48-hour response? -->
Absorb it, then cascade. A season draft costs cents and runs a few times a year per cottage, so the increase is small against a 48 CAD yearly plan. Within 48 hours, route triage to the cheapest model tier, keep Season Draft on a mid tier, and re-run the golden set to confirm quality holds.

## If Anthropic ships a competing product:
<!-- What's defensible that they can't replicate? -->
The record, not the model. Bookings under tenant isolation, the hard-limit guardrail, fairness history across seasons, branches and the shared cost ledger all live in Cottage Book, and none of it comes with a general assistant. The model is a swappable part: switch to another provider through `lib/ai.ts`.
