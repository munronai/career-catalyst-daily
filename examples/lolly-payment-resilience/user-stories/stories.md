# User Stories: Lolly Edge-Guard

## 1. Automated Outage Detection (The "Watchdog")
**Story:** As a POS Terminal, I want to automatically detect network degradation so that I can switch to Edge-Guard mode without manual intervention.

**Scenario: Latency Threshold Exceeded**
- **Given** the terminal is in `ONLINE` mode
- **And** the network heartbeat latency exceeds 2000ms for 3 consecutive pulses
- **When** the next transaction is initiated
- **Then** the terminal should switch to `OFFLINE_RESILIENT` mode in <500ms
- **And** the UI should display the Edge-Guard status icon.

## 2. Intelligent Offline Approval (The "Happy Path")
**Story:** As a Venue Operator, I want the POS to approve low-risk transactions while offline so that I don't lose revenue during a network outage.

**Scenario: Low-Risk Transaction Approval**
- **Given** the terminal is in `OFFLINE_RESILIENT` mode
- **And** a fan taps a standard Visa Debit card for $12.00
- **And** this card has not been used at this terminal in the last hour
- **When** the Edge-Guard risk engine processes the request
- **Then** it should return a `LOCAL_APPROVE` status
- **And** the transaction should be saved to the Encrypted Local Vault.

## 3. High-Risk Mitigation (The "Safety Valve")
**Story:** As a Venue CFO, I want the system to decline high-risk transactions while offline to prevent fraud.

**Scenario: Prepaid Card Over Floor Limit**
- **Given** the terminal is in `OFFLINE_RESILIENT` mode
- **And** a fan taps a high-risk Prepaid Card (identified by BIN)
- **And** the transaction amount is $45.00 (above the $20.00 prepaid floor limit)
- **When** the Edge-Guard risk engine processes the request
- **Then** it should return a `LOCAL_DECLINE` status
- **And** the fan should be prompted to use a different card or wait for network restoration.

## 4. Idempotent Background Sync (The "Recovery")
**Story:** As a System Administrator, I want offline transactions to sync automatically when the network returns without creating duplicate charges.

**Scenario: Drip-Sync After Restoration**
- **Given** 50 transactions are stored in the Encrypted Local Vault
- **And** the Latency Watchdog detects 5 consecutive heartbeats <500ms
- **When** the terminal returns to `ONLINE` mode
- **Then** the Sync Manager should upload transactions in batches of 5
- **And** the Cloud Gateway should verify the `trace_id` for each transaction to ensure no double-charges
- **And** the Local Vault should mark transactions as `SYNCED` upon confirmation.

## 5. Velocity Check Enforcement (The "Limit")
**Story:** As a Risk Manager, I want to limit the number of times a card can be used offline to prevent "Card Trawling" attacks.

**Scenario: Card Velocity Limit Reached**
- **Given** the terminal is in `OFFLINE_RESILIENT` mode
- **And** the card `XXXX-XXXX-XXXX-1234` has already been used 3 times in the last 60 minutes
- **When** the fan attempts a 4th transaction
- **Then** the Edge-Guard risk engine should return a `LOCAL_DECLINE`
- **And** the reason "Velocity Limit Reached" should be logged for the terminal operator.
