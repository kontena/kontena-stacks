# Drone on Kontena

[Drone](https://github.com/drone/drone) is a Continuous Delivery system built on container technology. Drone uses a simple yaml configuration file, a superset of docker-compose, to define and execute Pipelines inside Docker containers.

## Install

> Prerequisites: You need to have working [Kontena](https://kontena.io) Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/quick-start).

> Note: Currently Drone does not work with CoreOS Container Linux stable/beta because they have too old Docker Engine installed.

### Install Kontena Load Balancer

You need to have [Kontena Loadbalancer](https://www.kontena.io/docs/using-kontena/loadbalancer.html) installed. You can install one with following command:

```
$ kontena stack install kontena/ingress-lb
```

### Drone with GitHub integration

```
$ kontena stack install kontena/drone-github
```

### Drone with GitLab

```
$ kontena stack install kontena/drone-gitlab
```