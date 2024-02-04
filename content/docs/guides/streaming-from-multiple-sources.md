---
title: "Streaming From Multiple Sources"
description: ""
summary: ""
date: 2024-02-02T02:30:49+01:00
lastmod: 2024-02-02T02:30:49+01:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "streaming-from-multiple-sources-8180916cd0e3f964effd9d610deb9006"
weight: 300
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Architecture

Given an architecture that involves multiple applications writing to multiple topics with multiple different data formats, how can a user stream this data into an instance of a cortex database while preserving the integrity of the data?

{{< picture
  loading="eager"
  fetchpriority="high"
  formats="png"
  src="multi-streaming.png"
  alt="Example architecture streaming data from multiple topics"
>}}

### Incoming Data

Let's say that our applications are iot sensors on rental cars, writing updates directly into kafka so that the rental car company can monitor the status of various features of the car in real time. Here are some sample payloads:

##### Topic 1 - Fuel:

key: null <br/>
value:
```json
{
  "eventId": "8476591e-17d0-4168-bc50-3122042493c9",
  "carId": 12341234,
  "capacity": "90%"
}
```

##### Topic 2 - Location:

key: `ced6a6c2-a6b8-442a-a52d-4f4382fc217c` <br/>
value:
```json
{
  "car_id": 12341234,
  "latitude": "49.101323",
  "longitude": "10.329523"
}
```

##### Topic 3 - Speed:

key: `12341234` <br/>
value:
```json
{
  "avgSpeed": 105,
  "timestamp": 123412341
}
```

##### Topic 4 - Safety

key: null <br/>
value:
```json
{
  "car": 12341234,
  "event_type": "unbuckled_movement"
}
```

### Problems

There are several problems here:

1. The `car_id` parameter is named different things and sometimes not present in the value at all (and instead present in the key)
2. Event timestamps and ids are not consistently provided from the application
3. We may have different uses for the data in each topic. For instance, we may want to store all safety events for monitoring, but may only want to store the car's present location or present fuel capacity.
4. Individual fields do not mean anything outside of their topic context. `capacity` is clear in a topic called, "fuel", but does not mean anything in a database full of event records. 

We can solve for all of these problems by utilizing an advanced config file to stream our data in a controlled a useful way. See below:

### Advanced Config

```yaml
sink:
   default:
      messageTransform:
         additionalData:
            timest: $timestamp
            source: $topicName
      dbWriteStrategy:
        recordUpdateType: create_new
   topics:
      - name: car_fuel
        messageTransform:
          renamedFields:
            capacity: fuelCap
        dbWriteStrategy:
          recordUpdateType: overwrite_first
          primaryKey: carId
      - name: car_location
        messageTransform:
          renamedFields:
            latitude: carLat
            longitude: catLong
        dbWriteStrategy:
          recordUpdateType: overwrite_first
          primaryKey: carId
      - name: car_speed
        messageTransform:
          additionalData:
            source: $topic
          renamedFields:
            avgSpeed: carSpd
            timestamp: timest
        dbWriteStrategy:
          recordUpdateType: create_new
          primaryKey: carId
        ignoreDefault: true
      - name: car_safety
        messageTransform:
          renamedFields:
            car: carId
            event_type: carSfEv
```
