# Technical Architecture: Quick Win 1 — Capped Max Buffer Strategy

**System Owner:** Candidate (Senior PM, AI OS)
**Architecture Type:** Logic-Layer Extension
**Date:** March 24, 2026

---

## 1. Logic Overview
This quick win is a data-driven adjustment to the existing **Pricing Engine** logic. It does not require new ML models, but rather a "Buffer Layer" based on historical variance analysis.

---

## 2. Data Flow (ASCII)

```
[ Practice Area Config ] ----> [ Variance Lookup Table ]
           |                           |
           v                           v
[ Intake Logic ] --------> [ Buffer Calculator ] ----> [ UI: Capped Max Quote ]
                                       |
                                       v
                             [ Transactional DB ] <---- [ Human Adjustment ]
                                       |
                                       v
                             [ Savings Notification Service ]
```

---

## 3. Key Components

### A. Variance Lookup Table (JSON/Static)
- Maps high-variance Practice Areas to their 90th percentile "Price Creep" buffer.
- Example: `{ "Conveyancing": 1.25, "Probate": 1.30, "Employment_SLA": 1.00 }` (where 1.25 = +25% buffer).

### B. Buffer Calculator (API Helper)
- intercepts the standard "Base Quote" and multiplies it by the `variance_factor`.
- `Final_Quote = Base_Fee * (1 + 90th_Percentile_Variance)`.

### C. Savings Notification Trigger
- Listens for a `MATTER_VERIFIED` event where `Actual_Fee < Initial_Max_Quote`.
- Generates the payload for the Notification Service: `{ "user_id": 123, "savings_amount": 150.00, "percent_saved": 25 }`.

---

## 4. Implementation Speed
- **Effort:** Low (2-3 engineering days).
- **Risk:** Low (Logic-only change with no model training required).
