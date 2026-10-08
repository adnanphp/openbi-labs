# Kafka Lab

**Status:** 🚧 in progress

Deep-dive explorations of Kafka internals and production patterns —
partitioning, consumer groups, exactly-once semantics, Connect, and
Schema Registry.

Part of [OpenBI Labs](../README.md).

## What this lab explores

Kafka is a distributed log with an elegant surface and a deep
implementation. This lab pushes past "produce a message, consume a
message" to the parts that matter in production:

- **K1** — 3-broker KRaft cluster (this phase)
- **K2** — Partitioning strategies: how keys affect throughput and skew
- **K3** — Consumer groups: rebalancing behavior under load
- **K4** — Exactly-once semantics: the transactions API
- **K5** — Kafka Connect: Postgres → Kafka CDC with Debezium
- **K6** — Schema Registry: Avro and compatibility modes
- **K7** — Wrap-up and reproduction

## The cluster (K1)

Three brokers in **KRaft mode** (no ZooKeeper — Kafka 4.0 removed it
entirely). Combined broker + controller roles. Each broker holds
replicas of every partition in the lab's topics.
Client (localhost:19092, 19093, 19094)
│
┌────────┼────────┐
▼ ▼ ▼
kafka-1 kafka-2 kafka-3 ← brokers + controllers
│ │ │
└────────┼────────┘
│
KRaft quorum (metadata)

text

## Running it

```bash
# Start
docker compose up -d

# Wait for the cluster to form (~30-45 seconds)
docker compose ps

# Open the UI
open http://localhost:18080

# Stop (keeps data)
docker compose down

# Stop and wipe (removes data)
docker compose down -v
Verifying the cluster
bash
# Cluster metadata quorum status
docker exec -it kafka-lab-1 /opt/kafka/bin/kafka-metadata-quorum.sh \
  --bootstrap-server kafka-1:9092 describe --status

# Create a test topic
docker exec -it kafka-lab-1 /opt/kafka/bin/kafka-topics.sh \
  --bootstrap-server kafka-1:9092 \
  --create --topic test-topic --partitions 3 --replication-factor 3

# Inspect partition assignment
docker exec -it kafka-lab-1 /opt/kafka/bin/kafka-topics.sh \
  --bootstrap-server kafka-1:9092 --describe --topic test-topic
Ports
Service	Host port	Container port
Broker 1	19092	9092
Broker 2	19093	9092
Broker 3	19094	9092
Kafka UI	18080	8080
Ports chosen to avoid conflict with the OpenBI platform's own
single-broker Kafka on 9092–9093.

License
MIT
