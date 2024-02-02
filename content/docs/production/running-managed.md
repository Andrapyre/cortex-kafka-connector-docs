---
title: "Running Managed"
description: ""
summary: ""
date: 2024-02-02T01:45:26+01:00
lastmod: 2024-02-02T01:45:26+01:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "running-managed-437a7e05b075b9d6a43521b6de2ab784"
weight: 220
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Running in MSK

1. Download the latest release of the connector plugin [here](/releases/jar-files)
2. Upload the plugin jar to S3
3. Review the documentation for using a custom plugin [here](https://docs.aws.amazon.com/msk/latest/developerguide/msk-connect-plugins.html) and follow the steps to create a connector, referencing the jar that you uploaded and using the appropriate [simple config](/docs/config/simple-kafka-props)

### Running in Confluent

1. Download the latest release of the connector plugin [here](/releases/jar-files)
2. Follow the guide to creating a custom connector [here](https://docs.confluent.io/cloud/current/connectors/bring-your-connector/custom-connector-qs.html), referencing the jar that you downloaded and using the appropriate [simple config](/docs/config/simple-kafka-props)
