# CockroachDB on Kontena

[CockroachDB](https://www.cockroachlabs.com/product/cockroachdb-core/) is a distributed SQL database built on a transactional and strongly-consistent key-value store. It scales horizontally; survives disk, machine, rack, and even datacenter failures with minimal latency disruption and no manual intervention; supports strongly-consistent ACID transactions; and provides a familiar SQL API for structuring, manipulating, and querying data.

## Install
> Prerequisites: You need to have working [Kontena](http://www.kontena.io) Container Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/getting-started/quick-start).

First install CockroachDB with `Bootstrap new cluster? : Yes` option:

```
$ kontena volume create --driver local --scope instance cockroachdb-data
$ kontena stack install kontena/cockroachdb
> Bootstrap new cluster? : Yes
> Version : 1.0.2
> Cluster size : 3
> Affinity : label!=no-cockroach
 [done] Installing stack cockroachdb     
 [done] Triggering deployment of stack cockroachdb     
 [done] Waiting for deployment to start     
 [done] Deploying service node     
 [done] Deploying service seed     
 [done] Deploying service lb
```

This will deploy CockroachDB cluster to your grid. Other services can connect to it with `cockroachdb.${GRID}.kontena.local:26257` address. After first installation is done it advisable to run `stack upgrade` command and switch `Bootstrap new cluster? : False`

```
$ kontena stack upgrade cockroachdb kontena/cockroachdb
> Bootstrap new cluster? : No
> Version : 1.0.2
> Cluster size : 3
> Affinity : label!=no-cockroach
 [done] Upgrading stack cockroachdb     
 [done] Triggering deployment of stack cockroachdb     
 [done] Waiting for deployment to start     
 [done] Deploying service node     
 [done] Deploying service seed     
 [done] Deploying service lb
 ```

**Note:** Replace `${GRID}` with your grid name.

## Administration

You can find CockroachDB admin web ui at `http://cockroachdb.${GRID}.kontena.local:8080` (accessible via [Kontena VPN](https://www.kontena.io/docs/using-kontena/vpn-access.html))