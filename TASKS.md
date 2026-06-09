# Task List — IoT Sensor Telemetry Data Platform

> Living checklist. Tick a box when a task is done and pushed.
> Full context for each phase: see [docs/PROJECT_PLAN.md](docs/PROJECT_PLAN.md).

Last updated: 2026-06-09

---

## ✅ DONE

### Phase 0 — Foundations & Repo Setup
- [x] 0.1 Verify tooling (Docker, Python, git)
- [x] 0.2 Create project folder + git init
- [x] 0.3 Add `.gitignore` + `README.md`
- [x] 0.4 First commit + push to GitHub  *(commit edacf94)*
- [x] 0.5 `docker-compose.yml` skeleton

---

## 🔲 TO DO

### Phase 1 — Source System + Data Generation  ← **YOU ARE HERE**
- [ ] 1.1 Design the device registry data model (decide which columns change → SCD2)  ← **NEXT**
- [ ] 1.2 Source Postgres in Docker + init SQL
- [ ] 1.3 Device registry seeder (Python) — multiple device types
- [ ] 1.4 Telemetry generator (Python) — varied payloads, late/out-of-order data
- [ ] 1.5 Registry-change simulator (firmware/location updates → feeds CDC)

### Phase 2 — Streaming Ingestion (Kafka) + Schema Mapping
- [ ] 2.1 Add Kafka (+ KRaft) + Kafka UI to compose
- [ ] 2.2 Producer: publish telemetry to topics
- [ ] 2.3 Consumer: write raw events to storage
- [ ] 2.4 Schema mapping: heterogeneous payloads → canonical schema

### Phase 3 — CDC on Device Registry (Debezium)
- [ ] 3.1 Add Debezium Connect to compose
- [ ] 3.2 Configure Postgres → Kafka connector
- [ ] 3.3 Verify insert/update/delete change events captured

### Phase 4 — Raw Landing + Warehouse
- [ ] 4.1 Add MinIO + warehouse Postgres to compose
- [ ] 4.2 Land raw telemetry to MinIO
- [ ] 4.3 Land CDC change events to warehouse

### Phase 5 — Transformation with dbt
- [ ] 5.1 Init dbt project + warehouse connection
- [ ] 5.2 Staging models (clean + cast)
- [ ] 5.3 `dim_device` as SCD Type 2
- [ ] 5.4 `fact_readings` incremental model (watermark)
- [ ] 5.5 Hourly/daily rollups
- [ ] 5.6 Handle late / out-of-order data

### Phase 6 — Data Quality
- [ ] 6.1 dbt tests (not_null, unique, relationships, accepted_values)
- [ ] 6.2 Great Expectations suite on key tables

### Phase 7 — Orchestration (Airflow)
- [ ] 7.1 Add Airflow to compose
- [ ] 7.2 DAG: batch load → dbt run → tests
- [ ] 7.3 Freshness / failure alerting

### Phase 8 — Serving / BI Dashboard
- [ ] 8.1 Add Metabase to compose
- [ ] 8.2 Build dashboards on the marts

### Phase 9 — Polish & Portfolio
- [ ] 9.1 Architecture diagram + design notes
- [ ] 9.2 CI (lint + dbt build on PR)
- [ ] 9.3 Interview talking points doc
- [ ] 9.4 Final README polish
