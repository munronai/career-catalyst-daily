# Discovery Report: Multi-Omics "Data Connect" Hub

## 1. Overview
This report investigates the current friction in joining genomics, digital pathology, and primary care records within Genomics England, and evaluates the GA4GH Data Connect standard as a solution for building a unified "Patient Data Object" API.

## 2. Market/Field Analysis: The "Join" Problem

| Data Type | Primary Source | Current Format | Scalability Bottleneck |
| :--- | :--- | :--- | :--- |
| **Genomics** | Whole Genome Sequencing | VCF, BAM, CRAM | Massive file sizes; variant interpretation latency. |
| **Digital Pathology** | Tissue Biopsy Scans | DICOM, WSI (SVS) | Whole Slide Images (WSI) are 1GB+ each; lack of unified metadata. |
| **Primary Care** | EHR / GP Records | FHIR, HL7, SQL | Fragmented schemas; semantic misalignment across providers. |

### Areas of Concern (Pain Points)
1. **Manual Data Wrangling:** Researchers spend 60-80% of their time "joining" datasets using custom scripts rather than performing analysis.
2. **Infrastructure Strain:** Storing and moving massive WSI and Genomic files is cost-prohibitive for individual research projects.
3. **Privacy Silos:** Sensitive primary care data is often locked behind different governance layers than genomic data.

## 3. Technical Solution: GA4GH Data Connect
The GA4GH Data Connect standard provides a middleware layer that abstracts these disparities.

| Feature | Data Connect Capability | Value to Researcher |
| :--- | :--- | :--- |
| **Table API** | Describes datasets via JSON Schema. | Discover what fields exist (e.g., `smoker_status`, `variant_id`) without downloading data. |
| **Search API** | Standard SQL interface (`SELECT...WHERE`). | Join pathology features with genetic variants using familiar syntax. |
| **Federation** | Queries distributed across repositories. | "Single pane of glass" view across separate cloud buckets or on-prem servers. |

## 4. Key Findings & Recommendations
- **Finding 1:** Digital Pathology is currently the "dark data" of the omics world; it is rarely queryable alongside genomics at the record level.
- **Finding 2:** GA4GH Data Connect is "schema-agnostic," meaning we can model a "Patient Data Object" that includes pointers to massive files (WSI/VCF) while keeping searchable metadata in high-speed tables.
- **Recommendation:** Implement a **"Data Product" model** where each research cohort is exposed as a Data Connect Table, pre-joining genomics, pathology, and EHR metadata.
