# User Stories: Archax "TradFi-to-Crypto" Rosetta Stone

## Story 1: Searching for Asset Identifiers
**As an** Institutional Fund Developer,
**I want to** search for "ISIN" in the Archax developer portal,
**So that I can** find the technical documentation on how to map a token's contract address to its legal ISIN.

**Scenario: Successful ISIN Mapping Search**
- **Given** I am on the Archax Developer Portal home page,
- **When** I enter "ISIN mapping" into the search bar,
- **Then** the search results should prioritize the "Asset Identification & Legal Wrapper" guide,
- **And** it should explain the 1:1 relationship between the token contract and the ISIN.

---

## Story 2: Understanding Token "Burning"
**As a** Compliance Officer,
**I want to** hover over the term "Minting" and "Burning" in the API reference,
**So that I can** see the equivalent institutional terms "Subscription" and "Redemption" and their legal implications.

**Scenario: On-page Term Translation**
- **Given** I am reading the technical API documentation for the `mintAsset()` function,
- **When** I hover over the technical term "minting",
- **Then** a tooltip should appear showing: "TradFi equivalent: Subscription / Issuance",
- **And** it should provide a brief explanation of how this maps to the primary market lifecycle.

---

## Story 3: Transitioning from T+2 to Atomic Settlement
**As an** Operations Manager,
**I want to** read the "Settlement Workflow Blueprint",
**So that I can** visualize how a 2-day manual reconciliation process becomes a single-block atomic transaction.

**Scenario: Visualizing Atomic Settlement**
- **Given** I am reading the "Settlement Workflow Blueprint",
- **When** I view the "DvP (Delivery vs. Payment) Diagram",
- **Then** I should see a side-by-side comparison of the traditional T+2 process vs. the Archax Atomic T+0 process,
- **And** the documentation should explain how "Finality" replaces "Reconciliation."

---

## Story 4: Finding Regulatory Annotations
**As a** Legal Counsel for a Hedge Fund,
**I want to** find the "Regulatory Compliance Mapping" section of a smart contract function,
**So that I can** confirm how Archax's code satisfies MiFID II reporting requirements.

**Scenario: Compliance Mapping Check**
- **Given** I am viewing the "Core Asset Contract" documentation,
- **When** I scroll to the "Compliance Annotations" section of the `transfer()` function,
- **Then** I should see a mapping to the specific article of MiFID II that covers "Post-trade Transparency,"
- **And** it should confirm that the on-chain event satisfies this regulatory requirement.
