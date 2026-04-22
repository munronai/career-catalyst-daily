# Discovery Report: Genomics-as-a-Service for Primary Care

## Overview
Genomics England (GEL) and the NHS Genomic Medicine Service (GMS) are transitioning genomics from a specialist-led clinical function to a "mainstreamed" community health capability by 2026. This shift aims to integrate genomic insights into Primary Care (Neighborhood Health Teams) to improve prescribing safety, risk stratification, and early diagnosis.

## 1. The Problem: "Downstream" Bottlenecks
*   **Specialist Dependency:** Genomics is currently trapped in Tertiary care (hospitals), requiring complex referrals that delay diagnosis.
*   **Prescribing Risks:** GPs lack real-time access to pharmacogenomic data, leading to avoidable Adverse Drug Reactions (ADRs) costing the NHS ~£2.2bn annually.
*   **Fragmented Data:** Genomic results often exist as PDF reports outside the Primary Care Electronic Health Record (EHR), making them non-actionable for GPs.
*   **Diagnostic Odyssey:** Rare disease patients wait years for diagnosis; early primary care awareness is the missing link.

## 2. The 2026 Opportunity: Neighborhood Health
The "Neighbourhood Health" initiative aims to decentralize care. Genomics acts as a "multiplier" for this goal by:
*   **Pharmacogenomics (PGx):** Real-time prescribing alerts (e.g., for statins, antidepressants, clopidogrel).
*   **Risk-Based Screening:** Using Polygenic Risk Scores (PRS) and known variants (Lynch, FH) to tailor screening at the GP level.
*   **Digital Integration:** Moving from PDFs to FHIR-compliant data streams.

## 3. Targeted Tech & Standards
| Component | Status/Requirement | Purpose |
| :--- | :--- | :--- |
| **HL7 FHIR R4** | Mandatory Standard | Interoperability between GEL, GMS, and GP Systems (EMIS/TPP). |
| **GOMS API** | National Rollout 2026 | Genomic Order Management Service for digital test requesting. |
| **Genomic Alerts** | Development Phase | CDS (Clinical Decision Support) hooks for real-time alerts. |
| **Unified Genomic Record**| Pilot Phase | A single source of truth for genomic data. |

## 4. Key Discovery Findings
*   **GP Literacy:** GPs require "low-friction" tools—genomics must be a "background service," not an extra task.
*   **Actionability:** A genomic result is useless to a GP unless it comes with a "Next Step" recommendation (e.g., "Reduce dose to 20mg").
*   **Scale:** By 2026, the NHS expects thousands of tests per month to originate from Primary Care.

## 5. Areas of Concern
*   **Interoperability:** Ensuring the "Genomics Gateway" can talk to legacy GP systems.
*   **Ethics & Trust:** Managing patient consent for "upstream" genomic data usage.
*   **Resource Gap:** GPs are overstretched; the service must be lightweight and automated.
