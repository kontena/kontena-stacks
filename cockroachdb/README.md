# CockroachDB on Kontena

[CockroachDB](https://www.cockroachlabs.com/product/cockroachdb-core/) is a distributed SQL database built on a transactional and strongly-consistent key-value store. It scales horizontally; survives disk, machine, rack, and even datacenter failures with minimal latency disruption and no manual intervention; supports strongly-consistent ACID transactions; and provides a familiar SQL API for structuring, manipulating, and querying data.

## Install
> Prerequisites: You need to have working [Kontena](https://www.kontena.io) Container Platform installed. If you are new to Kontena, check [quick start guide](https://www.kontena.io/docs/quick-start).


First create a volume config for CockroadbDB deployment:

```
$ kontena volume create --driver local --scope instance cockroachdb-data
```

Then deploy CockroachDB stack:

```
$ kontena stack install kontena/cockroachdb
> Version : 1.1.3
> Cluster size : 3
> Affinity : label==~cockroachdb
 [done] Installing stack cockroachdb
 [done] Triggering deployment of stack cockroachdb
 [done] Waiting for deployment to start
 [done] Deploying service seed
 [done] Deploying service node
 [done] Deploying service lb
```

## Administration

You can find CockroachDB admin web ui at `http://cockroachdb.${GRID}.kontena.local:8080` (accessible via [Kontena VPN](https://www.kontena.io/docs/using-kontena/vpn-access.html))

**Note:** Replace `${GRID}` with your grid name.