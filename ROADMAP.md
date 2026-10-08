# OpenBI Labs — Roadmap

The labs are ordered so that later ones build on skills from earlier ones. The order is **recommended, not required** — you can read any lab on its own.

## The seven labs

### 1. Kafka Lab — `kafka-lab/`

**Focus:** Kafka as a platform, not a message pipe.

**What goes deep:**
- Partitioning strategies (key-based, round-robin, custom partitioners)
- Consumer groups and rebalancing behavior under load
- Retention policies, log compaction, log segments
- Exactly-once semantics with transactions
- Kafka Connect for CDC from Postgres
- Schema Registry + Avro/Protobuf
- Kafka Streams vs. Spark Structured Streaming
- Dead-letter queues and retry patterns
- Monitoring with Kafka JMX exporter + Prometheus
- KRaft vs. ZooKeeper modes

**Reuses from OpenBI:** FastAPI as a producer, Superset as a real-time consumer.

**New tools:** Kafka Connect, Schema Registry, Kafka Streams

**Time:** 3–4 weekends

**Deliverables:**
- `kafka-lab/README.md` — overview and reproduction steps
- `kafka-lab/docs/partitioning.md` — an experiment comparing partitioning strategies
- `kafka-lab/docs/consumer-groups.md` — rebalancing under load, measured
- `kafka-lab/docs/exactly-once.md` — EOS demo with transactions
- `kafka-lab/docs/connect-cdc.md` — Postgres → Kafka via Debezium
- `kafka-lab/docs/schema-registry.md` — Avro with compatibility modes
- `kafka-lab/notebooks/` — Jupyter notebooks for each experiment

---

### 2. Data Quality Lab — `dataquality-lab/`

**Focus:** The unglamorous work that separates professional pipelines from demos.

**Why second:** Shortest lab (2–3 weekends); builds directly on the existing dbt project.

**What goes deep:**
- dbt macros and Jinja beyond basic templating
- dbt packages ecosystem (dbt-utils, dbt-expectations)
- Custom dbt tests beyond schema.yml
- dbt exposures, metrics, semantic layer
- Data contracts (enforcement at ingestion)
- Soda Core or Great Expectations for quality gates
- Column-level lineage with OpenLineage
- Alerting on data SLAs
- Late-arriving data handling
- Slowly changing dimensions (SCD Type 2)
- Data reconciliation frameworks

**Reuses from OpenBI:** dbt project, Postgres warehouse.

**New tools:** Soda Core / Great Expectations, OpenLineage, Marquez

**Time:** 2–3 weekends

---

### 3. Observability Lab — `observability-lab/`

**Focus:** You can't operate what you can't measure.

**Why third:** Pairs with the Loki work already done in OpenBI v3.0.0; teaches production operations.

**What goes deep:**
- Prometheus internals: TSDB, scrape intervals, retention
- Recording rules, alert rules, Alertmanager routing
- Custom Prometheus exporters (Python)
- Grafana dashboards as code (grafonnet / jsonnet)
- Loki query optimization (avoiding high-cardinality labels)
- Distributed tracing with OpenTelemetry + Tempo/Jaeger
- SLI/SLO definitions with error budgets
- Structured logging patterns for correlation
- Cost-aware observability

**Reuses from OpenBI:** Prometheus, Grafana, Loki stack.

**New tools:** Tempo/Jaeger, OpenTelemetry, grafonnet

**Time:** 3 weekends

---

### 4. Streaming Lab — `streaming-lab/`

**Focus:** Beyond "producer/consumer works" to real event-driven architecture.

**Why fourth:** Builds on the Kafka lab; adds Flink and richer semantics.

**What goes deep:**
- Watermarks and event-time vs. processing-time
- Late event handling
- Windowing strategies (tumbling, sliding, session)
- Exactly-once with checkpointing internals
- Backpressure and rate limiting
- Dead-letter topics
- Schema evolution in streams
- Kafka Streams vs. Flink vs. Spark Structured Streaming
- Async event-driven patterns (saga, outbox)

**Reuses from OpenBI:** Kafka + Spark Structured Streaming tier.

**New tools:** Apache Flink, Kafka Streams

**Time:** 3–4 weekends

---

### 5. Spark + Delta Lab — `spark-lab/`

**Focus:** The Spark execution model and Delta Lake internals.

**Why fifth:** Uses the existing 1M-row pipeline; heavy on internals.

**What goes deep:**
- Physical execution plans (`explain()`, DAG visualization)
- Partitioning, bucketing, and file layout tuning
- Broadcast joins vs. sort-merge joins
- Skew handling strategies
- Adaptive Query Execution (AQE)
- Delta Lake time travel, MERGE, OPTIMIZE, Z-order
- Change Data Feed and streaming reads from Delta
- Schema evolution and enforcement
- Small file problem and compaction
- Benchmarking 10M–100M rows at varying cluster sizes
- MLflow integration for Spark ML experiments

**Reuses from OpenBI:** existing Silver/Gold pipeline.

**New tools:** MLflow, Spark UI, Delta CDF

**Time:** 3–4 weekends

---

### 6. Infra Lab — `infra-lab/`

**Focus:** Infrastructure as a first-class engineering discipline.

**Why sixth:** Most complex; benefits from prior labs being done.

**What goes deep:**
- Custom Helm charts for OpenBI services
- Kustomize overlays for dev/staging/prod
- Kubernetes operators (build a small one with kubebuilder)
- Network policies, pod security standards, RBAC
- HPA and VPA autoscaling under load
- Service mesh comparison (Linkerd vs. Istio)
- Terraform modules (extract OpenBI's config into reusable modules)
- Terraform state management: S3 backend + DynamoDB locking
- Terraform workspaces vs. separate states
- Cross-provider: provision Kind + AWS + GCP from one module
- GitOps with ArgoCD or Flux

**Reuses from OpenBI:** every K8s manifest and Terraform file.

**New tools:** ArgoCD/Flux, Linkerd/Istio, kubebuilder, external-secrets

**Time:** 4–5 weekends

---

### 7. BI + ML Lab — `analytics-lab/`

**Focus:** The user-facing side — dashboards and models.

**Why last:** Ties everything together with polish.

**What goes deep:**
- Superset custom charts and plugins
- Superset row-level security (RLS)
- Data modeling for BI (star vs. snowflake vs. one-big-table)
- Semantic layers (Cube, MetricFlow)
- Experiment tracking with MLflow
- Model registry and deployment
- Feature stores (Feast)
- A/B testing frameworks
- LLM-backed BI (SQL generation from natural language)

**Reuses from OpenBI:** Superset, RFM, forecasting.

**New tools:** MLflow, Feast, Cube

**Time:** 4 weekends

---

## Progress tracking

Update this table as labs complete:

| # | Lab | Status | Started | Completed |
| --- | --- | --- | --- | --- |
| 1 | kafka-lab | 📋 planned | — | — |
| 2 | dataquality-lab | 📋 planned | — | — |
| 3 | observability-lab | 📋 planned | — | — |
| 4 | streaming-lab | 📋 planned | — | — |
| 5 | spark-lab | 📋 planned | — | — |
| 6 | infra-lab | 📋 planned | — | — |
| 7 | analytics-lab | 📋 planned | — | — |

## Status legend

- 📋 **planned** — README exists, no code
- 🚧 **in progress** — experiments running, docs being written
- ✅ **complete** — README, docs, and reproducible experiments all in place

## Non-goals

- This is not a tutorial series. Labs assume the reader knows the tool.
- This is not a "build your own X" project. Labs use the tools as they are.
- Labs do not replace the [OpenBI platform](https://github.com/adnanphp/openbi). They extend it.
