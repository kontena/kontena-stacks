# Minio on Kontena

[Minio](https://minio.io) is a distributed object storage server built for cloud applications and devops.

## Install
> Prerequisites: You need to have working [Kontena](http://www.kontena.io) Container Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/getting-started/quick-start).

Install Kontena Load Balancer stack
`$ kontena stack install kontena/ingress-lb`

Install Minio stack
`$ kontena stack install kontena/minio`

This will deploy Minio distributed object storage cluster (4 instances) to your Kontena grid.
