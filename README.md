# OpenBI Labs

> **Deep-dive explorations of the tools behind [OpenBI](https://github.com/adnanphp/openbi).**

[![OpenBI Platform](https://img.shields.io/badge/OpenBI-v3.0.0-blue)](https://github.com/adnanphp/openbi/releases/tag/v3.0.0)
[![OpenBI Desktop](https://img.shields.io/badge/OpenBI_Desktop-v0.1.0-blue)](https://github.com/adnanphp/openbi-desktop/releases/tag/desktop-v0.1.0)

OpenBI Labs is a companion collection to the [OpenBI platform](https://github.com/adnanphp/openbi). Where the platform uses each tool as **one layer in a working system**, each lab here goes **deep** on a single tool — internals, edge cases, failure modes, and production patterns that a platform integration cannot cover.

## The three-repo story

| Repo | What it is | Focus |
| --- | --- | --- |
| [openbi](https://github.com/adnanphp/openbi) | The platform (v3.0.0) | End-to-end data engineering + BI + cloud-readiness |
| [openbi-desktop](https://github.com/adnanphp/openbi-desktop) | The client (v0.1.0) | Native Linux desktop app |
| **openbi-labs** *(this repo)* | The deep dives | What each tool does when pushed |

Each lab is:
- **Bounded** — a clear start and end state
- **Independent** — skippable; you can read any single lab on its own
- **Reusable** — plugs into the existing OpenBI platform as a substrate
- **Verifiable** — a runnable reproduction in the lab's own README

## The labs

| Lab | Focus | Status |
| --- | --- | --- |
| [kafka-lab](kafka-lab/) | Kafka internals: partitioning, consumer groups, exactly-once, Connect, Schema Registry | 📋 planned |
| [spark-lab](spark-lab/) | Spark execution model + Delta Lake internals: AQE, skew, Z-order, time travel | 📋 planned |
| [infra-lab](infra-lab/) | Kubernetes + Terraform depth: custom Helm charts, operators, GitOps, state management | 📋 planned |
| [dataquality-lab](dataquality-lab/) | dbt macros, data contracts, OpenLineage, quality gates, SCD Type 2 | 📋 planned |
| [observability-lab](observability-lab/) | Prometheus internals, alerting, OpenTelemetry tracing, SLIs/SLOs | 📋 planned |
| [streaming-lab](streaming-lab/) | Watermarks, windowing, Flink vs. Kafka Streams, event-driven patterns | 📋 planned |
| [analytics-lab](analytics-lab/) | Superset RLS, semantic layers, MLflow, feature stores, LLM-backed BI | 📋 planned |

Full descriptions and sequencing rationale in [ROADMAP.md](ROADMAP.md).

## Why these labs exist

When you use Kafka inside a data platform, you learn "produce a message, consume a message." That's 10% of Kafka.

The other 90% — partitioning strategy under skew, consumer group rebalancing during deploys, exactly-once semantics with transactions, Schema Registry compatibility rules, Connect for CDC — only surfaces when you push the tool. Each lab exists to push one tool.

## Reuse from OpenBI

Every lab connects to the existing OpenBI platform:

- **kafka-lab** uses the OpenBI FastAPI as a producer and Superset as a consumer
- **spark-lab** extends the existing Bronze/Silver/Gold Delta Lake pipeline
- **infra-lab** provisions the same Kind cluster via re-usable Terraform modules
- **dataquality-lab** works with the existing dbt project and Postgres warehouse
- **observability-lab** extends the Prometheus + Grafana + Loki stack
- **streaming-lab** deepens the Kafka + Structured Streaming tier
- **analytics-lab** extends Superset and the RFM/forecasting notebooks

The labs are not standalone tutorials. They are investigations of *the tools the platform already uses*, run against the platform's real data.

## Repository structure
openbi-labs/
├── README.md ← this file
├── ROADMAP.md ← what each lab explores and in what order
├── CONTRIBUTING.md ← conventions for adding a lab
├── LICENSE ← MIT
├── kafka-lab/
│ ├── README.md
│ ├── experiments/
│ ├── notebooks/
│ └── docs/
├── spark-lab/
├── infra-lab/
├── dataquality-lab/
├── observability-lab/
├── streaming-lab/
└── analytics-lab/

text

## Status

**Pre-alpha.** The umbrella is being established. No lab has code yet. See [ROADMAP.md](ROADMAP.md) for the sequencing plan.

## Related

- [OpenBI](https://github.com/adnanphp/openbi) — the platform these labs explore
- [OpenBI Desktop](https://github.com/adnanphp/openbi-desktop) — the native client
- [Dev.to writeup](https://dev.to/adnanphp) — "How I Built a Two-Tier Data Platform in 9 Phases"

## License

MIT
