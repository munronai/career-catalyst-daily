# PRD: Lolly Edge-Guard (Payment Resilience)

## 1. Objectives
- **Zero Downtime:** Ensure 100% transaction uptime at the point of sale.
- **Risk Mitigation:** Limit offline fraud/decline exposure to <1% of total transaction volume.
- **Operational Transparency:** Provide real-time reporting on terminal health and "Offline Revenue" status.

## 2. Target Audience
- **Tier 1 Venues:** Stadiums (60k+ capacity) and large-scale festivals.
- **Venue Operators:** CFOs and IT Directors focused on revenue continuity.

## 3. User Flows
### 3.1. The "Clean" Transition (Network Failure)
1. Terminal detects heartbeat failure (>2s latency).
2. UI displays a subtle "Edge-Guard Active" icon (invisible to fan).
3. Transaction is processed locally:
    - Chip/PIN verification (if supported offline).
    - Local Velocity Check (has this card been used 3+ times in the last hour?).
    - BIN Check (is this a high-risk prepaid card?).
4. Transaction "Approved" locally; receipt printed.
5. Transaction stored in encrypted local vault.

### 3.2. The "Sync" (Network Restored)
1. Terminal detects heartbeat restoration.
2. Background process initiates "Drip-Sync" to avoid flooding the backend.
3. Actual authorization requested from processor.
4. Reconciliation report updated for Venue CFO.

## 4. Functional Requirements
| ID | Feature | Description |
| :--- | :--- | :--- |
| FR1 | **Latency Watchdog** | Monitors network health and triggers Edge-Guard mode in <500ms. |
| FR2 | **Local Risk Engine** | Evaluates offline transactions against dynamic risk rules (BIN, Velocity, Amount). |
| FR3 | **Encrypted Local Vault** | Secure, tamper-proof storage for offline transaction payloads. |
| FR4 | **Idempotency Logic** | Ensures zero double-charges during the Sync phase. |
| FR5 | **CFO Dashboard** | Real-time view of "Pending Sync" revenue and risk exposure. |

## 5. Success Metrics
- **Transaction Continuity:** 100% of attempted transactions captured during network outages.
- **Recovery Rate:** >99% of offline transactions successfully authorized upon sync.
- **Transition Latency:** <500ms switch-over time.
