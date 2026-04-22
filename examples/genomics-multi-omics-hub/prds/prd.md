# PRD: Multi-Omics "Data Connect" Hub

## 1. Objectives
- **Standardize Data Access:** Implement the GA4GH Data Connect Table and Search APIs to provide a consistent interface for multimodal data.
- **Enable Multimodal Joins:** Provide a mechanism to query genomics, digital pathology, and primary care data in a single SQL operation.
- **Support Scalability:** Design for the 2026 goal of managing millions of multimodal records.

## 2. User Flows
### Researcher Cohort Discovery
1. **Researcher** logs into the Genomics England Research Environment.
2. **Researcher** sends a SQL query to the `/search` endpoint:
   ```sql
   SELECT p.id, p.genotype, d.pathology_score, e.primary_care_diagnosis
   FROM patient_genomics AS p
   JOIN digital_pathology AS d ON p.id = d.patient_id
   JOIN primary_care AS e ON p.id = e.patient_id
   WHERE p.variant = 'BRCA1' AND d.feature = 'High-Grade'
   ```
3. **API Hub** translates the query, fetches metadata from federated sources, and returns a unified JSON result.

## 3. Functional Requirements
- **FR1: Metadata Abstraction:** The hub must expose metadata from VCF (genomics), DICOM/SVS (pathology), and FHIR/SQL (EHR) as flattened GA4GH Tables.
- **FR2: SQL Query Engine:** Implementation of the GA4GH Search API supporting `SELECT`, `JOIN`, `WHERE`, and `LIMIT`.
- **FR3: Schema Discovery:** `/tables` and `/table/{name}/info` endpoints must return valid JSON Schemas for each dataset.
- **FR4: Virtual Joins:** The system must handle joins across tables that reside in different physical storage locations.

## 4. Success Metrics
- **Mean Time to Query (MTTQ):** Reduced from days (manual) to <10 seconds for multimodal joins.
- **Researcher Satisfaction:** 50% increase in positive feedback regarding data accessibility.
- **Data Utilization:** 30% increase in research projects utilizing more than two data types (e.g., Genomics + Pathology).
