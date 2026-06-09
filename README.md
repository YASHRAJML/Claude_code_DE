# IoT Sensor Telemetry Data Platform

An end-to-end, open-source data engineering platform that ingests high-volume IoT
sensor telemetry via **Kafka**, captures device-registry changes via **Debezium CDC**,
lands raw data in **object storage (MinIO)**, and transforms it with **dbt** into an
incrementally-loaded dimensional model (with **SCD Type 2**), orchestrated by
**Airflow** and surfaced in a **BI dashboard** — fully containerized with **Docker**.

> Built to demonstrate production-style data engineering: streaming + batch ingestion,
> change data capture, schema mapping, dimensional modeling, incremental loading,
> data quality, and orchestration.

---

## Architecture

```
  Python generator ──▶  Kafka  ──▶  Consumer ──▶  MinIO (raw)
  (telemetry +              ▲                          │
   registry changes)        │ Debezium (CDC)           ▼
                            │                  Warehouse (Postgres)
  Source Postgres ──────────┘                          │
  (device registry)                                    ▼
                                          dbt: staging → dims + facts
                                          (SCD2, incremental, late-data)
                                                       │
                                                       ▼
                                          Data quality (dbt tests + GE)
                                                       │
                                                       ▼
                                          BI dashboard (Metabase/Superset)

                       Airflow orchestrates the batch + quality layers
```

## Tech Stack
| Layer | Tool |
|---|---|
| Streaming | Apache Kafka |
| Change Data Capture | Debezium |
| Object storage | MinIO (S3-compatible) |
| Warehouse | PostgreSQL |
| Transformation | dbt |
| Orchestration | Apache Airflow |
| Data quality | dbt tests, Great Expectations |
| BI | Metabase / Superset |
| Runtime | Docker + Docker Compose |
| Language | Python 3.10+, SQL |

## Concepts demonstrated
- Streaming ingestion & schema mapping (heterogeneous device payloads → canonical schema)
- Change Data Capture (CDC)
- Slowly Changing Dimensions (Type 2)
- Incremental loading with watermarks
- Late / out-of-order data handling
- ELT (land raw, transform in-warehouse with dbt)
- Dimensional modeling (facts + dimensions)
- Data quality testing
- Workflow orchestration

---

## Repository layout
| Folder | Purpose |
|---|---|
| `generator/` | Python: device-registry seeder + telemetry generator |
| `ingestion/` | Kafka producers + consumers, schema-mapping logic |
| `debezium/` | CDC connector configs |
| `warehouse/` | Postgres init scripts |
| `dbt/` | dbt project: staging → marts (SCD2, incremental) |
| `quality/` | Great Expectations suites |
| `airflow/` | DAGs + Airflow config |
| `dashboards/` | BI configs / exports |
| `docs/` | Architecture diagrams, design notes, interview talking points |

## How to run
> The platform runs via Docker Compose. (Run instructions are added as each phase lands.)

```bash
cp .env.example .env   # then edit values
docker compose up -d
```

## Build progress
- [x] Phase 0 — Foundations & repo setup
- [ ] Phase 1 — Source system + data generation
- [ ] Phase 2 — Streaming ingestion (Kafka) + schema mapping
- [ ] Phase 3 — CDC on device registry (Debezium)
- [ ] Phase 4 — Raw landing + warehouse
- [ ] Phase 5 — Transformation with dbt (SCD2 + incremental + late data)
- [ ] Phase 6 — Data quality
- [ ] Phase 7 — Orchestration (Airflow)
- [ ] Phase 8 — Serving / BI dashboard
- [ ] Phase 9 — Polish & portfolio

See [`docs/PROJECT_PLAN.md`](docs/PROJECT_PLAN.md) for the full task-by-task roadmap.
