# Phase 1: Research & Discovery - RWA Documentation for TradFi Developers

## Overview
This report identifies the linguistic and conceptual "friction points" that institutional fund managers and TradFi developers face when interacting with Archax's blockchain-based RWA (Real-World Asset) infrastructure.

## Tabulated Comparison: The TradFi-to-Crypto Rosetta Stone

| TradFi Concept | Blockchain Equivalent | Translation / Bridge Mechanism |
| :--- | :--- | :--- |
| **ISIN / CUSIP** | **Smart Contract Address** | The "Legal Wrapper" maps the token contract to a registered ISIN. |
| **Settlement (T+2)** | **Atomic Settlement (T+0)** | Delivery vs. Payment (DvP) occurs in a single block transaction. |
| **Custody (Qualified)** | **MPC / HSM Custody** | Multi-Party Computation replaces centralized ledger entries with distributed key shards. |
| **Dividend / Coupon** | **Token Yield / Airdrop** | Automated smart contract distribution based on snapshot of token holders. |
| **Beneficial Owner** | **Wallet Address** | KYC/AML "Whitelisting" links a wallet address to a verified identity. |
| **Redemption** | **Token Burning** | Returning the token to the issuer (burning) to reclaim the underlying asset. |
| **Subscription / Issue** | **Token Minting** | Creating new supply of tokens on-chain against a deposited asset. |
| **Order Book** | **Liquidity Pool / DEX** | Automated Market Makers (AMMs) vs. Central Limit Order Books (CLOBs). |

## Analysis of Friction Points

### 1. Conceptual Gap: "Finality" vs. "Reconciliation"
- **TradFi:** Relies on multi-day reconciliation between banks and clearinghouses (CSDs). Errors are corrected via "adjustments" days later.
- **Blockchain:** Transactions are final once confirmed. There is no "undo" button, which terrifies TradFi operations teams who are used to manual oversight.

### 2. Identifier Friction: "Where is the ISIN?"
- Fund managers search for assets by ISIN. Blockchain explorers search by 42-character hex strings (0x...). The documentation must explicitly bridge these two identifiers to provide confidence.

### 3. Gas & Fee Uncertainty
- TradFi developers are used to fixed transaction costs or percentage-based fees. The concept of "Gas" (fluctuating costs based on network congestion) is seen as a barrier to predictable institutional budgeting.

## Areas of Concern (Strategic Focus)

1.  **Legal Enforcement:** How does a "Token Burn" translate to a legal discharge of debt in a traditional court?
2.  **Reporting Compliance:** How to map on-chain events (mints, burns) to existing regulatory reporting standards (MiFID II / CSDR).
3.  **Operational Risk:** Managing private keys vs. managing database credentials.

## Strategic Advantage for Archax
By providing a documentation layer that uses "Institutional-First" language, Archax can lower the barrier to entry for the trillions of dollars in TradFi capital seeking on-chain yields. We are not just selling technology; we are selling a "Language Bridge."
