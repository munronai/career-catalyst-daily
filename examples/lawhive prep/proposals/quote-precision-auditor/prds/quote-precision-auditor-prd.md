# PRD: Quote Precision AI Auditor

**Product Owner:** Candidate (Senior PM, AI OS)
**Status:** Draft / Proposal
**Date:** March 24, 2026

---

## 1. Product Objective
Develop a proactive auditing layer within the Lawhive intake flow that identifies high-complexity matters *before* fixed-fee quotes are issued, thereby eliminating pricing discrepancies and improving customer trust.

---

## 2. Key User Personas
1. **The Prospective Client:** Seeking an immediate, reliable quote for legal work without "hidden surprises."
2. **The Intake Solicitor:** Needs to verify high-complexity cases quickly without being a bottleneck for simple ones.
3. **Lawhive Operations:** Focused on maintaining high realization rates and firm profitability.

---

## 3. Functional Requirements

### 3.1 Complexity Signal Extraction (Intake Flow)
- **FEAT-1:** Extract key variance signals from user input (e.g., "Multiple Defendants," "Cross-Border," "Deceased Estate Details") using the `Lawrence` AI model.
- **FEAT-2:** Analyze uploaded evidence (PDFs, photos, emails) for latent complexity indicators (e.g., handwritten boundary notes in property disputes).

### 3.2 Variance Prediction Engine (The Auditor)
- **FEAT-3:** Score each case against a **Historical Variance Model** (trained on past Lawhive matters where quotes were adjusted).
- **FEAT-4:** Trigger a "Pre-Quote Review" flag if the predicted variance probability exceeds 20%.

### 3.3 Dynamic Routing & Verification
- **FEAT-5:** Auto-route "High-Variance" cases to a dedicated **Intake Audit Dashboard** for a human lawyer's 60-second verification.
- **FEAT-6:** Provide the lawyer with " Lawrence's Evidence Highlights" to accelerate the sign-off process.

---

## 4. User Flow
1. **User** enters case details and uploads initial evidence.
2. **Lawrence** extracts signals and passes them to the **AI Auditor**.
3. **Auditor** calculates a **Complexity Score** and **Variance Probability**.
4. **If Low Variance:** Immediate fixed-fee quote is issued to the User.
5. **If High Variance:**
    - User is shown: "We're just verifying a few details to ensure your quote is 100% accurate (est. 15 mins)."
    - **Intake Solicitor** receives a Slack notification/Dashboard alert.
    - **Solicitor** verifies/adjusts quote and clicks "Issue Quote."
    - User receives a "Verified Fixed Fee" notification.

---

## 5. Success Metrics (KPIs)
- **Primary:** Rate of post-issuance quote adjustments (Target: <2%).
- **Secondary:** User intake completion rate for high-complexity cases.
- **Secondary:** Time-to-quote for audited cases (Target: <30 minutes).

---

## 6. Assumptions & Constraints
- **Assumption:** Lawrence is capable of extracting multi-entity signals from messy legal documents with >90% accuracy.
- **Constraint:** We must not sacrifice the "Immediate Quote" experience for standard, low-complexity cases.
