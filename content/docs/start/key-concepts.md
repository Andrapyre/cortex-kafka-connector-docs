---
title: "Key Concepts"
description: "Explanation of the cortex kafka connector's core features"
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "key-concepts-6a1a6be4373e933280d78ea53de6158e"
weight: 10
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

See the Kafka Connect documentation [here](https://kafka.apache.org/documentation/#connect_overview) to begin.

### Creating/Updating Records (Sink)

Users can determine whether they would like the kafka sink connector to update records based on a primary key via the `cortex.record.update.type` property. `overwrite_first` is the default strategy. If it is set, an error will be thrown if no primary key is specified. If a primary key is specified, the sink connector will search for the first record with a corresponding primary key value found in the incoming record. If such a record is found, it will update it. Otherwise, it will create a new one. The `create_new` strategy bypasses any search for a pre-existing record and simply creates a new record in the Cortex database every time it processes one. If `create_new` is specified, no primary key is required.

### Primary Key
Both the Cortex sink and source connectors require (assuming the `cortex.record.update.type property` is set to `overwrite_first` in the sink connector) that the user specify a database primary key via the `cortex.database.primary.key` property. The sink connector reads a message from Kafka and determines if the key is a simple string or a json string/map (a composite key). If the former, it will create an entry in the value of primaryKey:kafkaKeyValue. If the latter, it will look for the primary key value in the map structure and add that to the value body to be written into the Cortex database. If no key is specified, it will look for the primary key in the value body and throw an error if none is found.

### Field Handling
Users can take advantage of the `cortex.mappings.fields` property to map kafka fields to database fields, or vice-versa. If the sink connector encounters a field in the data from Kafka which is not represented in the database, it will create the field automatically with a type that best fits the data which it has received. For best results, users should create all relevant fields in the database before the sink connector encounters them, otherwise the data type may not be accurate (for instance, the sink connector does not support automatically generating date or timestamp fields). Additionally, if automatically generated, the field may be automatically renamed to fit the Cortex requirements for a field synonym (i.e. no more than six characters).

### Message Transformation

Kafka natively supports writing custom transformers which take the message output from one topic, change the data structure/content of the messages with optional filtering, and dump the result in another topic. For simple transformation use cases, this puts a clear burden on the user. For this reason, the cortex kafka connector supports transformation *via configuration* for simple use cases. Currently, the connector only supports adding new fields. In order to configure message transformation, users must set up an advanced config file, documented [here](/docs/config/advanced)