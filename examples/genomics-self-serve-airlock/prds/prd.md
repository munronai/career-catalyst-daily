# PRD: Self-Serve Airlock API

## 1. Objectives
- **Automate** the privacy review of research outputs to reduce human dependency.
- **Provide** instant feedback to researchers on egress eligibility.
- **Standardize** privacy policies as machine-readable code.
- **Support** the 2026 Federated Data Model.

## 2. User Roles
- **Researcher:** Submits data for egress, wants fast approval.
- **Airlock Committee Member:** Defines privacy policies, handles exceptions.
- **Platform Engineer:** Integrates API into the Trusted Research Environment (TRE).

## 3. User Flows

### 3.1 Pre-flight Validation (Researcher)
1. Researcher finishes analysis in the TRE.
2. Researcher calls `POST /v1/validate` with their output file.
3. API returns a **Validation Report** within 60 seconds.
4. If "PASS", the researcher can proceed to egress.
5. If "FAIL", the report highlights specific lines/values (e.g., "Potential Participant ID at Row 402").

### 3.2 Automated Egress (Standard Request)
1. Researcher submits file via `POST /v1/egress`.
2. API applies **Privacy-as-Code** rules (e.g., "Max N=10 for summary tables").
3. API applies **Differential Privacy** noise if required.
4. File is automatically moved to the external MFT (Managed File Transfer) endpoint.
5. Researcher receives a notification: "Egress Approved & Completed."

## 4. Functional Requirements

| ID | Feature | Description |
| :--- | :--- | :--- |
| FR-1 | PII Scanner | Multi-threaded regex and ML-based scanner to detect Participant IDs, NHS numbers, and PII. |
| FR-2 | Privacy-as-Code Engine | YAML-based policy engine to define what data types are "Safe-by-Default." |
| FR-3 | Differential Privacy | Integrated library (e.g., Google's Differential Privacy) to anonymize low-count summary stats. |
| FR-4 | Model Weight Auditor | Specialized parser for PyTorch/TensorFlow weights to check for training data leakage. |
| FR-5 | Audit Logging | Immutable log of all validation attempts and egress results for compliance. |

## 5. Non-Functional Requirements
- **Latency:** Validation of <1GB files must take <2 minutes.
- **Scalability:** Must handle 500+ concurrent validation requests in a federated environment.
- **Security:** API must reside within the GEL secure boundary; no data leaves the boundary during validation.

## 6. Success Metrics
- **Manual Review Rate:** Reduce from 90% of requests to <45% within 12 months.
- **Researcher NPS:** Increase score for "Ease of Egress" by 40 points.
- **Cycle Time:** Reduce average egress time for "Safe" requests from 5 days to <30 minutes.
