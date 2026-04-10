# PRD: Archax "TradFi-to-Crypto" Rosetta Stone Documentation

## 1. Product Objective
To create a comprehensive, institutional-grade documentation layer that translates complex blockchain and tokenization concepts into familiar Traditional Finance (TradFi) terminology, accelerating the onboarding and integration of institutional clients onto Archax's RWA infrastructure.

## 2. Target Audience
- **Institutional Developers:** Moving from traditional banking APIs to Web3/Blockchain environments.
- **Compliance & Legal Officers:** Mapping tokenization events to existing financial regulations (MiFID II, CSDR).
- **Fund Operations Managers:** Understanding "Atomic Settlement" and "Digital Custody" in place of T+2 and CSDs.

## 3. User Flows & Functional Requirements

### 3.1 Terminology Translation Layer (Rosetta Stone)
- **Requirement:** A searchable dictionary that provides blockchain equivalents for TradFi terms.
- **Example:** Searching "ISIN" returns information on how Archax maps an ISIN to a Smart Contract Address.
- **Feature:** A "Hover over for TradFi term" feature on technical API documentation to show the equivalent financial concept.

### 3.2 Workflow Blueprints (Bridge Guides)
- **Requirement:** Step-by-step guides for common financial life cycles:
  - **Issuance Lifecycle:** From "Subscription" (TradFi) to "Token Minting" (On-chain).
  - **Secondary Market Trading:** From "Exchange Matching" to "On-chain Settlement (DvP)."
  - **Corporate Actions:** From "Dividend Distribution" to "Smart Contract Airdrop / Yield Payout."
  - **Redemption Lifecycle:** From "Redemption Request" to "Token Burning & Asset Release."

### 3.3 Governance & Compliance Mappings
- **Requirement:** Documentation sections explicitly linking smart contract logic to specific regulatory requirements.
- **Feature:** "Compliance Annotations" for every smart contract function (e.g., `transfer()` function explained as "Settlement of Legal Title").

### 3.4 Operational Best Practices (Institutional Custody)
- **Requirement:** A "Custodian's Guide to Wallets" explaining MPC, HSM, and key management using institutional security terminology.

## 4. Success Metrics
- **Onboarding Velocity:** Reduction in the average time from "API Key Issued" to "First Transaction Logged" by 40%.
- **Documentation NPS:** Direct feedback from institutional clients on the clarity of the documentation.
- **Search Success Rate:** Percentage of searches for TradFi terms (e.g., "ISIN") that lead to a relevant technical documentation page.

## 5. Technical Constraints & Assumptions
- **Constraint:** Documentation must remain up-to-date with evolving regulatory standards in the UK/EU.
- **Assumption:** Archax already has a base level of technical API documentation that this layer will wrap/augment.
- **Assumption:** The target audience has some familiarity with REST/gRPC but may have zero knowledge of Solidity/EVM.
