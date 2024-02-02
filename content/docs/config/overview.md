---
title: "Overview"
description: "Overview of different configuration possibilities"
summary: ""
date: 2023-09-07T16:06:50+02:00
lastmod: 2023-09-07T16:06:50+02:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "overview-conf-4e0d0e0f89f7decc11eaad4ae9193018"
weight: 100
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Configuration Types

There are two ways to configure the cortex kafka connector. One way is through kafka properties files and the other is through environment variables (only supported in docker). The docker image has built-in support for environment variable configuration. Before the connector runs, these environment variables are converted to two properties files which are then loaded into the connector. Environment variables are supported to enable ease of use.

### Advanced

Advanced configuration is currently only supported for docker instances.