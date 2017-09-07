# WordPress Cluster on Kontena

[WordPress](https://wordpress.org/) is open source software you can use to create a beautiful website, blog, or app.

## Install

> Prerequisites: You need to have working [Kontena](http://www.kontena.io) Platform installed. If you are new to Kontena, check [quick start guide](https://www.kontena.io/docs/quick-start.html).


### Create Volume Configurations

```
$ kontena volume create --driver local --scope instance wordpress-cluster-mysql
$ kontena volume create --driver local --scope stack wordpress-cluster-data
```

### Create Resilio Sync Secret

```
$ docker run -it --rm nimmis/resilio-sync rslsync --generate-secret
```

### Install Load Balancer

```
$ kontena stack install kontena/ingress-lb
```

### Deploy Wordpress Cluster Stack

```
$ kontena stack install kontena/wordpress-cluster
```

This will deploy:
- [MariaDB Galera](https://github.com/severalnines/galera-docker-mariadb) cluster with internal load balancer
- [Resilio Sync](https://github.com/nimmis/docker-resilio-sync) for syncing Wordpress uploads across cluster
- WordPress cluster

Installation can be finished via browser (node public ip or virtual host).


## Uninstall

```
$ kontena stack rm wordpress-cluster
$ kontena volume rm wordpress-cluster-mysql
$ kontena volume rm wordpress-cluster-data
$ kontena etcd rm --recursive /galera/wordpress-cluster
```