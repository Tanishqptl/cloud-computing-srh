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
