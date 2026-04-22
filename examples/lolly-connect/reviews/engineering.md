# Engineering Review: Lolly Connect
**Reviewer:** CTO/Lead Architect Persona
**Date:** 2024-05-23

## Verdict: APPROVE (with conditions)
The technical foundation is solid and modernized, but implementation effort for the legacy "bridge" should not be underestimated.

### Strengths
- **Modern Stack:** The choice of OAuth 2.0 + PKCE and an event-driven model is exactly what we need to scale. 
- **Decoupling:** Using an API Gateway to abstract the legacy EPoS backend allows us to modernize the core at our own pace without breaking partner integrations.
- **Observability:** The inclusion of `correlation_id` and signed webhooks shows a deep understanding of production support for distributed systems.

### Technical Concerns
- **Legacy XML/JSON Bridge:** Mapping our internal legacy schemas to the "Unified Hospitality API" will be the hardest part of Phase 1. We need to allocate senior backend resources here.
- **Latency at Peak:** Hospitality has extreme "lunch rush" peaks. We must ensure the Gateway and Redis cache can handle 10x normal load with < 200ms p95 latency.
- **Sandbox Parity:** Maintaining a sandbox that actually reflects production behavior (without using production data) is a non-trivial CI/CD challenge.

### Recommendation
Start with a "Read-Only" version of the Catalog and Order APIs to prove the Gateway architecture before moving to high-risk "Write" operations like Inventory adjustments.
