# Strategy: The Future of Autonomous Egress

## Vision
To create a "Zero-Trust, Zero-Wait" egress infrastructure for Genomics England, where privacy is enforced at the point of computation rather than the point of exit.

## Strategic Alignment
Genomics England is transitioning to a **Federated Data Model in 2026**. In this future state, data will reside in multiple regional and international nodes. A centralized, manual manual airlock team cannot scale to hundreds of nodes. The **Self-Serve Airlock API** is the foundational "connective tissue" that allows decentralized governance.

## Key Strategic Pillars

### 1. Shift-Left Privacy
By providing researchers with a **Pre-flight Validation API**, we move the privacy burden from the *end* of the research lifecycle to the *active development* phase. Researchers can iterate on their code to ensure outputs are compliant from the start.

### 2. Privacy-as-Code (PaC)
We will move away from PDF-based "Airlock Guidelines" toward executable YAML policies.
- **Old Way:** "Please ensure your table doesn't have small cell counts."
- **New Way:** `policy: { min_cell_count: 5, action: "auto_redact" }`
This ensures consistency across different research cohorts (e.g., Cancer vs. Rare Disease).

### 3. Trust but Verify
The API doesn't replace the Airlock Committee; it **empowers** them. By automating 80% of routine requests (e.g., summary statistics, aggregate counts), the Committee can focus their expertise on high-risk, high-value exports like novel AI architectures.

## Strategic Assumptions
1. **Assumption:** GEL's 2026 federated partners will accept an automated, API-driven governance model if it meets the ISO 27001 / Cyber Essentials Plus standards.
2. **Assumption:** Researchers are willing to adapt their workflows (e.g., using specific file formats) in exchange for near-instant egress.
3. **Assumption:** The volume of AI/ML research will continue to grow, necessitating non-tabular privacy auditing.

## Long-term Impact
By EOFY 2027, this API will enable GEL to participate in **Cross-Border Federated Analysis** (e.g., with UK Biobank and EU Genomic Health Data Space) by providing a standardized, machine-readable egress handshake. This positions GEL as the global leader in "Privacy-Preserving Genomic Research."
