# One-Pager: The "Institutional-Ready" .NET SDK for Archax

## The Hook
**Reduce "Time-to-First-Order" for institutional desks from 2 weeks to 2 hours.**

## The Problem
Institutional trading desks—particularly those in the UK/EU market that Archax serves—often operate on Windows-based infrastructure and C#/.NET tech stacks. Currently, these firms must build custom, low-level "plumbing" for the Archax ACE API v3.0 before they can even begin testing their trading algorithms. 

**Key Friction Points:**
1.  **Manual Auth:** Managing JWT lifecycles and MFA integration in custom code is error-prone and leads to session drops.
2.  **Integer Math:** Archax's use of integer-based scaling for prices/quantities requires developers to build custom scaling logic, which is a major source of "rounding-error" bugs.
3.  **WebSocket Fragility:** Implementing the mandatory 30-second ping/pong and exponential backoff for reconnection is a heavy lift for many smaller desks.

## The Solution
An official, open-source Archax .NET SDK (NuGet package) that abstracts the ACE API v3.0 into a type-safe, "idiomatic" C# experience.

**Core Pillars:**
-   **Native Auth Middleware:** Automated JWT renewal and secure secret management.
-   **Automatic Scaling:** Built-in `Decimal` handlers that automatically convert Archax's integer-based payloads into high-precision C# `decimal` types using instrument metadata.
-   **Resilient Connectivity:** A robust `ArchaxClient` with automatic WebSocket heartbeats, reconnection, and state re-synchronization.

## The Value
1.  **Onboarding Velocity:** New institutional partners can go live faster, increasing Archax's market share and volume.
2.  **Reliability & Safety:** By providing a standard implementation of scaling and auth, we reduce the risk of client-side execution errors.
3.  **Market Alignment:** Demonstrates Archax’s commitment to providing institutional-grade tooling that matches the quality of TradFi interfaces (FIX/Bloomberg).
4.  **Community Growth:** Open-sourcing the SDK allows the community to contribute bug fixes and new features, reducing Archax's long-term maintenance burden.

## Success Metric
- **Target:** 50% reduction in integration-related support tickets from new .NET-based institutional partners within 6 months of launch.
