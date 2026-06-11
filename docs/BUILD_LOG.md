# Build Log

A step-by-step journal of how the Pulsaire Intake & Audit Engine was designed, built, and tested.

## 2026-06-11 — Project kickoff

- Reviewed TripleTen final project brief and rubric (Sprint 7: Automate a Real-World Process with AI)
- Brainstormed 10 candidate automations for Pulsaire; shortlisted 4
- **Decision:** combine Idea #1 (AI Lead Qualification Engine) + Idea #4 (Audit-to-Insights Report Bot) into a single intake workflow
  - Rationale: one form submission powers both an internal sales-ops outcome and an external prospect-facing deliverable — stronger business value, same trigger
- Chose **Make** as the automation platform (vs. Zapier/n8n)
- Defined architecture: Google Form → Make → LLM (2 custom prompts) → Branch A (Sheets pipeline + alert email) / Branch B (Google Doc report → confidence-gated auto-send)
- Defined QC strategy: LLM confidence scoring, manual-review routing, full run logging, Make error handler
- Initialized this repo; drafted README and process map

## Next

- [ ] Map full before/after workflow in Miro
- [ ] Scaffold Google Form, Sheet (pipeline + log), Doc template
- [ ] Build Make scenario
- [ ] Test: clean input / vague input / garbage input
- [ ] Presentation deck
