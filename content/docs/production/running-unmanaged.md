---
title: "Running Unmanaged"
description: ""
summary: ""
date: 2024-02-02T01:38:12+01:00
lastmod: 2024-02-02T01:38:12+01:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "running-unmanaged-8f2657a5c0ff2ddcf7e2117245015356"
weight: 210
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### VM or Bare Metal

1. Make sure that you have an instance of a cortex database and a kafka cluster already running, with a kafka topic created and messages produced to the topic.
2. Download the relevant kafka binary [here](https://kafka.apache.org/downloads)
3. Download the latest release of the connector plugin [here](/releases/jar-files)
4. Go to the kafka binary and run something like the following (adjust the config files as described in the [simple config](/config/simple-kafka-properties) section - make sure that the jar in the `./output` folder is referenced, as well as the topic that you created in the previous step):
   ```sh
    bin/connect-standalone.sh config/connect-standalone.properties config/connect-file-sink.properties
   ```
5. Check your cortex database. You should see that the messages now exist in the database.
