# PRD: Archax .NET SDK (ACE API v3.0)

## 1. Objectives & Key Results (OKRs)

**Objective:** To provide an institutional-grade, open-source .NET SDK for the Archax ACE API v3.0.

-   **KR1:** Launch a public NuGet package supporting .NET 8.0+.
-   **KR2:** Implement 100% coverage of ACE API v3.0 Trading and Market Data endpoints.
-   **KR3:** Support "Resilient WebSockets" (auto-reconnect, heartbeats, and re-subscription).
-   **KR4:** 0% precision loss during integer-to-decimal conversions.

## 2. User Flows

### Flow A: Market Data Consumption
1.  Developer installs `Archax.SDK` NuGet.
2.  Initializes `ArchaxClient` with API Keys.
3.  Subscribes to L2 Order Book updates via an `Observable` or `IAsyncEnumerable` stream.
4.  SDK automatically handles 30s heartbeats and scales integer prices to C# `decimal`.

### Flow B: Order Execution
1.  Developer calls `client.Orders.CreateOrderAsync(...)`.
2.  SDK handles JWT lifecycle, injecting the bearer token.
3.  SDK scales the order quantity and price to the correct integer format for the Archax API.
4.  Developer receives a type-safe `OrderResponse` object.

## 3. Functional Requirements

| ID | Requirement | Description |
| :--- | :--- | :--- |
| **FR1** | **Automated JWT Renewal** | The SDK must monitor JWT expiration and automatically call the `/login` refresh endpoint before the 60-minute cutoff. |
| **FR2** | **Metadata-Driven Scaling** | The SDK must fetch instrument metadata (e.g., `decimalValue`) and use it to scale all integer payloads to/from C# `decimal`. |
| **FR3** | **WebSocket Heartbeat** | The SDK must automatically respond to server "Ping" messages with a "Pong" within 5 seconds. |
| **FR4** | **Exponential Backoff** | On WebSocket disconnection, the SDK must implement an exponential backoff strategy (e.g., 1s, 2s, 4s, 8s...) with max jitter. |
| **FR5** | **Thread-Safe Client** | `ArchaxClient` must be thread-safe and support high-throughput message processing. |

## 4. Non-Functional Requirements

-   **Performance:** SDK overhead must be < 5ms per message processing (excluding network latency).
-   **Logging:** Integration with `Microsoft.Extensions.Logging` for enterprise observability.
-   **Dependency:** Zero dependencies on external non-Microsoft libraries where possible (e.g., use `System.Text.Json` over `Newtonsoft.Json`).

## 5. Success Metrics

-   **Adoption:** Number of institutional partners utilizing the SDK for production trading.
-   **Support:** Significant reduction in "How-to" tickets regarding auth and precision handling.
-   **Stability:** Average WebSocket connection duration (Uptime).
