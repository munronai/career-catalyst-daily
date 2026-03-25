# User Stories: Quick Win 1 — Capped Max Buffer Strategy

**Project:** Quote Precision AI Auditor (Quick Win 1)
**Candidate:** Senior PM (AI OS)
**Date:** March 24, 2026

---

## 1. The "Maximum Certainty" Quote
**As a** prospective client in a high-variance category (e.g., Conveyancing),
**I want to** see the maximum possible fee upfront,
**So that** I have absolute budget certainty and no "hidden surprises" later.

- **Given** I am in the intake flow for a property sale,
- **When** the system identifies this as a "High-Variance" category,
- **Then** the UI should display: "Maximum Fixed Fee: £[Capped Amount]",
- **And** it should explicitly state: "Subject to review. We aim to drive this cost down for you."

---

## 2. The "Savings Delight" Notification
**As a** Lawhive client,
**I want to** be notified proactively when my actual case complexity is lower than the initial max quote,
**So that** I feel the firm is honest and looking out for my best interests.

- **Given** I have paid an initial deposit based on the "Capped Max" quote,
- **When** the human solicitor confirms the final matter complexity is "Standard" (lower than the cap),
- **Then** the system should trigger a "Lawhive Savings" email/SMS,
- **And** the message should state: "Great news! We've saved you £[Amount] (X%) vs. your initial quote."

---

## 3. The "Solicitor Adjustment" Workflow
**As a** Lawhive solicitor,
**I want to** easily adjust the fee downwards from the "Capped Max,"
**So that** I can focus on legal work rather than manual refund/credit processing.

- **Given** I am reviewing a case with a "Capped Max" status,
- **When** I determine the work is less complex than the 90th percentile buffer,
- **Then** I should be able to click a "Confirm Lower Complexity" button,
- **And** the system should automatically calculate the delta and update the client's final bill.
