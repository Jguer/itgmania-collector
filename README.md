# ITG Mania Collector

This collector group was created for [my fork of itgmania](https://github.com/jguer/itgmania) with the purpose of collecting data from the game using [OpenTelemetry](https://opentelemetry.io/) and sending it to a  LGTM (Loki, Grafana, Tempo, Mimir) observability stack.

# Why

As a big fan of rhythm games, I wanted to explore the real-time applications of modern observability tools. What better way to learn the intricacies of OpenTelemetry and the LGTM stack (Loki, Grafana, Tempo, Mimir) than by applying them to the fast-paced data stream of a game like ITGMania? This project serves as both a learning exercise and a practical demonstration of instrumenting a C++ application for detailed telemetry.

# Docker Compose

This directory contains a Docker Compose environment that can be used to test instrumented ITGMania.

## Services
* Grafana: for visualizing telemetry (`localhost:3000`)
* Grafana Mimir: for storing metrics (`localhost:9009`)
* Grafana Loki: for storing logs (`localhost:3100`)
* Grafana Tempo: for storing traces (`localhost:3200`)
* Grafana Pyroscope: for storing profiles (`localhost:4040`)
* Grafana Alloy: Acts as an OpenTelemetry collector and sends self-monitoring data to the stack (`localhost:4317` for grpc, `localhost:4318` for http OTEL collector)

Grafana is automatically provisioned with the appropriate datasources.

OTLP traffic received by Alloy can also be forwarded to Grafana Cloud. Set
`GRAFANA_CLOUD_OTLP_API_TOKEN` in your shell or compose environment before
starting the stack. The compose file already includes your cloud OTLP endpoint
and stack instance ID.

To start the environment, run:

```bash
docker compose up -d
```

To stop the environment, run:

```bash
docker compose down
```

## Visualizing

To visualize ITG Mania data in Grafana, open <http://localhost:3000> in a web
browser and look at the 'MMR' dashboard.

> **NOTE**: It can take up to a minute for ITG Mania metrics and profiles to start
> appearing.
