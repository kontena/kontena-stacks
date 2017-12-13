# MongoDB Replica Set on Kontena

[MongoDB](https://www.mongodb.com/what-is-mongodb) is a document database with the scalability and flexibility that you want with the querying and indexing that you need.

## Install
> Prerequisites: You need to have working [Kontena](http://www.kontena.io) Container Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/quick-start).

First create a volume configuration for MongoDB:

```
$ kontena volume create --driver local --scope instance mongo-rs-data
```

Then install `kontena/mongo-rs` stack:

```
$ kontena stack install kontena/mongo-rs
> Memory limit (GB) : 1
 [done] Creating stack mongo-rs
 [done] Triggering deployment of stack mongo-rs
 [done] Waiting for deployment to start
 [done] Deploying service peer
```

This will deploy MongoDB replica set to your grid. Other services can connect to it using following replica set member addresses:

- `peer-1.${GRID}.kontena.local:27017`
- `peer-2.${GRID}.kontena.local:27017`
- `peer-3.${GRID}.kontena.local:27017`

**Note:** Replace `${GRID}` with your grid name.

## Administration

You can connect to MongoDB command line interface using following command:

```
$ kontena service exec -it --shell mongo-rs/peer mongo -u admin -p $MONGO_ADMIN_PASSWORD --authenticationDatabase admin
```