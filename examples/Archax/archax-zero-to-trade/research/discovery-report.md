# Phase 1: Research & Discovery - The "Zero-to-Trade" Sandbox

## Problem Statement
The current onboarding process for institutional partners to Archax's "Testnet" environment is a high-touch, manual process that can take days. This friction delays the initial "proof of value" and can lead to lead drop-off during the technical evaluation phase. Institutional developers need a self-serve, "sandbox-first" experience that mirrors the production lifecycle without the legal or capital overhead.

## Discovery Findings: Institutional Onboarding Friction

| Friction Point | Current Experience (Estimated) | "Zero-to-Trade" Goal |
| :--- | :--- | :--- |
| **Account Creation** | Manual request -> Email -> Wait 24h. | Self-serve GitHub/SSO login -> Instant. |
| **API Keys** | Provided via manual secure-share. | Generated in Dashboard with custom scopes. |
| **Test Funds** | Request from "support" or "faucet". | Auto-funded with simulated assets on startup. |
| **Market State** | Static or stale order books. | Synthetic liquidity providers (bots) for realistic testing. |
| **Monitoring** | No visibility into why an order failed. | Integrated "Live API Console" with debug traces. |
| **Post-Trade** | Manual check of account balances. | Real-time Webhooks for settlement simulations. |

## Areas of Concern & Value Multipliers

1.  **Synthetic Liquidity (Realistic Testing):** A sandbox is only as good as its data. Static order books don't test execution logic. We need "Market-Making-as-a-Service" bots to provide realistic, dynamic L2 books.
2.  **The "Success Loop" (First Trade):** The most critical metric is "Time-to-First-Trade." A "Zero-to-Trade" experience reduces this from 3 days to < 15 minutes.
3.  **Self-Serve Autonomy:** Reducing the burden on the Archax Technical Account Management (TAM) team. Let the TAMs focus on production go-lives while the sandbox handles the "discovery" phase.

## Competitive Landscape
- **Kraken/Binance Sandbox:** Highly automated, "API-first" approach.
- **TradFi (LSEG/CME):** Often heavy-touch, requiring dedicated VPNs or FIX connectivity setups. Archax can win by providing a "SaaS-like" sandbox experience for institutional assets.
