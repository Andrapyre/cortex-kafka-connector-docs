---
title: "Simple (Docker)"
description: ""
summary: ""
date: 2024-02-01T22:18:05+01:00
lastmod: 2024-02-01T22:18:05+01:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "simple-docker-86779ef54ee397206c5b14b876da1def"
weight: 20
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Worker Config
`KAFKA_CONNECT_PLUGIN_PATH`: `plugin.path` <br/>
`KAFKA_CONNECT_BOOTSTRAP_SERVERS`: `bootstrap.servers` <br/>
`KAFKA_CONNECT_KEY_CONVERTER`: `key.converter` <br/>
`KAFKA_CONNECT_VALUE_CONVERTER`: `value.converter` <br/>
`KAFKA_CONNECT_HEADER_CONVERTER`: `header.converter` <br/>
`KAFKA_CONNECT_TASK_SHUTDOWN_TIMEOUT`: `task.shutdown.graceful.timeout.ms` <br/>
`KAFKA_CONNECT_OFFSET_COMMIT_INTERVAL`: `offset.flush.interval.ms` <br/>
`KAFKA_CONNECT_OFFSET_COMMIT_TIMEOUT`: `offset.flush.timeout.ms` <br/>
`KAFKA_CONNECT_CONFIG_PROVIDERS`: `config.providers` <br/>
`KAFKA_CONNECT_CONFIG_OVERRIDE_POLICY`: `connector.client.config.override.policy` <br/>
`KAFKA_CONNECT_METRICS_SAMPLE_WINDOW_MS`: `metrics.sample.window.ms` <br/>
`KAFKA_CONNECT_METRICS_NUM_SAMPLES`: `metrics.num.samples` <br/>
`KAFKA_CONNECT_METRICS_RECORDING_LEVEL`: `metrics.recording.level` <br/>
`KAFKA_CONNECT_METRICS_REPORTERS`: `metric.reporters` <br/>
`KAFKA_CONNECT_ENABLE_TOPIC_TRACKING`: `topic.tracking.enable` <br/>
`KAFKA_CONNECT_ALLOW_TOPIC_TRACKING_RESET`: `topic.tracking.allow.reset` <br/>
`KAFKA_CONNECT_CLUSTER_ID`: `connect.kafka.cluster.id` <br/>
`KAFKA_CONNECT_GROUP_ID`: `connect.group.id` <br/>
`KAFKA_CONNECT_TOPIC_CREATION_ENABLE`: `topic.creation.enable` <br/>
`KAFKA_CONNECT_OFFSET_STORAGE_FILE_FILENAME`: `offset.storage.file.filename` <br/>

### Cortex Config
`CORTEX_CLIENT_BENCHMARKING_ENABLED`: `cortex.client.benchmarking.enabled` <br/>
`CORTEX_CONNECTION_HOSTNAME`: `cortex.connection.host` <br/>
`CORTEX_CONNECTION_PORT`: `cortex.connection.port` <br/>
`CORTEX_CONNECTION_USERNAME`: `cortex.connection.username` <br/>
`CORTEX_CONNECTION_PASSWORD`: `cortex.connection.password` <br/>
`CORTEX_CONNECTION_APP_NAME`: `cortex.connection.app.name` <br/>
`CORTEX_CONNECTION_APP_HASH`: `cortex.connection.app.hash` <br/>
`CORTEX_DATABASE_PRIMARY_KEY`: `cortex.database.primary.key` <br/>
`CORTEX_FIELD_MAPPINGS`: `cortex.mappings.fields` <br/>
`CORTEX_RECORD_UPDATE_TYPE`: `cortex.record.update.type` <br/>

### General Connector Config
`KAFKA_CONNECT_MAX_TASKS`: `tasks.max` <br/>
`KAFKA_CONNECT_TRANSFORMS`: `transforms` <br/>
`KAFKA_CONNECT_PREDICATES`: `predicates` <br/>
`KAFKA_CONNECT_CONFIG_ACTION_RELOAD`: `config.action.reload` <br/>
`KAFKA_CONNECT_ERRORS_RETRY_TIMEOUT`: `errors.retry.timeout` <br/>
`KAFKA_CONNECT_ERRORS_RETRY_DELAY_MAX_MS`: `errors.retry.delay.max.ms` <br/>
`KAFKA_CONNECT_ERROR_TOLERANCE`: `errors.tolerance` <br/>
`KAFKA_CONNECT_ERRORS_LOG_ENABLE`: `errors.log.enable` <br/>
`KAFKA_CONNECT_ERRORS_LOG_INCLUDE_MESSAGES`: `errors.log.include.messages` <br/>

### Sink Connector Config
`KAFKA_CONNECT_SINK_TOPICS`: `topics` <br/>
`KAFKA_CONNECT_SINK_TOPICS_REGEX`: `topics.regex` <br/>
`KAFKA_CONNECT_SINK_DLQ_TOPIC_NAME`: `errors.deadletterqueue.topic.name` <br/>
`KAFKA_CONNECT_SINK_DLQ_TOPIC_REPLICATION_FACTOR`: `errors.deadletterqueue.topic.replication.factor` <br/>
`KAFKA_CONNECT_SINK_DLQ_ENABLE_HEADER_CONTEXT`: `errors.deadletterqueue.headers.enable` <br/>

### Source Connector Config
`KAFKA_CONNECT_SOURCE_TOPIC_CREATION_GROUPS`: `topic.creation.groups` <br/>
`KAFKA_CONNECT_SOURCE_EXACTLY_ONCE_SUPPORT`: `exactly.once.support` <br/>
`KAFKA_CONNECT_SOURCE_TRANSACTION_BOUNDARY`: `transaction.boundary` <br/>
`KAFKA_CONNECT_SOURCE_TRANSACTION_BOUNDARY_INTERVAL_MS`: `transaction.boundary.interval.ms` <br/>
`KAFKA_CONNECT_SOURCE_OFFSETS_STORAGE_TOPIC`: `offsets.storage.topic` <br/>
`KAFKA_CONNECT_SOURCE_OFFSET_PARTITION_NAME`: `offset.partition.name` <br/>
`KAFKA_CONNECT_SOURCE_DESTINATION_TOPIC_NAME`: `topic.name` <br/>