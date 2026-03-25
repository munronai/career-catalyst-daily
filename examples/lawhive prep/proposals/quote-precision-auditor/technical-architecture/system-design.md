# Technical Architecture: Quote Precision AI Auditor

**System Owner:** Candidate (Senior PM, AI OS)
**Architecture Type:** Event-Driven AI Service
**Date:** March 24, 2026

---

## 1. System Overview
The Quote Precision AI Auditor is a middleware service that sits between the **Intake Agent (Lawrence)** and the **Pricing Engine.** It performs asynchronous complexity scoring on inbound matter signals to detect high-variance pricing risks.

---

## 2. Component Diagram (ASCII Architecture)

```
[ User UI ] <---- (Quote / Verification Status)
    |
    v
[ Lawrence (Intake Agent) ] ----> [ Document Storage (S3/GCS) ]
    |                               ^
    | (Extracts Signals)            |
    v                               |
[ AI Auditor Service ] <------------+
    | (1. Complexity Scoring)
    | (2. Variance Prediction)
    |
    +---- (If Low Variance) ----> [ Pricing Engine ] ----> [ Immediate Quote ]
    |
    +---- (If High Variance) ---> [ Auditor Dashboard ] ---+
                                    |                      |
                                    v                      |
                             [ Human Solicitor ] <---------+
                                    | (Verify/Adjust)
                                    v
                             [ Pricing Engine ] ----> [ Verified Quote ]
```

---

## 3. Key Component Logic

### A. The Signal Extractor (Lawrence Layer)
- Leverages Lawhive's proprietary legal LLM (`Lawrence`) to perform **Entity & Context Extraction.**
- Outputs a JSON payload of complexity signals:
  - `entity_count`: Integer
  - `jurisdiction_match`: Boolean (Does it match a "Known High-Variance" state?)
  - `latent_complex_keywords`: List (e.g., "probate contest," "joint-boundary," "multi-party")
  - `document_quality_score`: 0-1 (Low scores trigger higher variance probability)

### B. The Variance Prediction Engine
- **Model:** Random Forest or XGBoost Classifier (Trained on historical "Matter Adjustment" logs).
- **Features:** Intake Signals + Historical Matter Realization Rates + Solicitor Availability.
- **Output:** `variance_probability` (0.0 - 1.0).

### C. Governance Layer ([ai-rulez](https://github.com/Lawhive/ai-rulez) Integration)
- The Auditor's "Audit Rules" are managed via Lawhive's open-source [ai-rulez](https://github.com/Lawhive/ai-rulez) framework.
- Allows PMs/Lawyers to update "Complexity Flags" without code changes.
- Ensures cross-platform synchronization of AI instructions (Claude, Cursor, Copilot) as matters evolve.
- Example Rule:
  ```yaml
  name: "Multiple-Defendant-Audit"
  trigger: "signals.entity_count > 2"
  action: "SET status=HIGH_VARIANCE; ROUTE_TO=Intake-Seniors"
  ```

---

## 4. Data Flow: "High-Variance" Scenario
1. **Intake Agent** extracts "3 Defendants" and "Contested Probate" from user chat.
2. **AI Auditor** receives payload, scores it against historical contested probate data.
3. **Engine** calculates `variance_probability = 0.85` (Threshold is 0.20).
4. **Auditor Service** updates the case status to `AWAITING_VERIFICATION` in the DB.
5. **Event Bus** (Kafka/PubSub) triggers a notification to the **Intake Solicitor Dashboard.**
6. **Solicitor** opens the case, sees "Lawrence's Evidence Summary," confirms the £1,500 fixed fee, and hits "Release Quote."
7. **Pricing Engine** issues the final, verified quote to the **User.**

---

## 5. Security & Compliance
- **SOC2 Compliance:** All document analysis happens within Lawhive's private VPC.
- **Redaction Layer:** Lawrence redacts PII before complexity scoring to ensure the Auditor only processes "Structural" metadata.
- **Audit Trail:** Every AI-suggested vs. Human-adjusted quote is logged for downstream training of the Variance Model.
