# User Stories: Self-Serve Airlock API

## US-1: Pre-flight Validation (Happy Path)
**As a** Researcher 
**I want to** validate my CSV export locally
**So that** I know it will pass the official airlock without waiting 4 days for feedback.

*   **Scenario:** Successful Pre-flight check
    *   **Given** I have a results file `summary_stats.csv` with 1,000 rows
    *   **And** the file contains no PII and all cell counts are > 5
    *   **When** I call `POST /v1/validate` with the file
    *   **Then** I should receive a `status: PASS` response
    *   **And** the response should include a `validation_token` for submission.

## US-2: PII Detection (Fail Case)
**As a** Researcher 
**I want to** be notified of specific privacy violations
**So that** I can fix them immediately.

*   **Scenario:** PII detected in output
    *   **Given** I have a results file `results.csv`
    *   **And** row 402 accidentally contains a Participant ID `GEL-123456`
    *   **When** I call `POST /v1/validate`
    *   **Then** I should receive a `status: FAIL` response
    *   **And** the report should highlight `Row 402, Column 1` as a `PII_VIOLATION`.

## US-3: Automated Egress (Happy Path)
**As a** Researcher 
**I want to** automatically egress "Safe-by-Default" data
**So that** I can receive my data in minutes.

*   **Scenario:** Auto-approval for low-risk data
    *   **Given** I am submitting a file of type `plot` (PNG)
    *   **And** the YAML policy defines `plots` as `Auto-Approve: True`
    *   **When** I call `POST /v1/egress`
    *   **Then** the API should return `workflow_status: COMPLETED`
    *   **And** the file should be available at my external endpoint within 10 minutes.

## US-4: Differential Privacy Injection
**As an** Airlock Committee Member
**I want** the system to automatically anonymize small cell counts
**So that** we can allow more summary data to be exported safely.

*   **Scenario:** Automated noise injection
    *   **Given** a researcher submits a table with a cell count of 3
    *   **And** the privacy policy requires a minimum count of 5
    *   **When** the Egress API processes the file
    *   **Then** it should apply Laplacian noise to the cell
    *   **And** the output file should be marked as `ANONYMIZED`.

## US-5: AI Model Weight Audit
**As an** AI Researcher
**I want** to export my model weights securely
**So that** I can share my model with the scientific community.

*   **Scenario:** Successful model audit
    *   **Given** I have a PyTorch `.pth` file
    *   **When** I call `POST /v1/validate` with `type: weights`
    *   **Then** the Model Auditor should check for training data leakage
    *   **And** return a `leakage_risk_score` below the threshold of 0.1.
