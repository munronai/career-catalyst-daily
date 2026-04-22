# Presentation: Self-Serve Airlock API
**Genomics England: Scaling Egress for the Federated Future**

---

## Slide 1: The Bottleneck
**Egress today is the "Waiting Room" of Genomic Science.**

- **The Problem:** Researchers wait **4–15+ days** to export results.
- **The Cause:** 90% of requests require manual review because automated scanners are "Black Boxes" and over-sensitive.
- **The Risk:** In 2026, a manual process cannot scale to a federated model across multiple nodes.

---

## Slide 2: The Data-Backed Reality
**Current performance vs. Targeted Goals**

| Metric | Current State | With Self-Serve API |
| :--- | :--- | :--- |
| **Standard Egress Time** | 6 Working Days | **< 30 Minutes** |
| **Manual Review Rate** | 90% | **< 45%** |
| **Researcher Feedback Loop** | 4 Days | **Instant (Pre-flight)** |
| **Cost per Egress** | £££ (Manual SME) | **£ (Automated compute)** |

---

## Slide 3: The Solution - "Privacy-as-Code"
**Moving from Manual Inspection to Autonomous Governance.**

1. **Pre-flight Check API:** Validate outputs in real-time *before* submission.
2. **Automated Guardrails:** machine-readable YAML policies define "Safe-by-Design" exports.
3. **Differential Privacy:** Automated noise injection for summary statistics to guarantee anonymity.
4. **AI-Ready:** Specialized auditors for ML model weights and complex outputs.

---

## Slide 4: Technical Execution
**Why this works.**

- **TRE Native:** Deployed inside the secure environment; no data leaks.
- **Language:** Built in Go for high-speed parsing of multi-gigabyte files.
- **Open Standards:** Uses `OpenDP` and `Presidio` for industry-standard PII detection.
- **Federated Ready:** A portable microservice that can be deployed at any federated node (UK Biobank, Regional Genomics Centres).

---

## Slide 5: Impact & ROI
**Unlocking the next wave of Genomic Discovery.**

- **Researcher Velocity:** Accelerates publication and clinical translation cycles by 50%.
- **Operational Savings:** Reallocates Airlock SMEs to higher-value research support.
- **Future Proofing:** The only way to scale egress in a decentralized, federated 2026 ecosystem.
- **Success Criteria:** 50% reduction in manual review by EOFY 2026.
