# Technical Specification: GaaS FHIR Gateway

## 1. System Architecture
The GaaS Gateway is a stateless, event-driven middleware that bridges the Genomics England (GEL) Unified Genomic Record with Primary Care EHRs via HL7 FHIR R4.

```mermaid
graph TD
    subgraph GP_EHR [GP Clinical System (EMIS/SystmOne)]
        Prescribing[Prescribing Module]
        CDS_Hooks[CDS-Hooks Client]
    end

    subgraph GAAS_GATEWAY [GaaS FHIR Gateway]
        Auth[OAuth2/Smart-on-FHIR]
        Mapper[FHIR-to-GEL Mapper]
        Rules[Clinical Rules Engine]
    end

    subgraph GEL_BACKEND [GEL Core Infrastructure]
        UGR[Unified Genomic Record]
        LabAPI[Lab Order Management]
    end

    Prescribing -->|Trigger| CDS_Hooks
    CDS_Hooks -->|Check| Auth
    Auth -->|Authorize| Mapper
    Mapper -->|Query| UGR
    UGR -->|Variant Data| Rules
    Rules -->|Alert/CDS Card| CDS_Hooks
    CDS_Hooks -->|Render UI| Prescribing
```

## 2. Component Breakdown
### 2.1. FHIR API Layer
*   **Standard:** HL7 FHIR R4.
*   **Resources Supported:**
    *   `Patient`: Demographics and NHS Number lookup.
    *   `MedicationRequest`: For PGx alert triggers.
    *   `Observation`: For genomic variants and lab results.
    *   `ClinicalImpression`: For recommendations/alerts.

### 2.2. Clinical Rules Engine
*   **Engine:** Based on OpenCDS or a custom lightweight Python engine.
*   **Knowledge Base:** Clinical Pharmacogenetics Implementation Consortium (CPIC) guidelines and UK Genomic Test Directory rules.
*   **Logic:** Executes "If [Drug X] and [Variant Y] then [Recommendation Z]".

### 2.3. Data Mapping Layer
*   **Function:** Converts internal GEL VCF/JSON formats into standardized FHIR `Observation` bundles.
*   **Standardization:** Uses LOINC for genomic tests and HGVS for variant nomenclature.

## 3. API Design (CDS-Hooks Example)
### Trigger: `medication-prescribe`
**Request (from EHR):**
```json
{
  "hook": "medication-prescribe",
  "hookInstance": "d347-123",
  "context": {
    "patientId": "NHS-883746",
    "medications": [
      {
        "resourceType": "MedicationRequest",
        "medicationCodeableConcept": {
          "coding": [{"system": "http://snomed.info/sct", "code": "312342004", "display": "Clopidogrel"}]
        }
      }
    ]
  }
}
```

**Response (from GaaS):**
```json
{
  "cards": [
    {
      "summary": "Genomic Alert: High Risk of Treatment Failure",
      "indicator": "warning",
      "detail": "Patient is a CYP2C19 Poor Metabolizer. Clopidogrel may be ineffective. Consider Prasugrel or Ticagrelor.",
      "source": {"label": "Genomics England GaaS"},
      "suggestions": [
        {
          "label": "Switch to Prasugrel",
          "actions": [{"type": "create", "description": "Update prescription to Prasugrel 10mg"}]
        }
      ]
    }
  ]
}
```

## 4. Security & Authentication
*   **Auth:** Smart-on-FHIR (OAuth2 + OIDC).
*   **Identity:** Integration with NHS CIS2 (Care Identity Service) for GP authentication.
*   **Encryption:** TLS 1.3 in transit; AES-256 at rest.

## 5. Performance Targets
*   **Gateway Latency:** <300ms.
*   **End-to-End Latency (including GEL backend):** <1000ms.
*   **Availability:** 99.9% (Tier 1 Clinical Service).
