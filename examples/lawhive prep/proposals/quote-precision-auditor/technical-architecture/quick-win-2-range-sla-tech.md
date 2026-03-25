# Technical Architecture: Quick Win 2 — Range-Based Expectation Management

**System Owner:** Candidate (Senior PM, AI OS)
**Architecture Type:** State-Machine & Routing Update
**Date:** March 24, 2026

---

## 1. Logic Overview
This win introduces a new "Pending Verification" state to the intake workflow and a basic SLA tracking service. It uses existing Complexity Signals to route traffic.

---

## 2. Component Diagram (ASCII)

```
[ Lawrence ] --(High Complexity Signal)--> [ State Manager ]
                                               |
                                               v
[ UI: Range + Timer ] <---- (SLA Timer API) -- [ "PENDING_VERIFY" State ]
                                               |
                                               v
[ Solicitor Dashboard ] <--- (Priority Sort) -- [ SLA Tracker Service ]
           |                                   |
           v                                   v
[ Final Price Release ] --(Status: ISSUED)--> [ User Notification ]
```

---

## 3. Key Components

### A. State Manager Update
- Introduces `status: PENDING_VERIFICATION` to the `Matter` object.
- Ensures the "Pay Now" button is disabled until the status shifts to `VERIFIED`.

### B. SLA Tracker Service
- **Logic:** `SLA_Deadline = Creation_Timestamp + 4 Hours`.
- Calculates `Time_Remaining` for the UI and Solicitor Dashboard.
- Triggers an "At-Risk" alert (Webhook to Slack) at `Deadline - 1 Hour`.

### C. Range Mapping Logic
- Simple lookup table based on `Practice_Area` and `Complexity_Score`.
- `Min = Median_Historical_Cost * 0.8`.
- `Max = Median_Historical_Cost * 1.2`.

---

## 4. Implementation Speed
- **Effort:** Medium (5-7 engineering days).
- **Risk:** Requires state-machine changes in the core intake flow.
