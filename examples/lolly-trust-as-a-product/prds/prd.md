# PRD: Lolly Trust Center & Governance APIs

## 1. Executive Summary
Lolly’s ISO 42001 accreditation provides a unique opportunity to build a "Trust Center" platform that automates compliance for enterprise clients. This PRD defines the requirements for a customer-facing Trust Portal and the integration of AI Governance metadata into our core API suite.

## 2. Problem Statement
Enterprise clients (Universities/Stadia) view Lolly’s AI (LollySense, tray scanning, facial verification) as a "high risk" component. Current procurement involves manual, repetitive ethics assessments that delay deals.

## 3. Goals & Objectives
- **Objective 1:** Reduce enterprise compliance review time from 6 weeks to <48 hours.
- **Objective 2:** Provide 100% transparency on AI bias and privacy metrics to institutional stakeholders (EDI boards, IT leads).
- **Objective 3:** Enable developers to build "Responsible-AI-aware" integrations using our Trust APIs.

## 4. Target Audience
- **Primary:** Enterprise IT Compliance Officers, University EDI Boards, Legal Counsel.
- **Secondary:** Third-party developers integrating with Lolly EPoS.

## 5. Functional Requirements

### 5.1. The Lolly Trust Portal
- **TP-1: Automated Document Access:** Gated access (SSO/Client ID) to ISO 42001 certificates, AI Impact Assessments (AIIA), and annual bias audit reports.
- **TP-2: Real-time Bias Dashboard:** Visual metrics showing LollySense performance across diverse demographic cohorts (anonymized) to prove non-bias.
- **TP-3: System Inventory:** A directory of every AI model in use at the client’s site, its purpose, and its ISO 42001 risk classification.

### 5.2. Trust-Aware APIs (Governance Metadata)
- **API-1: Governance Headers:** All AI-driven API responses (e.g., age verification, tray scanning) must include an `X-Lolly-Governance` header.
- **API-2: Confidence Scores:** Inclusion of model confidence scores and "Explanability" strings in JSON responses (e.g., `"reason": "Model identified 98% match for Item_X based on edge-detection geometry"`).
- **API-3: Audit Trail:** A specific endpoint `/v1/audit/ai-decisions` that returns a immutable log of AI decisions for legal/compliance review.

## 6. Non-Functional Requirements
- **Security:** Data residency must comply with UK/EU GDPR (ISO 27001 alignment).
- **Performance:** Governance metadata generation must not add >50ms latency to EPoS transactions.
- **Scalability:** Must support 10k+ concurrent requests during peak Stadia events.

## 7. Success Metrics
- **Sales Velocity:** 30% reduction in "Time-to-Sign" for Enterprise contracts.
- **Trust Adoption:** % of clients who enable "Trust Metadata" in their API integrations.
- **Brand Sentiment:** Mention of "Lolly Ethics/Trust" in 50%+ of University tender feedback.
