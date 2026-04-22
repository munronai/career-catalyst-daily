# PRD: Lolly Connect API Platform (v1.0)

## 1. Objectives & Key Results (OKRs)
*   **Objective:** Establish Lolly as the "API First" leader in UK hospitality.
*   **KR1:** Launch Developer Portal with 100% documentation coverage.
*   **KR2:** Enable 3 core partner categories: ERP (Fourth), Payroll (SAGE), and Inventory (Procure Wizard).
*   **KR3:** Maintain < 200ms latency for 95% of API requests.

## 2. Target Audience
1.  **3rd Party Developers:** Need stable, well-documented endpoints to build integrations.
2.  **Enterprise IT Managers:** Need secure, auditable data flows between Lolly and their back-office.
3.  **Lolly Internal Teams:** Need a standardized way to build new features (Dogfooding).

## 3. User Flows
### A. Partner Onboarding
1.  Developer signs up at `connect.itslolly.com`.
2.  Developer creates a "Project" and receives Sandbox API Keys.
3.  Developer uses interactive Swagger docs to test `/orders` and `/inventory` endpoints.
4.  Developer submits integration for "Certification."

### B. Enterprise Data Sync
1.  Operator enables "Fourth Integration" in Lolly HQ.
2.  Lolly Connect requests OAuth 2.0 authorization from the operator's Fourth account.
3.  Lolly Connect triggers a Webhook on every "End of Day" (EOD) event.
4.  Sales and Labor data are pushed to Fourth automatically.

## 4. Functional Requirements
### R1: Developer Portal
- Self-serve registration and API Key management.
- Sandbox environment with "Mock Data" generator.
- Documentation via OpenAPI 3.0.

### R2: Core API Endpoints
- **Identity API:** OAuth 2.0 (Authorization Code Flow with PKCE).
- **Catalog API:** Read/Write access to Menus, Pricing, and Tax.
- **Transaction API:** Real-time Order data and Historical Reporting.
- **Inventory API:** Real-time stock levels and adjustments.

### R3: Webhook Engine
- Event types: `order.created`, `order.refunded`, `inventory.low_stock`, `eod.finalized`.
- Retry logic (Exponential Backoff).
- Signature validation for security.

## 5. Non-Functional Requirements
- **Security:** AES-256 encryption at rest; TLS 1.3 in transit.
- **Availability:** 99.99% (SLA).
- **Scalability:** Horizontal scaling via Kubernetes to handle peak lunchtime traffic.

## 6. Success Metrics (KPIs)
- **Time to First Hello World (TTFHW):** Goal < 15 mins.
- **Error Rate:** < 0.1% for authenticated requests.
- **Partner NPS:** > 60.
