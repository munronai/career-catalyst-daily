# One-Pager: Self-Serve Airlock API

## The Hook
Transforming the Genomics England Airlock from a 15-day "Black Box" into a real-time, self-serve validation engine.

## The Problem
Egressing research results from Genomics England (GEL) currently takes 4–15+ days due to a manual-heavy review process. Automated scanners are over-sensitive, flagging safe genomic data as "high-risk" and forcing human intervention. As GEL moves to a federated model in 2026, this bottleneck will stifle innovation across decentralized nodes.

## The Solution: The "Self-Serve Airlock" API
An API-first egress layer that provides researchers with:
1.  **Pre-flight Validation:** A local-running or API-based scanner that identifies privacy violations *before* submission.
2.  **Privacy-as-Code (PaC):** Declarative guardrails that allow automated approval for common summary statistics and AI model weights.
3.  **Differential Privacy Integration:** Automated noise injection for summary results to guarantee anonymity without manual inspection.

## The Value
- **50% Reduction in Manual Review:** By moving from "review everything" to "exception-based review."
- **Real-time Feedback:** Researchers receive instant validation reports, reducing the current 4-day feedback loop to seconds.
- **Federation Ready:** A portable API that can be deployed across federated nodes to ensure consistent data governance.
- **Improved Security:** Standardized, machine-readable privacy policies replace inconsistent human interpretation.

## Success Metric
**Decrease "Time to Egress" for Standard Requests from 6 days to <1 hour by EOFY 2026.**
