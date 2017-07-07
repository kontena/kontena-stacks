# Redis Sentinel Cluster on Kontena

> Prerequisites: You need to have working [Kontena](https://kontena.io) Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/getting-started/quick-start).

First you need to provide [volume](https://kontena.io/docs/using-kontena/volumes) configurations for Redis Sentinel instances:

```
$ kontena volume create --driver local --scope instance redis-sentinel-data
$ kontena volume create --driver local --scope instance redis-sentinel-monitor
```

Then you can deploy Redis Sentinel stack simply with following command:

```
$ kontena stack install kontena/redis-sentinel
```

Or directly from your filesystem:

```
$ kontena stack install kontena.yml
```