# stolon on Kontena

[stolon](https://github.com/sorintlab/stolon/) is a cloud native PostgreSQL manager for PostgreSQL high availability. It's cloud native because it'll let you keep an high available PostgreSQL inside your containers.

## Install
> Prerequisites: You need to have working [Kontena](http://www.kontena.io) Container Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/getting-started/quick-start).

```
$ kontena volume create --driver local --scope instance stolon-keeper
$ kontena stack install kontena/stolon
```

This will deploy stolon (PostgreSQL) cluster to your grid. Other services can connect to it with `stolon.${GRID}.kontena.local:5432` address. Stolon proxy at that address will make sure that client always connects to the database master instance.

**Note:** Replace `${GRID}` with your grid name.

## Administration

Access `stolonctl` via interactive exec:

```
$ kontena service exec --shell -it stolon/keeper 'stolonctl status --cluster-name $STKEEPER_CLUSTER_NAME --store-backend $STKEEPER_STORE_BACKEND --store-endpoints $STKEEPER_STORE_ENDPOINTS'
```

Access `psql` (master node) via interactive exec:

```
$ kontena service exec -it --shell stolon/keeper 'PGPASSWORD=$STKEEPER_PG_SU_PASSWORD psql --host proxy --username stolon postgres'
```