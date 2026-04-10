# Phase 1: Research & Discovery - Archax .NET SDK

## Problem Statement
Institutional trading desks operating on Windows/.NET stacks face significant friction when onboarding to Archax due to the lack of a native, "production-ready" SDK. Developers are forced to build custom wrappers for low-level infrastructure (auth, socket management, precision handling) rather than focusing on alpha-generating strategies.

## Discovery Findings: Archax ACE API v3.0

| Feature | Archax Specification (v3.0) | .NET Implementation Pain Point |
| :--- | :--- | :--- |
| **Authentication** | JWT-based with 60min expiry; refresh required via POST `/login`. | Manual lifecycle management in `HttpClient`; risk of session drops. |
| **Data Precision** | Prices/Quantities as **Integers** (e.g., `1000000`). | Requires manual scaling using `decimalValue` metadata; risk of precision loss if using `double`. |
| **Connectivity** | REST for state; WebSocket for real-time market/private data. | `ClientWebSocket` requires manual management of state, reconnects, and heartbeats. |
| **Heartbeats** | Server Pings every 30s; Client must Pong with same timestamp. | Failure to respond results in termination; needs background task management. |
| **Schema** | Evolution of v3.0 REST/WS schemas. | Manual DTO maintenance is error-prone; lack of strong typing leads to runtime errors. |
| **Compliance** | FCA-regulated; requires strict audit trails. | No standard middleware for logging/observability in current manual wrappers. |

## Areas of Concern & Value Multipliers

1.  **Precision Engineering:** The most critical risk is incorrect integer-to-decimal conversion. A native SDK with built-in `ArchaicDecimal` or automated scaling handles this safely.
2.  **Resilience (The "Always-On" Socket):** WebSocket reconnections with exponential backoff and state synchronization (e.g., re-fetching order book snapshots) are non-trivial to implement correctly.
3.  **Onboarding Velocity:** A NuGet package reduces "Time-to-First-Order" from weeks (building custom wrappers) to hours.
4.  **Institutional Trust:** Providing a C#-first, type-safe interface aligns with the expectations of tier-1 institutional trading desks.

## Competitive Landscape
- **CCXT:** Excellent for multi-exchange, but lacks .NET-native deep integration and "idiomatic" C# patterns.
- **FIX (TradingStack):** High performance but complex for many desks; many prefer the flexibility of REST/WS for everything but high-frequency execution.
