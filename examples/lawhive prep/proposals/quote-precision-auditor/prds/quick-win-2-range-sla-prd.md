# PRD: Quick Win 2 — Range-Based Expectation Management

**Product Owner:** Candidate (Senior PM, AI OS)
**Status:** Draft / Quick Win
**Date:** March 24, 2026

---

## 1. Product Objective
To manage user expectations for high-complexity cases by replacing instant (often inaccurate) quotes with a "Professional Range" and a committed SLA for a verified final price.

---

## 2. Functional Requirements

### 2.1 Complexity Trigger (Routing)
- **FEAT-Q2.1:** Define a "Complexity Score" threshold (based on entity count, document volume, or practice area) that triggers the Range Quote UI.
- **FEAT-Q2.2:** Automatically bypass the "Instant Quote" engine when this threshold is met.

### 2.2 Range UI/UX
- **FEAT-Q2.3:** Display a "Likely Range" (e.g., £[Min] – £[Max]) based on historical medians for the case type.
- **FEAT-Q2.4:** Display the "Quote SLA Timer" (e.g., *"Our specialists are reviewing your files. Final verified quote in: 3h 45m"*).

### 2.3 SLA Management & Alerts
- **FEAT-Q2.5:** High-priority dashboard for solicitors to "Clear the Range Queue."
- **FEAT-Q2.6:** Escalation alerts to Ops Leads if a range quote exceeds 75% of its SLA time without a final price issuance.

---

## 3. Success Metrics
- **Primary:** User completion rate of "Range Quote" intake flows vs. "Instant Quote" flows.
- **Secondary:** Quote-to-Payment conversion rate.
- **Operational:** Average time-to-final-quote for range-based cases.

---

## 4. Assumptions & Constraints
- **Assumption:** Users with complex cases prefer a "considered" range over a "guessed" flat fee.
- **Constraint:** Range must not be so wide (e.g., £500 – £5,000) that it loses all utility for the user.
