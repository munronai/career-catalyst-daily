# Presentation: Multi-Omics "Data Connect" Hub
**Scaling Multimodal Discovery at Genomics England**

---

## Slide 1: The Vision
**Unlocking the "Patient Data Object"**
- **The Problem:** Genomics, Pathology, and EHR data live in separate, disconnected silos.
- **The Opportunity:** A single API to query the full breadth of a patient's biological and clinical history.
- **The Goal:** Reduce researcher friction and accelerate the delivery of precision medicine.

---

## Slide 2: The "Join" Friction (Data-Backed)
**Why Researchers are Stuck in ETL**
- **80%:** Time spent by researchers on data cleaning and manual joins.
- **3 Modalities:** Genomics (VCF), Digital Pathology (WSI), and Primary Care (EHR) currently lack a common query interface.
- **The Bottleneck:** Massive file sizes (1GB+ for WSI, 100GB+ for WGS) make traditional "download and join" workflows obsolete.

---

## Slide 3: The Solution - GA4GH Hub
**Standardized, Federated, and Queryable**
- **GA4GH Data Connect:** A schema-agnostic middleware that abstracts storage disparities.
- **SQL-First:** Researchers use familiar SQL to perform complex, multimodal joins.
- **Virtualization:** Query data where it lives; no need for massive data migrations or duplication.

---

## Slide 4: Technical Implementation
**Built for the 2026 Scale**
- **Orchestrated Federation:** Seamlessly joins data across AWS, Google Cloud, and On-Prem.
- **Automated Metadata Extraction:** Transforms "dark data" (massive files) into searchable metadata tables.
- **Interoperable by Design:** Plugs into the global GA4GH ecosystem, enabling international research collaboration.

---

## Slide 5: Impact & Success
**Results that Matter**
- **Speed:** Reduce cohort discovery time from weeks to seconds.
- **Scalability:** Built to handle the growth to millions of multimodal records by 2026.
- **Value:** High-signal "Data Products" that drive value for Pharma partners and Academic researchers alike.
