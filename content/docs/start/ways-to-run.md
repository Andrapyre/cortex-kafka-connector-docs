---
title: "Ways to Run"
description: "Guides lead a user through a specific task they want to accomplish, often with a sequence of steps."
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "ways-to-run-6a1a6be4373e933280d78ea53de6158e"
weight: 810
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Production Usage Types

#### 1. Fully-managed without containerization (not recommended)
1. Download the relevant kafka binary [here](https://kafka.apache.org/downloads)
2. Build the kafka connector plugin jar with the following command (substitute `linuxArm` for `macArm` or `linuxAmd` as per the target machine):
   ```sh 
    sbt "linuxArmBuild/assembly"
   ```
3. The jar should now be built into the `./output` folder.
4. Run kafka and produce messages to a kafka topic as described in the kafka documentation.
5. Go to the kafka binary and run something like the following (adjust the config files as described in the [config](#kafka-connect-config) section - make sure that the jar in the `./output` folder is referenced, as well as the topic that you created in the previous step):
   ```sh
    bin/connect-standalone.sh config/connect-standalone.properties config/connect-file-sink.properties
   ```

#### 2. Managed without docker (ex: AWS MSK Connect)
1. Build the kafka plugin jar as described in the previous section on how to run a fully-managed kafka connector
2. Upload the jar to S3
3. Follow the steps to create a connector, referencing the jar that you uploaded, and using the appropriate [config](#kafka-connect-config)

#### 3. Fully-managed with containerization

Users can fill out the following docker compose file and run it directly or port it into Kubernetes or another container orchestration. See especially the [docker config](#docker-config) section for instructions on which environment variables you can set.
