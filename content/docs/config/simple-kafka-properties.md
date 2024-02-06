---
title: "Simple (Kafka Props)"
description: "Docs for configuration kafka properties"
summary: ""
date: 2023-09-07T16:06:50+02:00
lastmod: 2023-09-07T16:06:50+02:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "simple-conf-kafka-props-4e0d0e0f89f7decc11eaad4ae9193018"
weight: 110
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### General

`plugin.path`: The full path to the Cortex connector jar <br/>
`connector.class`: Should be `com.cortex.kafka.connector.CortexSinkConnector` for a kafka-to-cortex integration and `com.cortex.kafka.connector.CortexSourceConnector` for a cortex-to-kafka integration. <br/>
`bootstrap.servers`: The kafka (not zookeeper) cluster hostname with port. <br/>
`key.converter`: Key converter class name: Ex: `org.apache.kafka.connect.storage.StringConverter` <br/>
`value.converter`: Value converter class name: Ex: `oorg.apache.kafka.connect.storage.StringConverter` <br/>
`group.id`: The connector group id. Required if running Kafka Connect in distributed mode. Can be any id that does not conflict with a group id that is currently in use. <br/>

### Cortex Specific

`cortex.client.benchmarking.enabled`: Enable in order to see regular logs of the time that Cortex client operations take. Default: false. <br/>
`cortex.connection.host`: The hostname for your Cortex database <br/>
`cortex.connection.port`: Your Cortex database port <br/>
`cortex.connection.app.name`: Set to `TestApp` <br/>
`cortex.connection.app.hash`: Set to the provided hash received from the Cortex team for the kafka_connector app. <br/>
`cortex.connection.username`: The username used to authenticate to the Cortex database. <br/>
`cortex.connection.password`: The password used to authenticate to the Cortex database. <br/>
`cortex.source.primary.key`: The primary key that the source connector will use when pulling data from the cortex database <br/>
`cortex.mappings.fields` _(Optional)_: The field name mappings from the fields in the kafka topic to the fields in the Cortex database. Valid syntax: kafkaFieldName:cortexFieldName,secondKafkaFieldName:secondCortexFieldName <br/>
`cortex.record.update.type`: The strategy used for determining how records are to be updated. Valid values: `create_new` and `overwrite_first` (*default*). <br/>

### Dead Letter Queue (Optional)
`errors.tolerance`: Set to `all` to enable the dead letter queue. <br/>
`errors.deadletterqueue.topic.name`: The name of the topic for the dead letter queue. <br/>
`errors.deadletterqueue.topic.replication.factor`: Set the replication factor for the dead letter queue (default is 3). <br/>
`errors.deadletterqueue.context.headers.enable`: Set this to `true` to enable error context headers. <br/>