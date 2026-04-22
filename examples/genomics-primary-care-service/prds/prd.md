# PRD: Genomics-as-a-Service (GaaS) Gateway

## 1. Executive Summary
The GaaS Gateway is a FHIR-compliant service layer that enables Primary Care clinicians to access, order, and act upon genomic data within their existing Electronic Health Records (EHR).

## 2. Objectives
*   **Enable Mainstreaming:** Move genomic clinical decision support into the "Neighbourhood Health" tier by 2026.
*   **Automate Safety:** Implement FHIR-based "Pharmacogenomic Alerts" for high-risk prescriptions.
*   **Standardize Data:** Use HL7 FHIR R4 to ensure interoperability between Genomics England and GP systems.

## 3. Target Users
*   **General Practitioners (GPs):** Receive alerts and order tests.
*   **Neighborhood Health Leads:** Monitor population-level genomic risk (e.g., FH prevalence).
*   **Patients:** View their genomic recommendations via the NHS App.

## 4. User Flows
### Flow A: The Pharmacogenomic Alert
1. GP selects a drug (e.g., Clopidogrel) in EMIS.
2. EHR sends a FHIR `MedicationRequest` to GaaS Gateway.
3. GaaS Gateway checks the Unified Genomic Record.
4. GaaS returns a `ClinicalImpression` with a "High Risk" alert and dose recommendation.
5. GP adjusts the prescription based on the alert.

### Flow B: Proactive Risk Screening
1. GaaS Gateway identifies patients in a practice list with Polygenic Risk Scores (PRS) in the top 5% for Type 2 Diabetes.
2. GaaS pushes a "Proactive Review" task to the GP's clinical inbox.
3. GP invites the patient for a targeted screening.

## 5. Functional Requirements
| ID | Requirement | Priority |
| :--- | :--- | :--- |
| **FR1** | FHIR R4 API for `Patient`, `Observation`, and `DiagnosticReport`. | P0 |
| **FR2** | Integration with National Genomic Test Directory for digital ordering. | P0 |
| **FR3** | CDS-Hooks support for real-time prescribing alerts. | P1 |
| **FR4** | OAuth2/Smart-on-FHIR authentication for clinical users. | P0 |
| **FR5** | Population health dashboard for Neighborhood Health Leads. | P2 |

## 6. Non-Functional Requirements
*   **Latency:** Alerts must return in <500ms to avoid clinical workflow disruption.
*   **Security:** Full compliance with NHS Data Security and Protection Toolkit (DSPT).
*   **Scalability:** Support 50,000 concurrent GP sessions.

## 7. Success Metrics
*   **Adoption Rate:** % of GP practices with GaaS active.
*   **Alert Actionability:** % of genomic alerts that result in a prescription change.
*   **Test Volume:** Growth in genomic tests ordered directly from Primary Care.
