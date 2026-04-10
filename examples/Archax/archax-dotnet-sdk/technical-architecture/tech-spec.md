# Technical Architecture: Archax .NET SDK (ACE API v3.0)

## 1. System Overview
The Archax .NET SDK is a high-performance, type-safe library built on .NET 8.0+. It provides a high-level abstraction over the Archax ACE API v3.0, handling low-level concerns like authentication lifecycle, integer-to-decimal scaling, and WebSocket resilience.

## 2. Component Breakdown

### 2.1. `ArchaxClient` (The Entry Point)
The main facade for interacting with the SDK. It orchestrates the internal services and provides a clean API for developers.
- **Responsibilities:** Initialization, service discovery, and configuration management.
- **Pattern:** Singleton-friendly, thread-safe.

### 2.2. `AuthManager`
Handles the complexity of Archax's JWT-based authentication.
- **Logic:** 
    - Stores the initial JWT and refresh token.
    - Uses a background timer to trigger a refresh via `/login` 5 minutes before the 60-minute expiry.
    - Injects the `Authorization: Bearer <token>` header into all REST requests via a `DelegatingHandler`.

### 2.3. `ScalingManager`
The "Precision Engine" of the SDK.
- **Logic:**
    - Fetches instrument metadata (e.g., `decimalValue = 8`) on startup.
    - Caches metadata in an `ImmutableDictionary<string, InstrumentMetadata>`.
    - Automatically scales outgoing `decimal` values to `long` (e.g., `1.23` -> `123000000`).
    - Automatically scales incoming `long` values to `decimal` (e.g., `123000000` -> `1.23`).

### 2.4. `ResilientWebSocketClient`
A wrapper around `System.Net.WebSockets.ClientWebSocket`.
- **Logic:**
    - **Heartbeats:** Monitors incoming `Ping` messages and automatically responds with a `Pong` containing the same timestamp.
    - **Exponential Backoff:** Implements a jittered backoff strategy for reconnections: `delay = min(max_delay, (2^attempt + random_jitter))`.
    - **State Recovery:** Automatically re-subscribes to previous topics (e.g., order books, trade streams) after a successful reconnection.

## 3. Data Flow Diagram (ASCII)

```text
[ Developer Code ]
       |
       v
[ ArchaxClient ]
       |
-----------------------------------------------------------------
|              |                |                |              |
v              v                v                v              v
[ AuthManager ] [ ScalingManager ] [ REST Client ] [ WS Client ] [ Logger ]
|              |                |                |              |
-----------------------------------------------------------------
       |                        |                |
       v                        v                v
[ JWT Refresh ]          [ Metadata Cache ] [ Heartbeat Loop ]
       |                        |                |
       -------------------------------------------
                         |
                         v
               [ Archax ACE API v3.0 ]
```

## 4. API Design (C# Interface)

```csharp
public interface IArchaxClient : IDisposable
{
    IOrderService Orders { get; }
    IMarketDataService MarketData { get; }
    IInstrumentService Instruments { get; }
}

public interface IOrderService
{
    Task<OrderResponse> CreateOrderAsync(CreateOrderRequest request);
    Task<OrderResponse> CancelOrderAsync(string orderId);
    IAsyncEnumerable<OrderUpdate> StreamOrdersAsync();
}

public interface IMarketDataService
{
    Task<OrderBook> GetOrderBookAsync(string symbol);
    IObservable<OrderBookUpdate> WatchOrderBook(string symbol);
}
```

## 5. Implementation Details
- **JSON Serialization:** Uses `System.Text.Json` with custom `JsonConverter<decimal>` for seamless scaling.
- **Concurrency:** Uses `Channels` (System.Threading.Channels) for high-throughput WebSocket message processing.
- **Observability:** Built-in support for `OpenTelemetry` and `ILogger`.
