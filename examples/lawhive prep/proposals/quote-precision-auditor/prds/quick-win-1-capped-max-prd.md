# PRD: Quick Win 1 — The "Capped Max" Buffer Strategy

**Product Owner:** Candidate (Senior PM, AI OS)
**Status:** Draft / Quick Win
**Date:** March 24, 2026

---

## 1. Product Objective
To eliminate negative price-adjustment friction by quoting a "Historical Max" price upfront and utilizing a "Price Drop" notification to delight users when actual complexity is lower.

---

## 2. Functional Requirements

### 2.1 Variance Analysis (Logic Layer)
- **FEAT-Q1.1:** Identify top 3 "High-Variance" practice areas (e.g., Conveyancing, Contested Probate).
- **FEAT-Q1.2:** Calculate the 90th percentile of price increases for these categories over the last 12 months.

### 2.2 Pricing Display Logic
- **FEAT-Q1.3:** For identified categories, display the quote as: *"Maximum Fixed Fee: £[Base + 90th% Buffer]"*.
- **FEAT-Q1.4:** Include mandatory disclaimer: *"Subject to review. Our goal is to drive this cost down; you only pay for the actual complexity detected."*

### 2.3 The "Savings" Notification
- **FEAT-Q1.5:** If a human solicitor confirms a price lower than the "Capped Max," trigger an automated "Lawhive Savings" email/SMS.
- **FEAT-Q1.6:** Display the "Savings Amount" and "% Saved" prominently in the user dashboard.

---

## 3. Success Metrics
- **Primary:** Churn rate post-initial-payment (Target: <5%).
- **Secondary:** User review mentions of "Savings" or "Honest Pricing."
- **Guardrail:** Conversion rate from Intake to Payment (must not drop by >3% due to higher upfront anchor).

---

## 4. Assumptions
- **Assumption:** Users value "Price Certainty" (even at a higher anchor) more than "Low Entry Price" with uncertainty.
- **Assumption:** Our "Max" price is still within the top quartile of market rates.
