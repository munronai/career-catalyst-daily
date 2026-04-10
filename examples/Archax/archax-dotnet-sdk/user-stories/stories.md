# User Stories: Archax .NET SDK (ACE API v3.0)

## Feature: Market Data Consumption
As a trading algorithm developer, I want to consume real-time order book updates without manually managing WebSockets or heartbeats.

### Scenario: Subscribing to an L2 Order Book
**Given** I have a valid `ArchaxClient` initialized with my API keys
**When** I call `client.MarketData.WatchOrderBook("BTCUSD")`
**Then** the SDK should automatically establish a WebSocket connection
**And** it should respond to the server's 30-second `Ping` messages with a valid `Pong`
**And** it should stream `OrderBookUpdate` objects where prices and quantities are automatically scaled to `decimal` based on instrument metadata.

### Scenario: Automatic Reconnection
**Given** an active WebSocket connection to "BTCUSD"
**When** the network connection is lost
**Then** the SDK should attempt to reconnect using an exponential backoff strategy
**And** once reconnected, it should automatically re-subscribe to the "BTCUSD" topic
**And** it should emit a `ConnectionRestored` event to my application.

---

## Feature: Order Execution
As an institutional trader, I want to execute orders using C# `decimal` types while ensuring the API receives the correct integer-scaled format.

### Scenario: Creating a Limit Order
**Given** the "BTCUSD" instrument has a `decimalValue` of 8
**When** I call `client.Orders.CreateOrderAsync` with a price of `50000.12345678` and quantity of `0.01`
**Then** the SDK should scale the price to `5000012345678` (long)
**And** it should scale the quantity to `1000000` (long)
**And** it should include the current JWT in the `Authorization` header
**And** it should return a type-safe `OrderResponse` indicating the order is `ACCEPTED`.

### Scenario: Automatic JWT Refresh
**Given** my current JWT will expire in 4 minutes
**When** I attempt to place a new order
**Then** the SDK's internal `AuthManager` should automatically call the `/login` refresh endpoint
**And** it should use the new JWT for the current order request
**And** the order execution should succeed without manual intervention.
