# User Stories: Quick Win 2 — Range-Based Expectation Management

**Project:** Quote Precision AI Auditor (Quick Win 2)
**Candidate:** Senior PM (AI OS)
**Date:** March 24, 2026

---

## 1. The "Professional Range" Intake
**As a** client with a complex legal matter (e.g., multi-party dispute),
**I want to** receive a likely price range rather than a "guess,"
**So that** I feel the firm is taking the complexity of my case seriously.

- **Given** Lawrence has flagged my case as "High Complexity" (e.g., entity count > 3),
- **When** I reach the pricing screen,
- **Then** the UI should display a range: "Estimated Range: £[Min] – £[Max]",
- **And** it should show a commitment: "Our specialists will verify a final price for you within 4 hours."

---

## 2. The "SLA Countdown" Dashboard
**As a** prospective client waiting for a verified quote,
**I want to** see the progress of my quote review,
**So that** I don't feel "lost in the machine" while waiting.

- **Given** I have submitted my case for a "Range Quote" review,
- **When** I visit my dashboard,
- **Then** I should see an "SLA Countdown Timer" (e.g., "Ready in: 2h 15m"),
- **And** I should see a status: "Solicitor Review in Progress."

---

## 3. The "Priority Queue" (Solicitor View)
**As an** intake solicitor,
**I want to** see which "Range Quotes" are closest to their 4-hour SLA deadline,
**So that** I can prioritize the right cases and maintain our service commitment.

- **Given** I am in the Intake Dashboard,
- **When** I filter by "Awaiting Verification,"
- **Then** cases should be sorted by "Time Remaining in SLA" (ascending),
- **And** cases with <1 hour remaining should be highlighted in red.
