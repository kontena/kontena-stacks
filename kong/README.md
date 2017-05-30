# Kong API gateway on Kontena

[Kong](https://getkong.org/) is the open-source API Gateway and Microservices Management Layer, delivering high performance and reliability.

## Install
> Prerequisites: You need to have working [Kontena](http://www.kontena.io) Container Platform installed. If you are new to Kontena, check [quick start guide](http://www.kontena.io/docs/getting-started/quick-start).   

`$ kontena stack install kontena/kong`

This will deploy Kong API gateway with PostgreSQL and optional [Kong Dashboard](https://github.com/PGBI/kong-dashboard) to your Kontena grid. After it is deployed you can access the Dashboard and Admin API with [Kontena VPN](http://kontena.io/docs/using-kontena/vpn-access.html):
- http://kong.${GRID}.kontena.local:8001
- http://dashboard.kong.${GRID}.kontena.local:8080

**Note:** Replace `${GRID}` with your grid name.
