# Research & Discovery: Genomics England "Self-Serve Airlock" API

## Problem Statement
The Genomics England Airlock process, while designed for security, has become a significant bottleneck for researchers. Despite the introduction of "automated" checks, manual intervention remains high (triggering reviews for safe data), and the system struggles with modern research outputs like AI model weights. With the move to a federated model in 2026, the current manual-heavy process is unsustainable.

## Data Points (April 2026)

| Request Type | Target (Working Days) | Actual (Working Days) | Delay Factor |
| :--- | :--- | :--- | :--- |
| Standard (Summary Stats) | 2 | 4–6 | Heuristic Over-sensitivity |
| Complex (AI/ML/Individual) | 10 | 15+ | Manual SME Intervention |
| Tier 1/2 (High Risk) | N/A | Variable | Mandatory Human Review |

## Primary Bottlenecks

### 1. Heuristic Over-Sensitivity (False Positives)
The automated system uses conservative regex and heuristic patterns to find Participant IDs. In high-dimensional data, common genomic coordinates (e.g., `chr1:12345`) or variant nomenclature are frequently flagged as sensitive, forcing a manual review that adds 2–3 days to the timeline.

### 2. AI & ML Model Complexity
Phase 2 AI Airlock requests (exporting model parameters) often "get stuck" because the scanner cannot effectively parse non-tabular binary files for hidden leakage. This results in 100% of these requests being diverted to the SME queue.

### 3. Federated Scalability Issues
As data remains in decentralized nodes (Federated Model 2026), egressing results across multiple jurisdictional boundaries requires a standardized "Privacy-as-Code" API that can be enforced locally.

## Areas of Concern
- **Researcher Friction:** Prolonged wait times delay clinical translations and publication cycles.
- **Operational Cost:** High ratio of manual output checkers to requests.
- **Technical Debt:** The current scanner is a "Black Box" to researchers; they only find out their file failed *after* a 4-day wait.

## Proposed Value
Reducing manual review by 50% via **Automated Privacy Guardrails** (Privacy-as-Code) and a **Pre-flight Check API** that allows researchers to validate files *before* submission.
