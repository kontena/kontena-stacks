# Fluentd log forwarders for Kontena

[Fluentd](http://www.fluentd.org/) is an open source data collector for unified logging layer.

Kontena supports fluentd log shipping that can be configured on each grid. When fluentd forwarding is enabled, all container logs are automatically sent to fluentd for further processing in addition of storing them in Kontena Master.

## AWS Cloudwatch Logs

You can use Amazon [CloudWatch Logs](http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html) to monitor, store, and access your log files.

### Installation

```
$ kontena stack install kontena/fluentd-cloudwatch
```

### Grid Configuration

```
$ kontena grid update --log-forwarder fluentd --log-opt fluentd-address=fluentd-cloudwatch.${GRID}.kontena.local:24224 ${GRID}
```

## Graylog Extended Log Format (GELF)

### Installation

```
$ kontena stack install kontena/fluentd-gelf
```

### Grid Configuration

```
$ kontena grid update --log-forwarder fluentd --log-opt fluentd-address=fluentd-gelf.${GRID}.kontena.local:24224 ${GRID}
```

## Loggly

[Loggly](https://www.loggly.com/) is a SaaS solution for log data management. With Loggly’s log management software, you’re able to bring logs from the depths of your entire infrastructure to one place where you can track activity and analyze trends.

### Installation

```
$ kontena stack install kontena/fluentd-loggly
```

### Grid Configuration

```
$ kontena grid update --log-forwarder fluentd --log-opt fluentd-address=fluentd-loggly.${GRID}.kontena.local:24224 ${GRID}
```

## Splunk HEC

[Splunk](https://www.splunk.com/) HTTP Event Collector (HEC) is a fast and efficient way to send data to Splunk Enterprise, Splunk Light and Splunk Cloud.

### Installation

```
$ kontena stack install kontena/fluentd-splunkhec
```

### Grid Configuration

```
$ kontena grid update --log-forwarder fluentd --log-opt fluentd-address=fluentd-splunkhec.${GRID}.kontena.local:24224 ${GRID}
```

## Elasticsearch

Fluentd agent forwards logs to Elasticsearch for indexing. Logs are stored in "logstash" way so it's easier to put e.g. Kibana in front.

### Installation

```
$ kontena stack install kontena/fluentd-elasticsearch
```

### Grid Configuration

```
$ kontena grid update --log-forwarder fluentd --log-opt fluentd-address=localhost ${GRID}
```
