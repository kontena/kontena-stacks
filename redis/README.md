# Redis on Kontena

[Redis](https://redis.io) is an open source (BSD licensed), in-memory data structure store, used as a database, cache and message broker

## Install
> Prerequisites: You need to have working [Kontena](http://www.kontena.io) Container Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/getting-started/quick-start).   

`$ kontena stack install kontena/redis`

This will deploy stateful Redis database to your grid. Other services can connect to it with `redis://redis.${GRID}.kontena.local:6379` address

**Note:** Replace `${GRID}` with your grid name.
