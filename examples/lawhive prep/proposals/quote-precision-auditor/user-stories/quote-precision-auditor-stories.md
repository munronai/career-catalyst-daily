# User Stories: Quote Precision AI Auditor

**Project:** Quote Precision AI Auditor
**Candidate:** Senior PM (AI OS)
**Date:** March 24, 2026

---

## 1. The "Immediate Quote" (Happy Path)
**As a** prospective client,
**I want to** receive an accurate fixed-fee quote immediately for my simple legal matter,
**So that** I can proceed with confidence and peace of mind.

- **Given** I have provided all standard intake information and uploaded a clear witness statement,
- **When** the Lawrence AI model detects no high-complexity signals (e.g., <2 entities, standard UK jurisdiction),
- **Then** the AI Auditor should calculate a low variance score (<20%),
- **And** the system should issue an immediate fixed-fee quote with a "Standard" complexity badge.

---

## 2. The "Verified Quote" (High-Variance Routing)
**As a** prospective client with a complex legal matter,
**I want to** be informed that my case is being verified for pricing accuracy,
**So that** I don't receive a quote that shifts after I've made a payment.

- **Given** I have uploaded a document mentioning "multiple business entities" and "international assets,"
- **When** the AI Auditor detects a high variance score (>20% probability of pricing shift),
- **Then** the system should show a "Verification in Progress" message (est. 15 mins),
- **And** the case should be auto-routed to the Intake Solicitor's high-priority queue.

---

## 3. The "Intake Audit" (Lawyer Sign-off)
**As an** intake solicitor,
**I want to** quickly verify and sign off on a complex case quote,
**So that** I can maintain high-volume matter through-put without missing critical pricing details.

- **Given** a new "High-Variance" case has been routed to my dashboard,
- **When** I open the case view and see the "Auditor Signal Highlights" (e.g., "Latent Complexity: Contested Boundary detected in Photo-4"),
- **Then** I should be able to confirm or adjust the suggested fixed fee in <60 seconds,
- **And** upon clicking "Issue Verified Quote," the client should be notified immediately.

---

## 4. The "Transparency Badge" (User Trust)
**As a** prospective client,
**I want to** understand *why* my quote is higher than a standard case,
**So that** I feel the pricing is fair and based on the actual complexity of my matter.

- **Given** the AI Auditor has flagged my case as "High Entity Count,"
- **When** my verified quote is issued,
- **Then** the UI should display a "Complexity Reason" (e.g., "Complexity: Enhanced entity verification required for 3+ defendants"),
- **And** the quote should explicitly state: "This is a Verified Fixed Fee—Our first price is our last price."

---

## 5. The "Feedback Loop" (ML Training)
**As a** Lawhive operations manager,
**I want to** see the delta between AI-suggested quotes and human-verified quotes,
**So that** we can continuously improve the accuracy of our automated pricing model.

- **Given** a human solicitor has adjusted a quote by >15% from the AI's initial suggestion,
- **When** the case is marked as "Quote Released,"
- **Then** the system should log the signal data and the solicitor's adjustment reason to the "Variance Training Log,"
- **And** this data should be used in the next fine-tuning cycle for the Auditor model.
