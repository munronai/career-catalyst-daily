# Strategy & Vision: The "Data Connect" Multi-Omics Era

## 1. Vision: From "Data Silos" to "Data Products"
Currently, data at Genomics England is treated as **static assets** (files in buckets). Our strategy is to pivot to **Data Products**—reusable, queryable, and versioned datasets that researchers can "consume" via a standard API without needing to know the underlying storage format.

### The "Patient Data Object" (PDO)
The centerpiece of our vision is the **PDO**. A PDO is a virtualized record that aggregates:
1. **Genotype metadata** (variants, zygosity, depth).
2. **Histopathology features** (AI-derived scores from digital slides).
3. **Primary Care history** (longitudinal EHR data from GPs).

## 2. 2026 Scalability Roadmap
By 2026, Genomics England expects to manage millions of patient records across multiple modalities. Our strategy addresses this growth:
- **Massive Parallel Querying:** Using GA4GH Data Connect enables federated queries that scale horizontally. Instead of one giant database, we have multiple specialized "Data Nodes" that the Hub orchestrates.
- **AI-Ready Infrastructure:** By exposing pathology and genomics through a unified SQL-like API, we lower the barrier for machine learning teams to train multimodal models (e.g., predicting tumor progression from a combination of genetics and tissue scans).

## 3. Assumptions
- **Governance:** Assuming that consent models allow for federated querying across genomics and primary care within the trusted research environment (TRE).
- **Data Availability:** Assuming digital pathology pipelines will produce structured metadata (e.g., cell counts, feature vectors) that can be stored in the Table API.
- **Interoperability:** Assuming the GA4GH Data Connect standard continues to gain adoption among major cloud and storage providers.

## 4. Strategic Alignment
This proposal acts as a **strategic multiplier** for Genomics England's goals:
1. **Accelerated Discovery:** Shifting 80% of researcher time from data wrangling to insight generation.
2. **Institutional Advantage:** Positioning Genomics England as the world leader in queryable, multimodal clinical-genomic data.
3. **Pharma Collaboration:** Providing a "High-Signal" API for Pharma partners to find specific patient cohorts for drug discovery.
