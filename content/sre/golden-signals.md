---
title: "Postgres, Kafka, Redis golden signals"
date: 2023-02-01T19:16:51+03:00
tags: ["sre", "postgres", "kafka", "redis", "golden signals"]
categories: ["sre"]
# author: "Me"
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Latency and Traffic metrics"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: false
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: false
editPost:
    URL: "https://github.com/rpalkin/til/tree/master/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

## Postgres

### Latency - max tx duration
```
(pg_stat_activity_max_tx_duration{server=“$postgres”, state="active"})
```

### Traffic - active connections
```
sum (pg_stat_activity_count{server=~"$postgres", state="active",, app="postgres-exporter"})
```

## Kafka

### Latency - lag by consumer group
```
sum(kafka_consumergroup_lag{app_kubernetes_io_instance="$kafka"}) by (consumergroup)
```

### Traffic - messages in by topic
```
sum(increase(kafka_topic_partition_current_offset{app_kubernetes_io_instance="$kafka", topic!~"__.*"}[1m])) by (topic)
```

## Redis

### Latency - avg command duration
```
sum(rate(redis_commands_duration_seconds_total{redisfailovers_databases_spotahome_com_name =~ "$redis"}[1m])) by (pod) /sum(rate(redis_commands_total{redisfailovers_databases_spotahome_com_name =~ "$redis"}[1m])) by (pod)
```

### Traffic - total command per sec
```
sum(rate(redis_commands_total{redisfailovers_databases_spotahome_com_name =~ "$redis"}[1m])) by (pod)
```
