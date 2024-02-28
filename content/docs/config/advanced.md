---
title: "Advanced"
description: ""
summary: ""
date: 2023-09-07T16:06:50+02:00
lastmod: 2023-09-07T16:06:50+02:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "advanced-4e0d0e0f89f7decc11eaad4ae9193018"
weight: 130
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Variables

The advanced config supports two variables, each of which can only be used if they are alone. For example, trying to construct a string literal with `$topicName` (e.g. `cortex-$topicName`) will result in a literal value of "cortex-$topicName" - the actual topic name cannot be read. For performance reasons, fields may only be specified once per message. Thus the following will produce a config error:

```yaml
additionalData:
  origin: $topicName
  source: $topicName
```

*$topicName*: Taken from the sink record topic name. 

*$timestamp*: Taken from the sink record timestamp. If set and the timestamp is `null` or not convertable to an `Integer`, message processing will fail and the message will be shunted to a dead letter queue.

### Sample Config File

See the following advanced config file with notes about which keys are required or not. Topic level configurations override the default configuration. Setting `ignoreDefault` on the topic level to `true` ignores all default settings.

```yaml
sink: # Required
   default: # Optional. Default - None
      messageTransform: # Required
         additionalData: # Required.
          # The following is sample data. 
          # It must be structured as an object. Anything else, an array, a string, etc. will throw an error. 
          # Keys and values must be strings
            orgName: cortex
            source: $topicName
   topics: # Optional. Default - None
      - name: cortex-sink-1 # Required
        messageTransform: # Required
           additionalData: # Required
              dept: engineering
              time: $timestamp
        ignoreDefault: true # Optional. Default - false
      - name: cortex-sink-2
        messageTransform:
           additionalData:
              dept: marketing
              stamp: $timestamp
```

### Running in Production

The Cortex kafka connector currently supports retrieving advanced config files from local storage or from AWS S3. See below to configure each option:

#### Local Storage

In order for the connector to load an advanced config file from local storage, the file needs to be present at the path: `/cortex/config.yml`.

#### AWS S3

To load an advanced config file from AWS S3, upload your config file to S3 and make sure that the following properties are specified accordingly: 
`cortex.config.file.aws.s3.bucket.name` - the file's bucket name
`cortex.config.file.aws.s3.object.key` - the file's object key

Additionally, make sure that the service running the connector has an IAM role that can directly access the object in S3.

#### Limitations

There is currently no support for loading a config file in S3 from a separate AWS account or when the connector is not running in an AWS environment at all.

### Important Notes

Any additional data specified in the above config will be overridden by values that are in the message itself. For example, using the sample config (above), a message written to the `cortex-sink-1` topic with a value of ```{"dept": "sales"}``` would produce a final value of ```{"dept": "sales", "time": 12341234}```, overriding the "engineering" value present in the config.
