# User Stories: Multi-Omics Hub

## Story 1: Multimodal Cohort Discovery
**As a** Cancer Researcher
**I want to** query patients who have a specific genetic mutation and a high-grade pathology score
**So that** I can build a cohort for a new clinical trial.

**Gherkin:**
- **Given** the Multi-Omics Hub is connected to the 'genomics_v1' and 'pathology_v1' tables
- **When** I submit a SQL query joining these tables on 'patient_id' where 'gene' is 'TP53' and 'histology_grade' > 3
- **Then** I should receive a JSON list of matching patient IDs with their respective metadata
- **And** the query should complete in under 10 seconds.

## Story 2: Longitudinal Analysis with EHR
**As a** Pharmacogenomics Researcher
**I want to** correlate genetic variants with primary care medication history
**So that** I can identify potential adverse drug reactions.

**Gherkin:**
- **Given** I have access to the 'primary_care_v1' table containing prescription history
- **When** I query for patients with the 'CYP2D6' poor metabolizer genotype who were prescribed 'Codeine'
- **Then** the system should return the dates and dosages of those prescriptions alongside the genetic variant details.

## Story 3: Schema Discovery
**As a** Data Scientist
**I want to** explore the available fields in the digital pathology dataset
**So that** I can design my machine learning feature set.

**Gherkin:**
- **Given** I am authenticated with the Data Connect API
- **When** I request the schema for the 'digital_pathology' table via the '/info' endpoint
- **Then** I should receive a JSON Schema document listing all available fields, their types (e.g., cell_count: integer), and descriptions.

## Story 4: Handling Massive Files (Edge Case)
**As a** Researcher
**I want to** get the direct download URL for a Whole Slide Image (WSI) after identifying a patient
**So that** I can perform a deep-dive visual analysis.

**Gherkin:**
- **Given** a query has identified Patient 'X' as a person of interest
- **When** I select the 'slide_url' field from the 'pathology_v1' table
- **Then** the API should return a pre-signed, time-limited URL for the massive SVS file in S3.
