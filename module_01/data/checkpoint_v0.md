# v0 Checkpoint: Ticket Triage Pipeline

**Date:** 2026-10-29 | **Model:** gpt-5.6-luna (reasoning_effort=none)

## 1. Pipeline Stage Status

| Stage | Name | Status | Notes |
|-------|------|--------|-------|
| 1 | Ingest | ✅ Pass | CSV loads correctly, 6 tickets read |
| 2 | Prepare | ✅ Pass | Empty messages skipped, 6/6 passed |
| 3 | Prompt | ✅ Pass | System + user messages built for each ticket |
| 4 | Call Model | ✅ Pass | gpt-5.6-luna, reasoning_effort=none |
| 5 | Parse Output | ⚠️ Fragile | Works now, but no fallback if model returns non-JSON |
| 6 | Deliver | ✅ Pass | Results collected into a list of dicts |

## 2. Errors Encountered (2/3 resolved)

| Stage | Error Type | Description | Resolved? |
|-------|------------|-------------|-----------|
| 1 — Ingest | `FileNotFoundError` | Typo in CSV path ('data/tickers.csv' instead of 'data/tickets.csv') | ✅ |
| 3 — Prompt | `KeyError` | Referenced ticket['subject'] instead of ticket['message'] | ✅ |
| 5 — Parse Output | `JSONDecodeError` | Model occasionally returns 'Sure! Here is...' prefix before JSON | ❌ |

## 3. Baseline Accuracy

4/5 (80%) on a hand-labeled spot-check

## 4. Open Questions

- The model confused 'Account' with 'General' on ticket 103. Would a few-shot example for Account changes fix this?
- Parse Output has no fallback. What happens if the model wraps JSON in markdown fences (```json ... ```)?
- Tickets are processed one at a time. Will this be too slow for 1,000 tickets?
