# Kontena Load Balancer

[Kontena Load Balancer](http://kontena.io/docs/using-kontena/loadbalancer.html) is fully managed by [Kontena](https://kontena.io) orchestration and enables consistent, portable load balancing on any infrastructure where Kontena Nodes are running.


## Install
> Prerequisites: You need to have working [Kontena](http://www.kontena.io) Container Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/getting-started/quick-start).

`$ kontena stack install kontena/ingress-lb`

## Using Kontena Load Balancer

Services are connected automatically by linking services to the load balancer service and defining load balancing rules via environment variables.

```
stack: foo/bar
version: 0.1.0
services:  
  web:
    image: nginx:latest
    environment:
      - KONTENA_LB_MODE=http
      - KONTENA_LB_BALANCE=roundrobin
      - KONTENA_LB_INTERNAL_PORT=80
      - KONTENA_LB_VIRTUAL_HOSTS=www.kontena.io,kontena.io
    links:
      - ingress-lb/lb
  api:
    image: registry.kontena.local/restapi:latest
    environment:
      - KONTENA_LB_MODE=http
      - KONTENA_LB_BALANCE=roundrobin
      - KONTENA_LB_INTERNAL_PORT=8080
      - KONTENA_LB_VIRTUAL_PATH=/api
    links:
      - ingress-lb/lb
  ```

  For further information, please see the complete [Kontena Load Balancer reference](http://kontena.io/docs/using-kontena/loadbalancer.html).
