# User Stories: Lolly Trust Infrastructure

## 1. Trust Portal: Document Access
**Story:** As an Enterprise Compliance Officer, I want to download Lolly's latest ISO 42001 AI Impact Assessment so that I can approve the procurement of LollySense kiosks.

**Scenario: Successful Document Retrieval**
*   **Given** I am logged into the Lolly HQ Trust Portal with a "Compliance Officer" role
*   **When** I navigate to the "AI Governance" section
*   **And** I select the "AI Impact Assessment (AIIA) - LollySense v4"
*   **Then** the document is downloaded as a digitally signed PDF
*   **And** an entry is recorded in the audit log showing I accessed this document.

---

## 2. Governance API: Bias Check Header
**Story:** As a Third-party Developer, I want to see the bias check status for an age verification request so that I can display a "Trust Badge" in my custom app UI.

**Scenario: API Response with Governance Metadata**
*   **Given** I have a valid API key with "Trust Access" enabled
*   **When** I call the `/v1/ai/verify-age` endpoint with a facial image
*   **Then** the response includes the `X-Lolly-Governance` header
*   **And** the header contains a `bias_check_status: "PASS"` field
*   **And** the `decision_confidence` is provided as a float between 0 and 1.

---

## 3. Trust Dashboard: Real-time Bias Visualization
**Story:** As a University EDI Board Member, I want to see a visualization of AI tray-scanning accuracy across different student demographics so that I can be sure the system is fair.

**Scenario: Viewing the Bias Dashboard**
*   **Given** I am viewing the Lolly HQ Trust Dashboard
*   **When** I select the "Tray Scanning - Fairness Metrics" view
*   **Then** I see a bar chart comparing accuracy rates for different demographic cohorts (e.g., Age, Gender, Ethnicity - anonymized)
*   **And** the chart displays the "Industry Benchmark" alongside Lolly's performance
*   **And** any deviations >5% are flagged for review.

---

## 4. Audit Log: AI Decision Traceability
**Story:** As a Legal Counsel for a Stadia operator, I want to retrieve the "Explanability" data for a specific failed age verification so that I can handle a customer complaint.

**Scenario: Fetching Audit Data for a Specific ID**
*   **Given** I have the `audit_log_ref` from a specific transaction
*   **When** I query the `/v1/audit/ai-decisions/{ref_id}` endpoint
*   **Then** the response returns the feature weights and logic used by the AI model for that specific decision
*   **And** the data shows whether a "Human-in-the-Loop" override was performed.
