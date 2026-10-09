# v0 Checkpoint: Ticket Triage Pipeline

**Date:** 2026-10-05  
**Author:** AI Engineer  
**Pipeline:** Customer support ticket classification  
**Model:** gpt-4.1-nano (temperature=0)

---

## 1. Pipeline Stage Status

| Stage | Name | Status | Notes |
|-------|------|--------|-------|
| 1 | Ingest | ✅ Pass | CSV loads correctly, 6 tickets read |
| 2 | Prepare | ✅ Pass | Empty messages skipped, 6/6 passed |
| 3 | Prompt | ✅ Pass | System + user messages built for each ticket |
| 4 | Call Model | ✅ Pass | gpt-4.1-nano, temperature=0 |
| 5 | Parse Output | ⚠️ Fragile | Works now, but no fallback if model returns non-JSON |
| 6 | Deliver | ✅ Pass | Results collected into a list of dicts |

## 2. Errors Encountered (2/3 resolved)

| Stage | Error Type | Description | Resolved? |
|-------|------------|-------------|-----------|
| 1 — Ingest | `FileNotFoundError` | Typo in CSV path ('data/tickers.csv' instead of 'data/tickets.csv') | ✅ |
| 3 — Prompt | `KeyError` | Referenced ticket['subject'] instead of ticket['message'] | ✅ |
| 5 — Parse Output | `JSONDecodeError` | Model occasionally returns 'Sure! Here is...' prefix before JSON | ❌ |

## 3. Baseline Accuracy: 4/5 (80%)

| Ticket | Expected | Predicted | Match |
|--------|----------|-----------|-------|
| 101 | Billing | Billing | ✅ |
| 102 | Technical | Technical | ✅ |
| 103 | Account | General | ❌ |
| 104 | General | General | ✅ |
| 105 | Billing | Billing | ✅ |

## 4. Open Questions

1. The model confused 'Account' with 'General' on ticket 103. Would adding a few-shot example for Account changes fix this?
2. Parse Output has no fallback — what happens if the model wraps JSON in markdown fences (```json ... ```)?
3. We tested on 5 tickets. Is 5 enough to trust the accuracy, or do we need 20+?
4. Should we add a 'confidence' threshold and route low-confidence tickets to a human?
5. The current pipeline processes tickets one at a time. Will this be too slow for 1,000 tickets?
