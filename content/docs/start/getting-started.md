---
title: "Getting Started"
description: "Quick start guide for first-time users"
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "getting-started-6a1a6be4373e933280d78ea53de6158e"
weight: 1
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Sample service configuration

Create a sandbox directory for your project with a `docker-compose.yml` file in the project root. Write the following content to the docker compose file - it contains a sample kafka instance, a cortex database, simple source and sink connectors, and a user interface so that you can visualize what is happening in kafka.

```yaml
version: '3.8'

services:
  zookeeper:
    image: 'bitnami/zookeeper:3.7'
    environment:
      ALLOW_ANONYMOUS_LOGIN: "yes"
  kafka:
    image: 'bitnami/kafka:3.4.0'
    ports:
      - "29092:29092"
      - "9092:9092"
    environment:
      KAFKA_CFG_ZOOKEEPER_CONNECT: "zookeeper:2181"
      ALLOW_PLAINTEXT_LISTENER: "yes"
      KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP: "CLIENT:PLAINTEXT,EXTERNAL:PLAINTEXT"
      KAFKA_CFG_LISTENERS: "CLIENT://:9092,EXTERNAL://:29092"
      KAFKA_CFG_ADVERTISED_LISTENERS: "CLIENT://kafka:9092,EXTERNAL://localhost:29092"
      KAFKA_CFG_INTER_BROKER_LISTENER_NAME: "CLIENT"
    depends_on:
      - zookeeper
  kafka-ui:
    image: provectuslabs/kafka-ui:latest
    ports:
      - "8080:8080"
    depends_on:
      - kafka-connect-sink
      - kafka-connect-source
    environment:
      KAFKA_CLUSTERS_0_NAME: local
      KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS: kafka:9092
      KAFKA_CLUSTERS_0_KAFKACONNECT_0_NAME: sink-connector
      KAFKA_CLUSTERS_0_KAFKACONNECT_0_ADDRESS: http://kafka-connect-sink:8083
      KAFKA_CLUSTERS_0_KAFKACONNECT_1_NAME: source-connector
      KAFKA_CLUSTERS_0_KAFKACONNECT_1_ADDRESS: http://kafka-connect-source:8083
      DYNAMIC_CONFIG_ENABLED: 'true'
  cortex-db:
    image: 'docker.cortex-ag.com/cortex-ip/starter:v6.2.1'
    ports:
      - '29001:29000'
  kafka-connect-sink:
    image: 'docker.cortex-ag.com/cortex/kafka-connector:latest'
    environment:
      KAFKA_CONNECT_MODE: "standalone"
      KAFKA_CONNECTOR_TYPE: "sink"
      KAFKA_CONNECT_BOOTSTRAP_SERVERS: "kafka:9092"
      KAFKA_CONNECT_KEY_CONVERTER: "org.apache.kafka.connect.storage.StringConverter"
      KAFKA_CONNECT_VALUE_CONVERTER: "org.apache.kafka.connect.storage.StringConverter"
      CORTEX_CONNECTION_HOSTNAME: "cortex-db"
      CORTEX_CONNECTION_PORT: "29000"
      CORTEX_CONNECTION_USERNAME: "admin"
      CORTEX_CONNECTION_PASSWORD: "admin"
      CORTEX_CONNECTION_APP_NAME: "TestApp"
      CORTEX_CONNECTION_APP_HASH: "K1cyPPmWtVGVNE8rb4pkcZ3K5OGAqMSwLUBxRDkBQJg="
      CORTEX_FIELD_MAPPINGS: "test-id:testId"
      CORTEX_DATABASE_PRIMARY_KEY: "testId"
      KAFKA_CONNECT_ERROR_TOLERANCE: "all"
      KAFKA_CONNECT_SINK_TOPICS: "cortex-sink"
      KAFKA_CONNECT_SINK_DLQ_TOPIC_NAME: "cortex-sink-dlq"
      KAFKA_CONNECT_SINK_DLQ_TOPIC_REPLICATION_FACTOR: "1"
      KAFKA_CONNECT_SINK_DLQ_ENABLE_HEADER_CONTEXT: "true"
      KAFKA_CONNECT_OFFSET_STORAGE_FILE_FILENAME: "/tmp/connect.offsets"
    depends_on:
      - kafka
  kafka-connect-source:
    image: 'docker.cortex-ag.com/cortex/kafka-connector:latest'
    environment:
      KAFKA_CONNECT_MODE: "standalone"
      KAFKA_CONNECTOR_TYPE: "source"
      KAFKA_CONNECT_BOOTSTRAP_SERVERS: "kafka:9092"
      KAFKA_CONNECT_KEY_CONVERTER: "org.apache.kafka.connect.storage.StringConverter"
      KAFKA_CONNECT_VALUE_CONVERTER: "org.apache.kafka.connect.storage.StringConverter"
      CORTEX_CONNECTION_HOSTNAME: "cortex-db"
      CORTEX_CONNECTION_PORT: "29000"
      CORTEX_CONNECTION_USERNAME: "user"
      CORTEX_CONNECTION_PASSWORD: "user"
      CORTEX_CONNECTION_APP_NAME: "TestApp"
      CORTEX_CONNECTION_APP_HASH: "K1cyPPmWtVGVNE8rb4pkcZ3K5OGAqMSwLUBxRDkBQJg="
      CORTEX_DATABASE_PRIMARY_KEY: "testId"
      KAFKA_CONNECT_ERROR_TOLERANCE: "all"
      KAFKA_CONNECT_SOURCE_OFFSET_PARTITION_NAME: "copy_existing"
      KAFKA_CONNECT_SOURCE_OFFSETS_STORAGE_TOPIC: "offsets"
      KAFKA_CONNECT_OFFSET_STORAGE_FILE_FILENAME: "/tmp/connect.offsets"
      KAFKA_CONNECT_SOURCE_DESTINATION_TOPIC_NAME: "cortex-source"
    depends_on:
      - kafka
```

### Running the service

1. Run the following:
```bash
docker compose up
```

2. Go to [http://localhost:8080](http://localhost:8080). You may need to wait a few moments for the kafka user interface to start.

3. Make sure the `cortex-sink` topic is created. If it is not already created, create it with one partition.

4. Start to create a new message and paste the following values for the key and value respectively

Key: 
```json
359c46bb-317a-48b4-b95c-181e1dc707df
```

Value: 
```json
{
    "key": "value",
    "time": 123481234
}
```




