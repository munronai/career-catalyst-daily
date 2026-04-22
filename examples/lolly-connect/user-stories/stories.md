# User Stories: Lolly Connect

## Feature: Partner Onboarding & Sandbox
**Story:** As a 3rd-party developer, I want to create a sandbox account so that I can test my integration without affecting live production data.

**Scenario: Successful Sandbox Creation**
- **Given** I am on the Lolly Connect Developer Portal
- **When** I register for a "Standard" developer account
- **And** I create a new project named "Fourth ERP Sync"
- **Then** the system should generate a `client_id` and `client_secret`
- **And** I should be able to access the sandbox environment immediately.

---

## Feature: Real-time Order Sync
**Story:** As an ERP Partner (e.g., Fourth), I want to receive a webhook notification when an order is completed so that I can update the operator's financial records in real-time.

**Scenario: Order Completion Notification**
- **Given** I have a valid subscription to the `order.created` webhook
- **When** a transaction is finalized on a Lolly EPoS terminal
- **Then** Lolly Connect should send a POST request to my registered callback URL
- **And** the payload should contain the `order_id`, `total_amount`, and `timestamp`
- **And** the request should be signed with a valid HMAC signature.

---

## Feature: Inventory Adjustment via API
**Story:** As an Inventory Management system, I want to adjust stock levels in Lolly HQ via API so that the EPoS system reflects accurate availability (e.g., "86ing" an item).

**Scenario: Successful Stock Adjustment**
- **Given** I have an active OAuth 2.0 access token with `inventory.write` scope
- **When** I send a PATCH request to `/v1/inventory/{sku_id}` with `adjustment: -10`
- **Then** the API should return a `200 OK` status
- **And** the Lolly HQ dashboard should show the updated stock level for that SKU
- **And** the Lolly EPoS terminals should update their "available quantity" within 5 seconds.

---

## Feature: Token Revocation
**Story:** As a Restaurant Manager, I want to revoke access for a specific integration so that I can maintain security if I stop using a 3rd-party service.

**Scenario: Integration Disconnection**
- **Given** I am logged into Lolly HQ
- **When** I navigate to "Connected Apps" and click "Revoke" for the "Procure Wizard" app
- **Then** the API Gateway should immediately reject any further requests using that app's tokens
- **And** the partner should receive a `401 Unauthorized` response on their next call.
