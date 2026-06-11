# Process Map: Manual vs. Automated

## The manual process (before)

| # | Step | Who | Time |
|---|------|-----|------|
| 1 | Prospect emails or DMs an inquiry | Prospect | — |
| 2 | Read inquiry, research the company | Drew | 10 min |
| 3 | Judge fit, budget signals, urgency | Drew | 5 min |
| 4 | Write a personalized response | Drew | 10 min |
| 5 | Log lead in spreadsheet (often skipped) | Drew | 5 min |
| 6 | (Rarely) write a custom automation assessment | Drew | ~2 hrs |

**Pain points:** slow first response (hours–days), inconsistent qualification, leads not logged, assessments skipped because they're unpaid work. Steps 2–6 are pure reading/copying/repetitive judgment — ideal LLM territory.

## Where AI adds value

- **Extracting** pain points, tools, team size from free-text form answers
- **Classifying** lead fit, budget tier, urgency
- **Scoring** lead quality 1–100 with reasoning
- **Generating** a personalized reply draft and a structured audit report

## The automated process (after)

1. **Trigger:** Google Form "Free Automation Readiness Audit" submission (external input)
2. **LLM Call 1 — Analyst prompt:** score, classification, pain points, recommended action, confidence (structured JSON)
3. **Router:**
   - **Branch A (always):** add row to Sheets `Pipeline` tab → Gmail alert to Drew with score + suggested reply
   - **Branch B (confidence-gated):**
     - confidence ≥ threshold → **LLM Call 2 — Report Writer prompt** → create Google Doc from template → email report to prospect
     - confidence < threshold → mark `manual_review` in Sheets → alert Drew → no auto-send
4. **Logging (always):** append run record to Sheets `Log` tab (timestamp, lead, branch outcomes, status)
5. **Error handler:** any module failure → log `error` row + alert Drew

## Time comparison

- Manual: ~30 min/lead + 2 hrs/assessment
- Automated: ~0 min (review of flagged leads only)
- At 30 leads/month: **~70 hours/month returned**
