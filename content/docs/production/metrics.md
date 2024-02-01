---
title: "Metrics"
description: ""
summary: ""
date: 2024-02-01T23:13:40+01:00
lastmod: 2024-02-01T23:13:40+01:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "metrics-aedd0f96a1483d1096274cd2c5f57f69"
weight: 999
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Metrics
All connector metrics are exposed via JMX, so that users will have maximum flexibility in choosing which metrics provider they use. <br/>

**Under _metrics/meters_:** <br/>
`kafka-connect-cortex-sink-error-database-connection`: Total sink connector errors due to the database connection failing <br/>
`kafka-connect-cortex-sink-records`: Total records processed by the sink connector <br/>
`kafka-connect-cortex-sink-records-successful`: Total records successfully processed by the sink connector <br/>
`kafka-connect-cortex-sink-records-failed`: Total records unsuccessfully processed by the sink connector <br/>

`kafka-connect-cortex-source-error-database-connection`: Total source connector errors due to the database connection failing <br/>
`kafka-connect-cortex-source-records`: Total records processed by the source connector <br/>
`kafka-connect-cortex-source-records-successful`: Total records successfully processed by the source connector <br/>
`kafka-connect-cortex-source-records-failed`: Total records unsuccessfully processed by the source connector <br/>

**Under _metrics/timers_:**<br/>
`kafka-connect-cortex-sink-record-processing-time`: Total time that the sink connector took to process a single record <br/>
`kafka-connect-cortex-source-batch-processing-time`: Total time that the source connector took to process a single batch from the database into Kafka
