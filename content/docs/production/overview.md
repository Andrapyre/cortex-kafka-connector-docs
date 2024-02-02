---
title: "Overview"
description: ""
summary: ""
date: 2024-02-02T01:26:02+01:00
lastmod: 2024-02-02T01:26:02+01:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "overview-9c33c4d061d751cdeb403d1c80075921"
weight: 200
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Running in production

There are generally three ways to run kafka connectors:

1. Unmanaged in a VM or bare metal.
2. Managed in a cloud-specific environment, such as AWS MSK or Confluent
3. Containerized

Beginning users will find options 2 and 3 the easiest to get started with. Option 1 should only be undertaken by advanced users in specific scenarios. The cortex kafka connector supports all three equally.
