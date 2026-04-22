# User Stories: Genomics-as-a-Service (GaaS)

## 1. General Practitioner (GP) Flows

### Story 1: Pharmacogenomic Alerting
**As a** GP
**I want** to be alerted if a patient has a genetic variant that makes a drug unsafe
**So that** I can avoid prescribing medication that causes an adverse reaction.

*   **Scenario: Prescribing Clopidogrel to a "Poor Metabolizer"**
    *   **Given** a patient has a CYP2C19 *2/*2 variant in their Unified Genomic Record
    *   **When** I attempt to prescribe Clopidogrel in EMIS
    *   **Then** the GaaS Gateway should trigger a "High Risk" alert card
    *   **And** recommend an alternative like Prasugrel.

### Story 2: Digital Test Ordering
**As a** GP
**I want** to order a genomic test directly from my clinical system
**So that** I don't have to fill out paper forms or log into external portals.

*   **Scenario: Ordering a test for Familial Hypercholesterolemia (FH)**
    *   **Given** I am in the patient's record
    *   **When** I search for "FH Genomic Test" in the digital directory
    *   **Then** the system should pre-populate the FHIR `ServiceRequest` with patient demographics
    *   **And** send the request directly to the GEL Lab API.

---

## 2. Patient Flows

### Story 3: Viewing Recommendations via NHS App
**As a** patient
**I want** to see my genomic recommendations in my NHS App
**So that** I can understand my risks and share them with other clinicians.

*   **Scenario: Accessing PGx data after a pharmacy visit**
    *   **Given** a genomic prescribing recommendation has been saved to my record
    *   **When** I log into the NHS App and navigate to "My Health Record"
    *   **Then** I should see a section for "Genomic Insights"
    *   **And** see a summary of my drug-gene interactions (e.g., "Always inform your dentist about your genetic status for local anesthetics").

---

## 3. Neighbourhood Health Lead Flows

### Story 4: Population Risk Dashboarding
**As a** Neighbourhood Health Lead
**I want** to see an anonymized view of genomic risk across my practice list
**So that** I can allocate resources to proactive screening programs.

*   **Scenario: Identifying an FH cluster**
    *   **Given** the GaaS Gateway is active across 5 practices
    *   **When** I access the "Neighbourhood Risk Dashboard"
    *   **Then** I should see the total count of patients with known FH-causing variants
    *   **And** be able to trigger a bulk invitation for clinical review for those not yet on statins.
