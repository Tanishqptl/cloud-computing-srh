# ADR 001: Lean Lambda Architecture for Vertex Auto Parts (SHP05)

## Context
Launch customer **SHP05 (Vertex Auto Parts)** requires **2-minute freshness**, **65% ocean / 95% air reliability**, and a **$50/month** budget.
October metrics (`docs/metrics.md`) show 4 of 7 lanes miss targets: SGSIN-BEANR (44.4%), NLRTM-USHOU (50.0%), CNNGB-DEHAM (60.0%), and DXB-FRA (93.3%). Fast ocean delay detection is needed to trigger air expediting, while rate files arrive daily.

## Options
1. **Pure Batch:** Cheap (~$5-10/mo) but fails the 2-minute freshness SLA.
2. **Kappa (Stream-only):** Meets 2-minute freshness with one pipeline, but streaming daily rate files adds unnecessary cost against the $50/mo cap.
3. **Lean Lambda (Chosen):** Serverless speed layer (Pub/Sub + streaming to BigQuery) for live events + batch layer (GCS + BigQuery scheduled SQL, dropping Dataproc and Kafka) for daily files.

## Decision & Consequences
Adopt **Lean Lambda**: meets 2-minute freshness for live delay alerts, keeps cost around $15-30/mo (under the $50 budget), at the trade-off of maintaining two ingestion paths.

## Monthly GCP Cost Estimate (Stretch)
- **Cloud Storage (GCS):** ~$0.05/mo (daily rate/schedule CSVs, < 1 GB in `europe-west3`).
- **BigQuery (Storage + Scheduled SQL + Streaming):** ~$2.00–$5.00/mo (free tier covers first 10 GB storage and 1 TB queries/mo; lightweight streaming inserts).
- **Pub/Sub:** ~$0.00–$1.00/mo (first 10 GB/mo free).
- **Compute (Cloud Run / minimal Dataflow streaming):** ~$10.00–$20.00/mo (serverless scale-to-zero / micro worker).
- **Total Estimated Cost:** **~$12–$26/month**, well within SHP05's **$50/month** budget.
