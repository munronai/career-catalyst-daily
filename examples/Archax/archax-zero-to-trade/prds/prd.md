# PRD: Archax "Zero-to-Trade" Sandbox Experience

## 1. Objectives & Key Results (OKRs)

**Objective:** To create the most frictionless self-serve sandbox environment for institutional developers.

-   **KR1:** Reduce "Time-to-First-Trade" (TTFT) from 72 hours to < 15 minutes.
-   **KR2:** Support 100% of the ACE API v3.0 core trading and data schemas.
-   **KR3:** Automate 100% of the "Testnet" onboarding requests.
-   **KR4:** 90%+ positive "Developer NPS" for the sandbox experience.

## 2. User Flows

### Flow A: Instant Onboarding
1.  Developer visits `sandbox.archax.com`.
2.  Logs in with **GitHub/LinkedIn/Corporate SSO**.
3.  Sandbox automatically generates a "Primary Sandbox Account" with a $10M simulated balance.
4.  User can immediately "Copy API Keys" from the dashboard.

### Flow B: Interactive Testing (Playground)
1.  Developer goes to "API Playground" tab.
2.  Sandbox pre-fills auth headers with the user's sandbox keys.
3.  Developer selects "Create Order" endpoint.
4.  Developer uses a JSON editor with "IntelliSense" (schema-aware) to craft a trade.
5.  Developer hits "Execute" and sees the real-time response + a WebSocket update notification.

## 3. Functional Requirements

| ID | Requirement | Description |
| :--- | :--- | :--- |
| **FR1** | **OAuth-First Onboarding** | Support for GitHub, LinkedIn, and common SAML/SSO providers for instant account creation. |
| **FR2** | **"Faucet-by-Default"** | Auto-funding of new accounts with "Simulated USD", "Simulated BTC", and "Simulated ETH" ($10M USD-equiv). |
| **FR3** | **Synthetic Liquidity Bots** | Background processes to provide continuous L2 order book updates and trade execution for simulated pairs. |
| **FR4** | **API Explorer** | Built-in Swagger/OpenAPI UI for REST and a "Message Inspector" for WebSocket streams. |
| **FR5** | **Webhook Simulator** | Ability to configure endpoints to receive "Trade Settlement" notifications. |

## 4. Non-Functional Requirements

-   **Availability:** 99.9% uptime (independent of Production ACE infrastructure).
-   **Performance:** API latency must mirror Production ACE (low-ms) to ensure realistic testing.
-   **Isolation:** Total data and process isolation from Production; no cross-contamination.
-   **Observability:** Robust logging of API errors to help developers self-diagnose integration bugs.

## 5. Success Metrics

-   **TTFT (Time-to-First-Trade):** The median duration from account creation to the first successful `201 Created` order response.
-   **Completion Rate:** % of users who complete the "Sandbox Quickstart" tutorial.
-   **Support Deflection:** Reduction in "How-to" tickets for the technical onboarding phase.
