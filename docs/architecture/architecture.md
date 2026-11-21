# SHP05 (Vertex Auto Parts) — Platform Architecture

- **Live (Speed Layer):** Pub/Sub -> Dataflow/Cloud Run -> BigQuery Live -> Ops View & Air-Expedite Alerts (< 2 min freshness).
- **Batch Layer (Daily):** Carrier Rate/Schedule Files -> Cloud Storage -> BigQuery Scheduled SQL -> Curated Tables -> Exec View (replaces Dataproc & Kafka to stay under $50/mo).

```mermaid
flowchart LR
  subgraph live["SPEED LAYER — LIVE (< 2 min)"]
    events["Shipment Events"] --> pubsub["Pub/Sub"] --> stream["Dataflow / Cloud Run"] --> bqlive["BigQuery Live"] --> ops["Ops View & SLA Alerts"]
  end
  subgraph batch["BATCH LAYER — SCHEDULED (Daily)"]
    files["Rate & Schedule Files"] --> gcs["Cloud Storage"] --> bqbatch["BigQuery Scheduled SQL"] --> bqcurated["BigQuery Curated"] --> exec["Exec View"]
  end
```
