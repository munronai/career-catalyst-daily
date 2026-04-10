# User Stories: Archax "Zero-to-Trade" Sandbox

## Story 1: Instant Onboarding (The Happy Path)
**As a** Developer at a Tier-1 Institutional Firm,
**I want to** log in using my GitHub account and get instant API keys,
**So that** I can start testing the Archax ACE API without waiting for manual approval.

**Scenario: Successful Instant Onboarding**
- **Given** I am on the `sandbox.archax.com` login page
- **When** I click "Login with GitHub" and authorize the application
- **Then** a new Sandbox account should be created for me
- **And** I should be redirected to the "API Credentials" page
- **And** I should see a pre-funded balance of $10,000,000 USD_SIM in my account dashboard.

---

## Story 2: First Trade Execution
**As a** Developer,
**I want to** execute a limit order via the sandbox API,
**So that** I can verify my system's integration with the Archax order lifecycle.

**Scenario: Successful Limit Order Execution**
- **Given** I have a valid Sandbox API Key and Secret
- **When** I send a `POST /v1/orders` request with a `limit` order for `1 BTC_SIM` at `60000 USD_SIM`
- **Then** I should receive a `201 Created` response with an `order_id`
- **And** the order should be matched by the Synthetic Liquidity Engine
- **And** my account balance should update to reflect the trade execution.

---

## Story 3: Schema Validation & Debugging
**As a** Developer,
**I want to** receive detailed error messages when I send an invalid API request,
**So that** I can quickly fix integration bugs during the development phase.

**Scenario: Handling Invalid Order Payload**
- **Given** I am testing the `POST /v1/orders` endpoint
- **When** I send a request with a missing required field (e.g., `side`)
- **Then** I should receive a `400 Bad Request` response
- **And** the response body should contain a `validation_errors` array specifying the missing field
- **And** the "API Logs" section of the dashboard should show the failed request with the full trace.

---

## Story 4: Faucet Refill
**As a** Developer,
**I want to** refill my sandbox account balance if it runs low during testing,
**So that** I can continue testing high-volume trading scenarios.

**Scenario: Successful Balance Refill**
- **Given** my `USD_SIM` balance is less than $1,000,000
- **When** I click the "Refill Faucet" button in the dashboard
- **Then** my `USD_SIM` balance should be increased by $10,000,000
- **And** the "Refill" button should be disabled for the next 24 hours.
