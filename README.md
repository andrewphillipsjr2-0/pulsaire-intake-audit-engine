# Pulsaire Intake & Audit Engine

**AI-powered lead qualification + instant automation audit reports — built on Make.**

TripleTen Final Project · Sprint 7: *Automate a Real-World Process with AI* · by Andrew Phillips Jr. ([Pulsaire](https://pulsaire.com))

---

## The Problem

AI automation agencies (like Pulsaire) lose deals two ways:

1. **Slow lead response.** Manually reading, researching, and qualifying each inbound inquiry takes ~20 minutes per lead. Responding within 5 minutes vs. 1+ hours dramatically increases conversion — most agencies can't do it.
2. **Unpaid discovery work.** Prospects want proof of value before they commit. Writing a custom "here's what you could automate" assessment takes ~2 hours per prospect — so it rarely happens.

## The Solution

One Make scenario, triggered by a single **Automation Readiness Audit** form, with two AI-powered branches:

| Branch | Audience | What the LLM does | Output |
|---|---|---|---|
| **A — Qualify** | Internal (Pulsaire) | Scores lead 1–100, classifies fit/budget/urgency, extracts pain points, recommends next action | Google Sheets pipeline row + instant email alert with suggested reply |
| **B — Audit Report** | External (prospect) | Generates a personalized mini-report: top 3 automation opportunities, estimated hours saved, recommended starting point, book-a-call CTA | Google Doc emailed to the prospect automatically |

### Quality Control

- LLM returns a **confidence score** with every analysis
- Low confidence or malformed input → report is **NOT auto-sent**; lead flagged `manual_review` and Drew is notified
- Every run (success or failure) logged to a `Log` tab: timestamp, lead, status, error message
- Make error-handler route catches failed LLM calls — nothing fails silently

## Architecture

```
Google Form (prospect fills audit)
        │
        ▼
   Make scenario
        │
        ▼
  LLM analysis (custom prompts)
        │
   ┌────┴─────────────┐
   ▼                  ▼
Branch A           Branch B
Lead score &       Personalized audit
classification     report (Google Doc)
   │                  │
   ▼                  ▼
Sheets pipeline    Confidence check
+ email alert      ├─ high → email report to prospect
to Drew            └─ low  → flag manual_review, alert Drew
        │
        ▼
   Log tab (every run)
```

## Tools Used

- **Make** — orchestration (4+ connected services)
- **Google Forms** — external input (prospect-facing)
- **OpenAI / Gemini** — LLM steps with two custom prompts ([see /prompts](./prompts))
- **Google Sheets** — structured output: pipeline + run log
- **Google Docs** — generated audit report
- **Gmail** — internal alerts + automated report delivery
- **Miro** — workflow mapping ([see /docs](./docs))

## ROI

| Metric | Manual | Automated |
|---|---|---|
| Lead qualification | ~20 min/lead | ~0 min (instant) |
| Audit/assessment | ~2 hrs/prospect (rarely done) | ~2 min, every prospect |
| First response time | hours–days | < 5 minutes |
| At 30 leads/month | ~70 hrs/month | ≈ 0 |

## Repo Structure

```
docs/       Process maps, build log, rubric mapping
prompts/    The two production LLM prompts + design notes
assets/     Screenshots of the workflow, tests, and outputs
```

## Project Status

See [docs/BUILD_LOG.md](./docs/BUILD_LOG.md) for the step-by-step build journal.
