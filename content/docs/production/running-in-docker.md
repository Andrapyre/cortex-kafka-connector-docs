---
title: "Running in Docker"
description: ""
summary: ""
date: 2024-02-01T23:11:41+01:00
lastmod: 2024-02-01T23:11:41+01:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "running-in-docker-84e6e76c844e8126222ba57d220c8bc3"
weight: 240
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Usage

Fill in the docker compose file below with the relevant values and then run the command immediately following:

```yaml
version: '3.8'
services:
  kafka-connect-sink:
    image: docker.cortex-ag.com/cortex/kafka-connector:latest
    environment:
      KAFKA_CONNECT_MODE: "standalone"
      KAFKA_CONNECTOR_TYPE: "sink"
      KAFKA_CONNECT_BOOTSTRAP_SERVERS: "<your bootstrap server url>"
      KAFKA_CONNECT_KEY_CONVERTER: "org.apache.kafka.connect.storage.StringConverter"
      KAFKA_CONNECT_VALUE_CONVERTER: "org.apache.kafka.connect.storage.StringConverter"
      CORTEX_CONNECTION_HOSTNAME: "<your cortex db hostname>"
      CORTEX_CONNECTION_PORT: "<your cortex db port>"
      CORTEX_CONNECTION_USERNAME: "<cortex db user>"
      CORTEX_CONNECTION_PASSWORD: "<cortex db pass>"
      CORTEX_CONNECTION_APP_NAME: "<cortex db app name>"
      CORTEX_CONNECTION_APP_HASH: "<cortex db app hash>"
      CORTEX_DATABASE_PRIMARY_KEY: "<db primary key>"
      KAFKA_CONNECT_ERROR_TOLERANCE: "all"
      KAFKA_CONNECT_SINK_TOPICS: "<topics from which to consume data>"
      KAFKA_CONNECT_SINK_DLQ_TOPIC_NAME: "<topic name for dead letter queue>"
      KAFKA_CONNECT_SINK_DLQ_TOPIC_REPLICATION_FACTOR: "1"
      KAFKA_CONNECT_SINK_DLQ_ENABLE_HEADER_CONTEXT: "true"
      KAFKA_CONNECT_OFFSET_STORAGE_FILE_FILENAME: "/tmp/connect.offsets"

  kafka-connect-source:
    image: docker.cortex-ag.com/cortex/kafka-connector:latest
    environment:
      KAFKA_CONNECT_MODE: "standalone"
      KAFKA_CONNECTOR_TYPE: "source"
      KAFKA_CONNECT_BOOTSTRAP_SERVERS: "<your bootstrap server url>"
      KAFKA_CONNECT_KEY_CONVERTER: "org.apache.kafka.connect.storage.StringConverter"
      KAFKA_CONNECT_VALUE_CONVERTER: "org.apache.kafka.connect.storage.StringConverter"
      CORTEX_CONNECTION_HOSTNAME: "<your cortex db hostname>"
      CORTEX_CONNECTION_PORT: "<your cortex db port>"
      CORTEX_CONNECTION_USERNAME: "<cortex db user>"
      CORTEX_CONNECTION_PASSWORD: "<cortex db pass>"
      CORTEX_CONNECTION_APP_NAME: "<cortex db app name>"
      CORTEX_CONNECTION_APP_HASH: "<cortex db app hash>"
      CORTEX_DATABASE_PRIMARY_KEY: "<db primary key>"
      KAFKA_CONNECT_ERROR_TOLERANCE: "all"
      KAFKA_CONNECT_SOURCE_OFFSET_PARTITION_NAME: "copy_existing"
      KAFKA_CONNECT_SOURCE_OFFSETS_STORAGE_TOPIC: "offsets"
      KAFKA_CONNECT_OFFSET_STORAGE_FILE_FILENAME: "/tmp/connect.offsets"
      KAFKA_CONNECT_SOURCE_DESTINATION_TOPIC_NAME: "<target topic to dump data from Cortex db>"
```

```sh
docker compose up
```
